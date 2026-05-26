
**Plattformunabhängigkeit**: Verwende `File.separator` anstelle von hartcodierten `/` oder `\`, um plattformübergreifende Kompatibilität sicherzustellen.
    
**Saubere Pfade**: Baue Dateipfade dynamisch zusammen, statt sie manuell zu verketteln. Verwende dafür `Paths.get()` oder `File`-Konstruktoren, um die richtige Trennung zu garantieren.
    
**Vermeidung von Problemen**: Manuelle Eingabe von `\` kann zu Fehlern führen, da `\` in vielen Sprachen (z.B. Java, HTML) als Escape-Sequenz gilt. Nutze deshalb den Java File Separator oder das Utility `Paths`.





````java
((?=.*[Kk]?[Ee]?[Yy].?[Rr]?[Ee]?[Ss]?[Uu]?[Ll]?[Tt]?.*)(.*[Kk]eyResult.*|[A-Z_]*KEY_RESULT[A-Z_]*)|^(?!.*[Kk][Ee][Yy].?[Rr][Ee][Ss][Uu][Ll][Tt]).*)"


((?=.*[Cc]?[Hh]?[Ee]?[Cc]?[Kk].?[Ii]?[Nn]?.*)(.*[Cc]heckIn.*|[A-Z_]*CHECK_IN[A-Z_]*)|^(?!.*[Cc][Hh][Ee][Cc][Kk].?[Ii][Nn]).*)"
````

