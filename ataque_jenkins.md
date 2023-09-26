Ataque a Jenkins - Paso a Paso


Introducción

Este documento detalla el análisis, la explotación y las banderas obtenidas durante un ejercicio de seguridad en un entorno con Jenkins como objetivo. El propósito es demostrar habilidades en reconocimiento, análisis de vulnerabilidades, explotación y escalación de privilegios.


Paso 1: Reconocimiento

    Identificación de IP y MAC:
        Se realizó un escaneo inicial con ifconfig en la máquina Kali y herramientas como arp-scan para identificar las direcciones IP y MAC activas.
        Objetivo identificado: 192.168.189.139.

    Escaneo de Puertos:
        Se utilizó nmap para realizar un escaneo de puertos.
        Resultado: 12 puertos abiertos, incluido el puerto 8080 con un servicio HTTP vinculado a Jenkins.

    Acceso al Panel de Jenkins:
        Al acceder al servicio HTTP, se encontró la página de inicio de Jenkins en el puerto 8080.



Paso 2: Análisis de Vulnerabilidades

    Enumeración de Servicios y Versiones:
        Herramienta utilizada: nmap con scripts NSE.
        Resultado: Jenkins ejecutándose en un sistema Windows 10 (64 bits), hostname: BUTLER.

    Ataque de Fuerza Bruta al Login:
        Herramientas:
            CEWL: Generó una lista personalizada de posibles nombres de usuario desde el sitio web.
            Burp Suite: Probó combinaciones de usuario y contraseña.
        Credenciales válidas encontradas: usuario: Jenkins | contraseña: Jenkins.



Paso 3: Explotación

    Acceso a la Consola de Jenkins:
        Se utilizó la consola de scripting disponible en Jenkins para ejecutar comandos.
        Herramienta auxiliar: revshell.com para generar un reverse shell.
        Logro: Se obtuvo acceso como usuario BUTLER.

    Ejecución de Comandos Remotos:
        Uso de comandos en la consola para explorar directorios y encontrar archivos sensibles.
        Descubrimiento de restricciones de privilegios en ciertos archivos.



Paso 4: Escalación de Privilegios

    Análisis de Privilegios del Usuario Actual:
        Herramienta: LINPEAS.
        Resultado: El usuario BUTLER tiene el permiso SeImpersonatePrivilege.

    Abuso de Privilegios:
        Herramienta utilizada: PrintSpoofer.
        Escenario: Se ejecutó un script para obtener acceso como NT AUTHORITY\SYSTEM.
        Logro: Acceso total al sistema.



Paso 5: Obtención de las Banderas

    Bandera 1:
        Ubicación: C:\Users\butler\Desktop\bandera1.txt.
        Contenido: c3e92e2d4d3f0694dcda839ee173ec77.

    Bandera 2:
        Ubicación: C:\Users\Administrator\Desktop\bandera2.txt.
        Contenido: 8b86666d49366c4555fd88d68265bd21.






Herramientas Utilizadas

    Nmap: Escaneo de puertos y servicios.
    CEWL: Generación de listas de usuarios.
    Burp Suite: Ataque de fuerza bruta.
    LINPEAS: Identificación de privilegios.
    PrintSpoofer: Escalación de privilegios.
    Reverse Shell: Creación de shells remotos.





Conclusiones

    Éxito en la explotación:
        Se obtuvo acceso como NT AUTHORITY\SYSTEM en la máquina objetivo.
        Se lograron capturar las dos banderas.

    Errores detectados en el sistema objetivo:
        Contraseñas por defecto.
        Permisos mal configurados.
        Ausencia de parches de seguridad.

    Recomendaciones:
        Cambiar configuraciones por defecto y establecer contraseñas fuertes.
        Limitar permisos de usuarios.
        Realizar actualizaciones de seguridad y auditorías regulares.