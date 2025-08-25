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
        