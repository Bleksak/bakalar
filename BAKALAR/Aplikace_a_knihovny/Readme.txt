Pro sestavení je potřeba Apache Maven verze 3.8 nebo vyšší a OpenJDK verze 17.

Sestavení nástroje: mvn -f agent clean compile assembly:single
Sestavení testovacích aplikací: mvn -f tests clean install

Spuštění nástroje: java -javaagent:"agent/target/agent-jar-with-dependencies.jar" -jar <Aplikace.jar>
Pro spuštění aplikace s využitím externích knihoven je potřeba nakonfigurovat filtr tříd tak, aby se neinstrumentovaly třídy z dané knihovny.
Zároveň je potřeba otevřít externí moduly pro reflexi pomocí spouštějícího parametru --add-opens.

Například pro využití standardní knihovny Javy:
--add-opens java.base/java.util=ALL-UNNAMED
--add-opens java.base/java.lang=ALL-UNNAMED
--add-opens java.base/java.io=ALL-UNNAMED

Příklad spuštění testu Util:
java --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED -javaagent:"agent/target/agent-jar-with-dependencies.jar" -jar tests/Util/target/app.jar
