
## Custom Docker Caching

### 1. Der Input (`inputs`)

**Wofür du es brauchst:** Definiert das gewünschte Docker-Image, wenn du die Action im Workflow aufrufst.

**Wie du es schreibst:**

YAML

```yml
inputs:
  image:
    description: 'The Docker image to cache and load'
    required: true
```

### 2. Der Cache-Key (`Sanitize Image Name`)

**Wofür du es brauchst:** GitHub braucht einen sauberen String als Cache-ID. Sonderzeichen (`/`, `:`) im Image-Namen zerstören Dateipfade. Wir ersetzen sie durch `-` (z.B. `postgres:18` wird `postgres-18`).

**Wie du es schreibst:**

YAML

```yml
- name: Sanitize Image Name
  id: vars
  run: echo "dir_name=$(echo '${{ inputs.image }}' | tr '/:' '-')" >> "$GITHUB_OUTPUT"
```

### 3. Der Check (`cache/restore`)

**Wofür du es brauchst:** Sucht nach einem bestehenden Cache mit dem generierten Key und lädt ihn herunter, falls vorhanden.

**Wie du es schreibst:**

YAML

```yml
- name: Restore from Global Cache
  id: cache-restore
  uses: actions/cache/restore@v6
  with:
    path: /tmp/docker-cache/${{ steps.vars.outputs.dir_name }}
    key: docker-cache-${{ steps.vars.outputs.dir_name }}
```

### 4. Bei Treffer: Lokal laden (`Cache Hit`)

**Wofür du es brauchst:** Wenn der Cache gefunden wurde (`cache-hit == 'true'`), überspringen wir den Download und laden die gespeicherte `.tar`-Datei direkt in Docker.

**Wie du es schreibst:**

YAML

```yml
- name: Load from Global Cache
  if: steps.cache-restore.outputs.cache-hit == 'true'
  run: docker load -i /tmp/docker-cache/${{ steps.vars.outputs.dir_name }}/image.tar || true
```

### 5. Bei Fehlschlag: Download & Export (`Cache Miss`)

**Wofür du es brauchst:** Wenn der Cache _nicht_ existiert (`cache-hit == 'false'`), wird das Image normal aus dem Netz geladen (`pull`) und als `.tar`-Datei für den Cache vorbereitet (`save`).

**Wie du es schreibst:**

YAML

```yml
- name: Pull and Save Image Locally
  if: steps.cache-restore.outputs.cache-hit == 'false'
  run: |
    mkdir -p /tmp/docker-cache/${{ steps.vars.outputs.dir_name }}
    docker pull ${{ inputs.image }}
    docker save ${{ inputs.image }} -o /tmp/docker-cache/${{ steps.vars.outputs.dir_name }}/image.tar
```

### 6. Das Speichern (`cache/save`)

**Wofür du es brauchst:** Lädt die neu erstellte `.tar`-Datei zu GitHub hoch, damit der nächste Run bei Schritt 4 direkt einen Treffer ("Hit") landet.

**Wie du es schreibst:**

YAML

```yml
- name: Save to Global Cache
  if: steps.cache-restore.outputs.cache-hit == 'false'
  uses: actions/cache/save@v6
  with:
    path: /tmp/docker-cache/${{ steps.vars.outputs.dir_name }}
    key: docker-cache-${{ steps.vars.outputs.dir_name }}
```



#  Matrix & Parallele Steps

### 1. Matrix: Der Vorbereitungs-Job (`outputs`)

**Wofür du es brauchst:** Findet Testdateien im Ordner und packt sie in ein JSON-Array. Das wird als Output an den nächsten Job übergeben, damit die Matrix dynamisch wächst.

**Wie du es schreibst:**

YAML

```yml
outputs:
  file_list: ${{ steps.generate-file-list.outputs.file_list }}
steps:
  - id: generate-file-list
    run: |
      FILES=$(find webapp/e2e -type f | jq -R . | jq -s . | jq -c)
      echo "file_list=$FILES" >> $GITHUB_OUTPUT
```

### 2. Matrix: Die Ausführung (`strategy/matrix`)

**Wofür du es brauchst:** Nimmt das JSON-Array aus dem ersten Job via `fromJSON()` entgegen. GitHub startet nun vollautomatisch für jede Testdatei einen eigenen, parallelen Runner.

**Wie du es schreibst:**

YAML

```yml
run-e2e-tests:
  needs: [prepare-e2e-tests]
  strategy:
    fail-fast: false
    matrix:
      file: ${{ fromJSON(needs.prepare-e2e-tests.outputs.file_list) }}
  steps:
    - run: pnpm run e2e:headless ${{ matrix.file }}
```

_Tipp:_ `fail-fast: false` verhindert, dass bei _einem_ kaputten Test sofort alle anderen abbrechen.

### 3. Parallel-Feature: Das Setup (`- parallel:`)

**Wofür du es brauchst:** Standardmäßig laufen Schritte nacheinander. Mit `parallel:` zwingst du GitHub Actions dazu, unabhängige Setup-Schritte (wie Node, Java und Docker Caches) **gleichzeitig auf demselben Runner** auszuführen.

**Wie du es schreibst:**

YAML

```yml
    - parallel:
      - name: Setup Java Environment
        uses: ./.github/actions/setup-java-maven

      - name: Setup Node Environment
        uses: ./.github/actions/setup-node-pnpm

      - name: Load Postgres Docker Cache
        uses: ./.github/actions/global-docker-cache
        with:
          image: ${{ env.POSTGRES_DB_IMAGE }}
```
