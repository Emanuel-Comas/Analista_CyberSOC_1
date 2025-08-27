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

        -- Analiza lso logs proporcionados para Windows y FortiGate.
        -- Define reglas de correlación para detectar:
            -- Más de 3 intentos fallidos de inicio de sesión desde la misma IP en 5 minutos.
            -- Tráfico recurrente a puertos bloqueados, por ejemplo, RDP, SSH.
        -- Escribe un breve informe que incluya:
            -- Descripción de los eventos clave que estás monitoreando.
            -- Reglas configuradas y razones detrás de ellas.
            -- Acciones recomendadas para mitigar las amenazas detectadas.


## Conclusión del módulo.

    La monitorización en tiempo real es una herramienta poderosa para detectar amenazas y responder, 
    de manera proactiva, con eejmplos prácticos de logs y reglas de correlación, este modulo ha preparado 
    a los estudiantes para implementar configuraciónes efectivas en entornos SOC.