```markdown
# JDBC (Java Database Connection)


## JDBC

- JDBC-Klassen und -Schnittstellen befinden sich im Paket `java.sql`.
- JDBC-Treiber sind separate Komponenten, die zur Laufzeit verfügbar sein müssen.
- Maven wird für Abhängigkeiten in einem Maven-Projekt verwendet.

## Maven-Abhängigkeit

xml

`<dependency>
	<groupId>mysql</groupId>     
	<artifactId>mysql-connector-java</artifactId>     
	<version>8.0.23</version> 
</dependency>`

## JDBC-Arbeitsschritte

1. **Treiber laden/registrieren:**
    
    - JDBC-Treiber registrieren, z.B., `Class.forName("com.mysql.cj.jdbc.Driver");`.
2. **Datenbankverbindung herstellen:**
    
    - Konfiguration von URL, Benutzername und Passwort.
    - `DriverManager.getConnection(url, username, password);` für Verbindung.
3. **SQL-Anweisung vorbereiten:**
    
    - Parametrisierte SQL-Anweisungen mit `PreparedStatement`.
4. **SQL-Anweisung ausführen:**
    
    - `executeQuery` für SELECT, `executeUpdate` für UPDATE, INSERT, DELETE.
5. **Rückgabewerte verarbeiten:**
    
    - Iteration durch ResultSet für SELECT-Ergebnisse.
6. **Verbindungen schließen:**
    
    - Ressourcen wie Connection, Statement, PreparedStatement explizit schließen.
```