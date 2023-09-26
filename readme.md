Tarea Semana 4 - Ethical Hacking: Reto Monkey
Introducción

Este informe documenta el análisis, la explotación y la escalación de privilegios realizados en la máquina MONKEY. El objetivo fue encontrar dos banderas ocultas en el sistema, demostrando habilidades en reconocimiento, análisis de vulnerabilidades y explotación manual.
Paso 1: Reconocimiento

    Identificación de la máquina objetivo:
        Herramientas utilizadas:
            ifconfig: Identificar la IP de la máquina atacante (Kali).
            arp-scan -l: Listar dispositivos en la red junto con sus direcciones MAC.
        Resultado:
            Dirección IP: 192.168.189.135.
            Sistema operativo estimado: Linux/Unix.

    Escaneo de puertos:
        Comando:

        nmap -sV -sVC 192.168.189.135

        Puertos abiertos identificados:
            21/tcp (FTP)
            22/tcp (SSH)
            80/tcp (HTTP).

Paso 2: Análisis de Vulnerabilidades

    Enumeración de servicios:
        Uso de nmap con opciones para identificar versiones y vulnerabilidades.
        Resultado: No se encontraron exploits automatizados relevantes.

    Exploración web:
        Herramienta: Dirbuster.
        Resultado: Identificación de directorios adicionales, incluyendo phpmyadmin y monkey.

Paso 3: Explotación

    Acceso inicial:
        Utilización de credenciales predeterminadas para acceder al servicio FTP.
        Archivos encontrados:
            Contraseña cifrada descifrada posteriormente como junior01.

    Ataque de fuerza bruta:
        Herramienta: Burp Suite con Cluster Bomb.
        Resultado: Acceso al panel de administración ip/monkey/index.php.

    Ejecución de shell reverso:
        Aprovechamiento de la función "subir imagen" para cargar un archivo malicioso.
        Logro: Acceso al sistema a través de HTTP.

Paso 4: Escalación de Privilegios

    Acceso SSH:
        Uso de credenciales obtenidas (hackermentor:M1_P4ssw0rd_segur@).
        Logro: Acceso al servidor con privilegios limitados.

    Ejecución de script malicioso:
        Identificación de un script ejecutado por el usuario root cada 60 segundos.
        Modificación del script para escalar privilegios y acceder a la bandera2.

Paso 5: Obtención de las Banderas

    Comando para localizar las banderas:

    find / -name bandera*.txt 2>/dev/null

    Ubicación y contenido:
        Bandera 1: ~/bandera1.txt
        Contenido: 47ee0702e489445bae251df46bc88b73.
        Bandera 2: /root/bandera2.txt
        Contenido: d844ce556f834568a3ffe8c219d73368.

Herramientas Utilizadas

    Reconocimiento:
        ifconfig, arp-scan, nmap.
    Análisis web:
        Dirbuster, Burp Suite.
    Explotación:
        crackmapexec, ssh.

Conclusiones

    Éxitos:
        Se lograron identificar y explotar vulnerabilidades en servicios web y de red.
        Escalación de privilegios exitosa mediante la modificación de un script.

    Lecciones aprendidas:
        La importancia de deshabilitar o proteger funciones predeterminadas como FTP y páginas administrativas.
        La necesidad de monitorear scripts automatizados en sistemas sensibles.

Recomendaciones

    Mitigación de vulnerabilidades:
        Actualizar y proteger servicios como FTP y PHPMyAdmin.
        Deshabilitar funciones innecesarias y eliminar credenciales predeterminadas.
    Prácticas de seguridad:
        Implementar monitoreo constante de scripts y procesos críticos.
        Realizar auditorías periódicas para identificar configuraciones inseguras.