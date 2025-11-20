# Monitorización de eventos en tiempo real.

    Comprender cómo funciona la monitorización de eventos en tiempo real, su importancia en un entorno 
    SOC y aprender a configurar sistemas de monitorieo para detectar y responder a incidentes de una 
    manera inmediata.


## Qué es la monitorización de eventos en tiempo real.

    Es el proceso de recopilar, análizar y correlacionar eventos de seguridad provenientes de diversas 
    fuentes para detectar y responder a posibles amenazas de manera inmediata.


-- Beneficios principales.

    -- Detección temprana de amenazas: Identificar actividades sospecosas antes de que se conviertan en 
    incidentes criticos.
    -- Visión centralizada: Unificar datos de múltiples fuentes para un análisis más efectivo.
    -- Respuesta inmediata: Automatizar acciones o facilitar decisiones rápidas ante incidentes.

-- Como funciona:

    1 - Recopilación: Los dispositivos y sistemas envian logs al SIEM (Syslog, Windows Event Forwarding, etc).
    2 - Análisis: El SIEM aplica reglas para identificar patrones sospechosos.
    3 - Correlación: Relacióna eventos ente diferentes sistemas, (por ejemplo, intento de acceso en el Firewall y en un servidor).
    4 - Alertas: Notifica a los analistas o ejecuta respuestas automáticas según la criticidad.


## Configuración en la monitorización en tiempo real.

    1 - Configuración de fuentes de datos:

        -- Windows: Configura la recopilación de logs a travez de "Windows Event Forwarding(WEF)" o 
        agentes especificos como "Winlogbeat".
        -- FortiGate: Habilita el envio de logs a través de Syslog o directamente al "SIEM".

    2 - Definición de reglas de correlación:
    
        -- Regla 1: Detectar múltiples intentos fallidos de inicio de sesión desde la misma "IP" en 
        5 minutos.
        -- Regla 2: Alertar sobre conexiones a puertos no autorizados en el "Firewall",(por ejemplo, 
        RDP, Remote Desktop Protocol.)
        
    3 - Configuraciónes de alertas:
    
        -- Notificar a trávez de correos electrónicos o dashboards en tiempo real.
        -- Escalar als alertas criticas automáticamente para análisis inmediato.
        
    4 - Validación y pruebas:
    
        -- Genera eventos de pruebas, como intentos fallidos de inicio de sesión o tráfico a puertos 
        bloqueados, para verificar que las alertas funcionan correctamente.


## Ejemplo de logs: Windows.

    -- Log de intentos fallidos de inicio de sesión(Event ID 4625).


        Log Name: Security  
        Source: Microsoft-Windows-Security-Auditing  
        Event ID: 4625  
        Level: Information  
        Account Name: admin  
        Logon Type: 3 (Network)  
        Source Network Address: 203.0.113.45  
        Failure Reason: Unknown user name or bad password 

    -- Analisis del log:

        Tipo de log: Inicio de sesión fallido.
        Usuario afectado: admin.
        Fuente del intento: IP 203.0.113.45
        Posible amenaza: Fuerza bruta.

    -- Reglas de correlación:

        Si más de 5 ventos con ID 4625 desde la misma IP ocurren en 5 minutos, generar una alerta.

    -- Respuesta sugerida:

        1 - Bloquear la IP 203.0.113.45 en el firewall.
        2 - Revisar logs adicionales en el servidor para intentos exitosos posteriores.
        3 - Habilitar medidas adicionales como CAPTCHA o MFA para al cuenta afectada.


## Ejemplo de Logs: FortiGate.

    Para habilitar los logs en un Firewall "FortiGate a un SIEM", se utiliza por lo general el protocolo "syslog" y se configura. 


    -- Log de conexión a puerto bloqueado.

        date=2024-12-01 time=14:35:21 log_id=0100040000 type=traffic subtype=deny  
        src=198.51.100.12 src_port=56243 dst=192.168.1.10 dst_port=3389  
        service=RDP action=deny  
        msg="Denied by policy 101"

    -- Análisis del log:

        Tipo de evento: Intento de acceso denegado.
        Fuente del tráfico: IP 198.51.100.12
        Destino: Puerto 3389(RDP) en el servidor 192.168.1.10
        Razón: Bloqueado por politica del firewall.

    -- Regla de correlación:

        Generar alerta si se detecta más de 3 intentos en puertos criticos, por ejemplo, RDP, SSH, en menos de 
        1 minuto.

    -- Respuesta sugerida:

        1 - Análisar si la IP 198.51.100.12 ah generado más trafico sospechoso.
        2 - Bloquear la IP si persiste el comportamiento.
        3 - Verificar la exposición del puerdo "RDP" en la red y limitar accesos solo a direcciones especificas.


## Caso práctico: Configuración de reglas.

    Un analista esta configurando la monitorización de eventos en tiempo real para un servidor Windows y un 
    firewall FortiGate.

    -- Objetivo.

        -- Configurar reglas de correlación para detectar:

            1 - Intentos fallidos de inicio de sesión en el servidor Windows.
            2 - Tráfico hacia puertos bloqueados en el firewall.

        -- Tareas del estudiante.

            1 - Identificar los eventos clave en los logs de Windows y FortiGate.
            2 - Configurar uan regla teórica para correlacionar estos eventos.
            3 - Proponer una respuesta inmediata para mitigar posibles amenazas detectadas.


## Buenas prácticas en la monitorización en tiempo real.

    -- Asegurar fuentes de datos completas:
        Verificar que todos los dispositivos criticos estan enciando logs al "SIEM".

    -- Reducir falsos positivos:
        Ajusta las reglas para evitar alertas por comportamiento legitimo.

    -- Documentar reglas y procedimientos:
        Asegúrarte de que todas las reglas estén documentadas y actualizadas según las necesidades de la organización.

    -- Implementar respuesta automática:
        Configurar el "SIEM" para bloquear automáticamente IPs maliciosas o enviar alertas inmediatas a los 
        análista.

## Actividad individual.

    Titulo:

        Inplementación de reglas para la monitorización en tiempo real.

    -- Instrucciones:

        -- Analiza los logs proporcionados para Windows y FortiGate.
        -- Define reglas de correlación para detectar:
            -- Más de 3 intentos fallidos de inicio de sesión desde la misma IP en 5 minutos.
                Bloquear IP y rastrear su origen.
            -- Tráfico recurrente a puertos bloqueados, por ejemplo, RDP, SSH.
                Revisar logs en busqueda de intentos exitosos.
        -- Escribe un breve informe que incluya:
            -- Descripción de los eventos clave que estás monitoreando.
                Log de intentso fallidos de inicio de sesión.
            -- Reglas configuradas y razones detrás de ellas.
                Si hay mas de 5 eventos con el mismo ID del log, generar una alerta.
            -- Acciones recomendadas para mitigar las amenazas detectadas.
                Bloquedo y aislamiento del servidor comprometido y rastreo de la IP atacante.


## Conclusión del módulo.

    La monitorización en tiempo real es una herramienta poderosa para detectar amenazas y responder, 
    de manera proactiva, con eejmplos prácticos de logs y reglas de correlación, este modulo ha preparado 
    a los estudiantes para implementar configuraciónes efectivas en entornos SOC.


## Análisis de eventos y detección de patrones sospechosos.

    Aprender a analizar eventos de seguridad para identificar patrones sospechosos, utilizando ejemplos reales de logs de Firewall, FortiGate, Windows Server y el SIEM Wazuh.


## Importanciadel análisis de eventos.

    El análisis de eventos implica examinar logs generados por dispositivos y sistemas para identificar 
    comportamientos anómalos o maliciosos, la correlación entre eventos aparentemente aislados puede 
    revelar patrones sospechosos que representen amenazaas reales.


-- Beneficios del análisis de patrones.
    
    1 - Detección temprana de ataques: Identifica comportamientos sospechosos antes de que causen daños.

    2 - Contextualización de amenazas: Amplia el análisis utilizando herramientas externas como 
    VirusTotal y ANY.RUN.

    3 - Optimización del monitoreo: Mejora reglas y procesos de detección basados en evidencia.

-- Tipos comunes de patrones sospechosos.

    -- Actividad repetitiva desde la misma IP o cuenta.
    -- Uso anómalo de recursos del sistema.
    -- Comportamiento fuera del horario habitual.


## Fuentes de datos clave.

    -- Firewall FortiGate: Detedcta intentos de conexión sospechosos, tráfico a puertos bloqueados y 
    actividad maliciosa.

    -- Windows Server: Registra intentos de inicio de sesión, creación de procesos y modificaciónes del sistema.

    -- Wazuh(SIEM): Correlaciona eventos de múltiples fuentes. genera alertas y proporciona visibilidad 
    centralizada.

    -- VirusTotal y ANY.RUN: 
        -- VirusTotal: Herramienta para analizar hashes de archivos, direcciónes IP, URLs y dominios 
        en busca de indicadores de compromiso conocidos.

    -- ANY.RUN: Sandbox interactivo para analizar archivos maliciosos y obtener información detallada 
    sobre su comportamiento.


## Ejemplos de análisis de eventos.

    -- Ejemplo 1 - FortiGate – Tráfico a Puertos Bloqueados:

        -- Log del Firewall:

            date=2024-12-02 time=15:12:34 log_id=0100040000 type=traffic subtype=deny  
            src=203.0.113.12 src_port=55023 dst=192.168.1.20 dst_port=3389  
            service=RDP action=deny msg="Blocked by policy 110"

        -- Análisis: 

            - Evento: Intento de acceso al puerto 3389 (RDP), bloqueado por la política del firewall.
            - Fuente: IP 203.0.113.12.
            - Destino: Servidor 192.168.1.20.
            - Patrón Detectado: Repetidos intentos desde la misma IP indican posible ataque de fuerza 
            bruta.

        -- Acciones:

            1 - Bloquear la IP 203.0.113.12.
            2 - Verificar si el puerto 3389 está expuesto públicamente y limitar el acceso.
            3 - Consultar VirusTotal para investigar la IP y determinar si está asociada con actividades maliciosas.

        -- Uso de Virus Total:

            - Ingresa la IP 203.0.113.12 en VirusTotal para verificar si está reportada como maliciosa.
            
            - Analiza los resultados: Si la IP está asociada con botnets o intentos de ataque, aumenta la prioridad de la alerta.


    -- Ejemplo 2 - Windows Server – Inicio de Sesión Fallido:

        -- Log de Seguridad (Event ID 4625):

            Log Name: Security  
            Source: Microsoft-Windows-Security-Auditing  
            Event ID: 4625  
            Account Name: administrator  
            Logon Type: 3 (Network)  
            Source Network Address: 198.51.100.45  
            Failure Reason: Unknown user name or bad password

        -- Análisis:

            - Evento: Inicio de sesión fallido en la cuenta administrator.
            - Fuente: IP 198.51.100.45.
            - Patrón Detectado: Múltiples intentos fallidos en un corto período podrían indicar fuerza bruta.

        -- Acciones:

            1 - Revisar si hubo intentos exitosos posteriores.
            2 - Consultar VirusTotal para investigar la IP 198.51.100.45.
            3 - Si la IP está clasificada como maliciosa, configurarla en listas de bloqueo.

    -- Ejemplo 3 - Wazuh – Detección de Malware por Hash:

        -- Alerta en Wazuh:

            Alert ID: 10002  
            Rule: File Integrity Monitoring  
            File: C:\Temp\invoice2024.exe  
            Hash: f7e2d7b0b8a8b0c3d5a8977f80c9ad55  
            Action: Detected

        -- Análisis:

            - Evento: Detección de un archivo sospechoso en el sistema.
            - Archivo: invoice2024.exe.
            - Hash: f7e2d7b0b8a8b0c3d5a8977f80c9ad55

        -- Acciones:

            1 - Consultar VirusTotal para verificar el hash del archivo.
                - VirusTotal indica que el hash corresponde a un malware conocido.

            2 - Enviar el archivo a ANY.RUN para analizar su comportamiento.
                - El sandbox muestra que el archivo intenta conectarse a un servidor C2.

            3 - Aislar el sistema afectado, eliminar el archivo y verificar si hubo exfiltración de datos.


## Caso práctico:

    -- Escenario: El 'SIEM' ha generado alertas para los siguientes eventos:

        1 - Tráfico sospechoso detectado por el firewall hacia un puerto bloqueado.
        2 - Múltiples intentos fallidos de inicio de sesión en un servidor Windows.
        3 - Un archivo sospechoso identificado en un endpoint.

    -- Tareas del estudiante:

        1 - Analiza los logs proporcionados.
        2 - Usa VirusTotal para investigar una IP o hash sospechoso.
        3 - Si se detecta un archivo sospechoso, describe cómo lo analizarías en ANY.RUN y qué datos buscarías.

        4 - Documenta los pasos de respuesta y tus hallazgos.


## Buenas prácticas para detección de patrones.

    1 - Correlacionar eventos: Usa el SIEM para relacionar actividad entre diferentes sistemas (e.g., firewall y servidor).

    2 - Automatizar consultas en VirusTotal: Configura el SIEM para consultar automáticamente IPs y hashes en plataformas de inteligencia de amenazas.

    3 - Analizar en sandbox: Antes de ejecutar archivos desconocidos, utiliza ANY.RUN para evaluar comportamientos peligrosos.

    4 - Priorizar alertas críticas: Enfócate en eventos que involucren cuentas privilegiadas o sistemas críticos.

## Actividad individual.

    -- Título: "Análisis y Detección de Patrones Sospechosos"

        -- Instrucciónes:

            1 - Revisa los logs de los ejemplos anteriores (FortiGate, Windows Server, Wazuh).
            2 - Utiliza VirusTotal para investigar una IP o hash sospechoso y documenta los hallazgos.
            3 - Describe cómo utilizarías ANY.RUN para analizar un archivo sospechoso y qué información buscarías en el reporte.

            4 - Escribe un informe breve sobre los patrones sospechosos detectados y las acciones recomendadas.


## Conclusión del modulo.

    El análisis de eventos y detección de patrones sospechosos es esencial para un analista CyberSOC. Herramientas como VirusTotal y ANY.RUN enriquecen el análisis al proporcionar inteligencia accionable sobre archivos, IPs y dominios.


    -- Tarea adicional: Explora otras herramientas de análisis de malware o IPs, como Hybrid Analysis o AbuseIPDB. Compara sus características con VirusTotal y ANY.RUN, y describe cómo podrías integrarlas en tu flujo de trabajo.




##   Prácticas de monitorización en entornos simulados.

-- Objetivo del Módulo:

    Poner en práctica las habilidades de monitorización mediante el análisis de eventos reales simulados, incluyendo ejemplos de ataques con ransomware, Golden Ticket (técnica de ataque a Kerberos) y exploración de red con Nmap. Se guiará al estudiante en la identificación de patrones sospechosos y la implementación de respuestas.

## Introducción.

    El análisis de eventos en entornos simulados proporciona una experiencia práctica que permite a los analistas mejorar su capacidad para detectar y responder a incidentes de seguridad.

## Escenarios simulados.

    -- Escenario 1: Ataque de Ransomware Detectado:
        
        -- Descripción:

            Un usuario ejecuta un archivo adjunto de un correo electrónico malicioso, lo que inicia un ransomware que encripta archivos en el sistema. Los eventos generados incluyen la detección de un archivo ejecutable sospechoso y actividad anómala en el sistema.

        -- Logs generados:

            -- Wazuh (File Integrity Monitoring):

                Alert ID: 40001  
                Rule: Suspicious File Creation  
                File: C:\Users\Victim\Documents\important.docx.locked  
                Hash: b1c3d4e5f67890aabbccddeeffg33445  
                Action: Detected

            -- Windows Event Log (Event ID 4688):

                EventID: 4688.

                New Process Name: C:\Windows\System32\encryptor.exe  
                Creator Process ID: 4050  
                Account Name: victim  
                Command Line: encryptor.exe -target "C:\Users\Victim\Documents"  

            -- Acciónes Recomendadas:

                1 - Utilizar VirusTotal para analizar el hash b1c3d4e5f67890aabbccddeeffg33445 y confirmar si está asociado con ransomware.

                2 - Aislar el sistema afectado para evitar la propagación del ransomware.
                3 - Analizar la fuente del archivo ejecutable (correo electrónico, descarga, etc.).
                4 - Restaurar los datos desde un respaldo, si está disponible.

    -- Escenario 2: Ataque de Golden Ticket en Kerberos:

        -- Descripción:

            Un atacante utiliza credenciales comprometidas para crear un Golden Ticket, otorgándose acceso persistente y completo al dominio.

        -- Logs Generados:

            -- Windows Security Log (Event ID 4769)

                EventID: 4769  
                Account Name: attacker$  
                Service Name: krbtgt  
                Ticket Options: 0x40810010  
                Client Address: 10.10.10.50  
                Failure Code: 0x0  


            -- Wazuh (Suspicious Kerberos Activity)

                Alert ID: 50002  
                Rule: Kerberos Ticket Anomaly Detected  
                Service Name: krbtgt  
                Ticket Duration: 10 years  
                Action: Detected

        -- Patrón Detectado.

            Ticket con duración anómala (10 años).
            Solicitud de Ticket-Granting Service (TGS) con privilegios elevados.


        -- Acciones Recomendadas

            Identificar si la cuenta attacker$ es legítima y revisar su actividad.
            Restablecer la clave del servicio krbtgt para invalidar el Golden Ticket.
            Revisar logs adicionales para determinar el origen de las credenciales comprometidas.
            Auditar accesos y permisos en el dominio para detectar otras actividades sospechosas.


    -- Escenario 3: Exploración de Red Detectada con Nmap:

        -- Descripción:

            Un atacante utiliza Nmap para explorar los puertos abiertos en un servidor corporativo. Los logs indican múltiples conexiones rápidas y sin éxito.


        -- Logs Generados:

            -- FortiGate (Firewall Log)

                date=2024-12-02 time=14:25:32 log_id=0100040000 type=traffic subtype=deny  
                src=203.0.113.20 src_port=53421 dst=192.168.1.50 dst_port=22  
                service=SSH action=deny msg="Port scan detected"


            -- Wazuh (Port Scanning Detection)

                Alert ID: 60001  
                Rule: Port Scanning Activity Detected  
                Source IP: 203.0.113.20  
                Scanned Ports: 22, 80, 443, 3389  
                Action: Detected

            -- Patrón Detectado

                Varias solicitudes desde la misma IP a diferentes puertos en un corto período.
                Uso típico de herramientas de exploración, como Nmap.

            -- Acciones Recomendadas

                Bloquear la IP 203.0.113.20 en el firewall.
                Revisar si otros sistemas han recibido tráfico desde la misma IP.
                Configurar reglas para limitar la velocidad de conexiones entrantes por IP.


## Actividad Práctica.

    -- Título: "Análisis y Respuesta a Incidentes Simulados"

        Instrucciones:

            1 - Selecciona uno de los escenarios simulados (ransomware, Golden Ticket, o exploración de red).

            2 - Analiza los logs proporcionados para identificar el evento sospechoso y correlacionar la información.

            3 - Utiliza herramientas como VirusTotal para verificar hashes o direcciones IP.

            4 - Documenta las acciones que tomarías para responder al incidente, incluyendo mitigaciones y recomendaciones futuras.

        -- Entrega esperada:

            -- Un informe breve que contenga:

                Descripción del incidente detectado.
                Evidencia de los eventos analizados.
                Acciones tomadas y razones detrás de ellas.


## Buenas Prácticas.

    1 - Configurar Alertas Clave: Monitorea eventos críticos como creación de procesos, actividad en puertos sensibles y accesos privilegiados.

    2 - Usar Herramientas de Enriquecimiento: Integra VirusTotal y Wazuh para mejorar la detección de amenazas.

    3 - Auditar Configuraciones Periódicamente: Asegúrate de que las reglas y políticas estén optimizadas.

    4 - Practicar en Entornos Controlados: Simula regularmente escenarios avanzados como ransomware y ataques Kerberos.


## Conclusión del Módulo.

    Este módulo ha proporcionado experiencias prácticas en la detección y respuesta a incidentes, usando ejemplos de ransomware, Golden Ticket y exploración de red. Estas simulaciones fortalecen la capacidad de los analistas para identificar patrones sospechosos y reaccionar con rapidez y precisión.