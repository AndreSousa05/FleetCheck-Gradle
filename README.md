# FleetCheck – Build Systems Lab

This project is intentionally incomplete. Follow the worksheet in the order given.

Expected final application output:

```
FleetCheck 1.0
Vehicles loaded: 4
Vehicles requiring service: 2
Average mileage: 37000 km
```

Do not copy the solution POM. The objective is to observe how each build change alters the result.

Relevant error :[ERROR] /C:/Users/andre/Desktop/3º Ano - 1º Semestre/Qualidade de software/w4/FleetCheck_Starter/FleetCheck_Starter/src/main/java/pt/upt/fleetcheck/App.java:[4,38] package com.fasterxml.jackson.databind does not exist

APP Java : package com.fasterxml.jackson.databind

Question: Why is this a better failure than the one from Step 1?
    The code is syntacticlly correct and we pass the compilation phase failing only in the test phase 

Evidence 4: Explain what the Shade plugin changed compared with the default JAR.
   without the plugin, mvn produces only fleetcheck-1.0.0.jar, with has no Main-Class, with the plugin, the build produces an executable, self-contained JAR, fleetcheck-1.0.0-all.jar

Question: Which hidden environmental assumption did the wrapper remove?
    the wrapper remove the assumption that the maven is installed on the machine

Evidence 7: Why does the SBOM contain components that you did not explicitly type in the original dependencies section?
    Maven resolve transitive dependencies, when we declare a direct dependency, that library depends on oter libraries to function and Maven automatically downloads them

Evidence 8.1: Copy one relevant error line and identify the missing dependency.
    Linha de erro: error: package com.fasterxml.jackson.databind does not exist (import ObjectMapper). Dependência em falta: com.fasterxml.jackson.core:jackson-databind, usada por ObjectMapper e TypeReference.

Evidence 8.2: Compare this output with mvn dependency:tree. Did changing the build system change the application dependencies?
    In both Maven and Gradle, jackson-databind is the only direct dependency; jackson-core and jackson-annotations are transitive (pulled in automatically). Changing the build system did not change the application's actual dependencies — only the declaration syntax and the command/format used to inspect the graph changed.

Evidence 8.3: Explain what changed in the JAR after the runtime dependencies were included.
    Before, the default JAR only contained FleetCheck's own classes, with no Main-Class, so java -jar failed. After the jar { ... } block, Gradle merges the runtimeClasspath (via zipTree) into the JAR and writes Main-Class: pt.upt.fleetcheck.App into the manifest — turning it into a self-contained, executable "fat JAR" that runs with java -jar with no extra setup.

Question: Which hidden environmental assumption did the Gradle Wrapper remove?
    It removes the assumption that Gradle is already installed on the machine, in the right version.