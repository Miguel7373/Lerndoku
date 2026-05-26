

# Prometheus
### Starten von Prometheus

Du kannst dir das tar auf der github page holen und es dann extrahieren
Dann kanst du im `prometheus.yml` file deine settings machen und danach mit `./prometheus` das too starten


# PromQL
### Filtern anhand von Labels

Hier ein paar Beispiele:

```
temp_celsius{raum="wohnzimmer"}
```

Selektiert die Time Series mit dem Namen `temp_celsius` und dem Label `raum="wohnzimmer"`.

```
temp_celsius{raum!="wohnzimmer"}
```

Selektiert die Time Series mit dem Namen `temp_celsius`, welche im Label `raum` nicht den Wert `wohnzimmer` besitzen.

```
temp_celsius{raum=~".+zimmer"}
```

Selektiert die Time Series mit dem Namen `temp_celsius` welche im Label `raum` einen Wert besitzen, welcher auf `zimmer` endet.

```
temp_celsius{raum!~".+zimmer"}
```

Selektiert die Time Series mit dem Namen `temp_celsius` welche im Label `raum` einen Wert besitzen, welcher nicht auf `zimmer` endet.



### Vergleichen
Du kannst mit den standard Vergleichs Operatoren auch hier vergleichen 

### Funktionen 
https://prometheus.io/docs/prometheus/latest/querying/functions/