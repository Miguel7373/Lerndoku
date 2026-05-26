
# Testcontainers
> **Kurzfassung:** Testcontainers startet echte, leichtgewichtige Docker-Container (z. B. Postgres) direkt aus Ihren Tests. So testen Sie Ihre Anwendung gegen **reale** Infrastruktur statt.

---

## Was ist Testcontainers?

Testcontainers ist eine Bibliothek, die in Tests automatisch **Docker‑Container** mit den benötigten Abhängigkeiten startet und verwaltet. Anstatt z. B. eine lokale DB manuell zu installieren, bekommt jeder Test eine **saubere, reproduzierbare** Instanz – inkl. automatischer Aufräumung.

**Unterstützte Sprachen/Ökosysteme (Auszug):** Java, Kotlin, .NET, Node.js/TypeScript, Python, Go, Rust, Ruby.

---

## Voraussetzungen & Grundprinzip

- **Docker** muss auf der Testmaschine laufen (Desktop oder Remote Daemon).
    
- Tests deklarieren benötigte Services als Container (Image + Ports + Env + Healthchecks).
    
- Testcontainers sorgt für **Lifecycle**: Start vor dem Test, Wait‑Strategy/Healthcheck, Stop/Cleanup danach (oder Reuse).
    

**Sicherheits‑/Ops‑Hinweis:** Verwenden Sie nur **vertrauenswürdige Images** (z. B. offizielle Postgres/MariaDB/Kafka etc.) und pinnen Sie Versionen (z. B. `postgres:16-alpine`).

---

## Kernkonzepte

- **Generische Container**: Beliebige Images starten (`GenericContainer`).
    
- **Module**: Vorgefertigte Klassen/Helfer für populäre Technologien (Postgres, Kafka, RabbitMQ, Selenium usw.).
    
- **Wait Strategies**: Warten, bis ein Service bereit ist (Port offen, Log‑Regex, HTTP 200, Healthcheck).
    
- **Netzwerke & Aliasse**: Mehrere Container zu einem Test‑Netzwerk verbinden.
    
- **Reuse**: Container zwischen Tests wiederverwenden, um Startzeit zu sparen (optional).
    
- **Ryuk / Reaper**: Nebenprozess räumt Container/Netze/Volumes am Ende auf.
    

---

## Schnellstart

1. **Docker installieren** (inkl. Zugriff für Ihr CI).
    
2. **Bibliothek hinzufügen** (z. B. Maven/Gradle, npm/yarn/pnpm, pip/poetry, go, bundler).
    
3. **Test schreiben**: Container deklarieren, Wait‑Strategy definieren, Verbindung in der App konfigurieren, Assertions schreiben.
    
4. **Tests starten**: Lokal und im CI identisch.
    

---

## Sprach/Framework‑Beispiele

### Java 

```java

import org.springframework.test.context.ActiveProfiles;  
import org.springframework.test.context.DynamicPropertyRegistry;  
import org.springframework.test.context.DynamicPropertySource;  
import org.testcontainers.containers.PostgreSQLContainer;  
import org.testcontainers.junit.jupiter.Container;  
import org.testcontainers.junit.jupiter.Testcontainers;

@SpringBootTest  
@Testcontainers  
@ActiveProfiles("test")  
class ExamplePersistenceServiceIT {  
  
    @Container  
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:17-alpine");  
  
    @DynamicPropertySource  
    static void configureProperties(DynamicPropertyRegistry registry) {  
        registry.add("spring.datasource.url", postgres::getJdbcUrl);  
        registry.add("spring.datasource.username", postgres::getUsername);  
        registry.add("spring.datasource.password", postgres::getPassword);  
    }  
  
    @Autowired  
    private ExamplePersistenceService persistenceService;  
  
    @DisplayName("Should establish DB connection")  
    @Test  
    void shouldEstablishConnection() {  
        assertThat(postgres.isRunning()).isTrue();  
    }
}
```
