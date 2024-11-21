nombre: SonarQube Cloud
sobre:
  empuje:
    ramas:
      - principal
  tirar. solicitud:
    tipos: [abrir, sincronizar, reabrir]
los puestos de trabajo:
  construir:
    nombre: BuildConstruir y analizar
    en: ventanas-últumos
    pasos:
      - nombre: Configuración upJDK 17
        usos: actions/setup-java-v4
        con:
          java-versión: 17
          distribución: 'zulu' - Opciones de distribución alternativas están disponibles.
      - usos: actions/checkout.v4
        con:
          a fondo: 0 Los clones huebé deben desactivarse para una mejor relevancia del análisis
      - nombre: paquetes de caché SonarQube Cloudpackages
        usos: actions/cache-v4
        con:
          ruta:~\sonar\cache
          clave: $- runner.os}}-sonar
          restaura-claves: $. runner.os}}-sonar
      - nombre: Cache SonarQube Cloud escáner
        id: cache-sonar-scanner
        usos: actions/cache-v4
        con:
          ruta: .sonar.scanner
          clave: $. runner.os}}-sonar-scanner
          restaura-teclas: $- runner.os}}-sonar-scanner
      - nombre: Instalar escáner de SonarQube Cloud
        if: steps.cache-sonar-scanner.outputs.cache-hit .= 'true'
        Concha: powerhell
        Correr: .
          New-Item -Path ..sonar-scanner -ItemType Directory
          actualización de la herramienta dotnet-sonarscanner --tool-path ..sonar-scanner
      - nombre: Construir y analizar
        env:
          GITHUB.TOKEN: Secrets de $.GITHUB.TOKEN - Necesitado para obtener información de relaciones públicas, si lo hubiera
          SONAR.TOKEN: $- Secrets.SONAR.TOKEN}}
        Concha: powerhell
        Correr: .
          ..sonar.scantnet-sonarscanner begin /k:"SergioRivera8888S-Proyecto-Prueba" /o:"sergiorivera8888" /d:sonar.token="$-secres.SONAR-TOKEN"" /dsonar.host.url=https://sonarcloud.io"
          construcción de dotnet
          ..sonar.scanner.dotnet-sonarscanner end /d:sonar.token="$" secrets.SONAR.TOKEN ".
