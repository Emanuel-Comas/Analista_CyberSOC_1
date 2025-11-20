# Importancia y Tipos de Logs en Ciberseguridad

    Comprender la relevancia de los logs en la ciberseguridad, cómo contribuyen a la detección y mitigación de amenazas, y familiarizarse con los tipos más comunes de logs generados en diferentes sistemas y dispositivos.

## Qué Son los Logs y por Qué Son Importantes?.

    Los logs son registros generados por sistemas, aplicaciones y dispositivos que documentan eventos o actividades ocurridas en un entorno tecnológico. Estos registros son fundamentales para la ciberseguridad, ya que proporcionan evidencia detallada sobre el comportamiento del sistema y los usuarios.

    -- Funciones Principales de los Logs en Ciberseguridad:

        1 - Detección de amenazas: Identifican actividades sospechosas, como intentos de acceso no autorizado o ejecución de malware.

        2 - Análisis forense: Permiten rastrear incidentes para determinar su origen y alcance.

        3 - Cumplimiento normativo: Ayudan a demostrar conformidad con regulaciones como GDPR, PCI DSS o ISO 27001.

        4 - Monitoreo continuo: Facilitan la supervisión en tiempo real para responder rápidamente a incidentes.


    -- Características Clave de los Logs:

        -- Fecha y hora (timestamp): Identifica el momento exacto del evento.

        -- Fuente y destino: Indica quién inició y dónde ocurrió la actividad.

        -- Tipo de evento: Especifica la naturaleza del evento (inicio de sesión, fallo, ejecución de proceso).

    
## Tipos Comunes de Logs en Ciberseguridad.

    1 - Logs de Seguridad:

        Generados por sistemas operativos, aplicaciones y dispositivos para registrar eventos relacionados con la seguridad.

        -- Ejemplos:

            -- Windows Security Logs:

                Event ID 4625: Intento fallido de inicio de sesión.
                Event ID 4688: Creación de un proceso.
                Event ID 4769: Solicitud de ticket Kerberos.

            -- Linux Audit Logs:

                type=SYSCALL msg=audit(1625769341.123): syscall=execve success=yes  

                -- Indica si un comando crítico fue ejecutado con éxito.


    2 -  Logs de Firewall:

        Registran el tráfico de red permitido y bloqueado, además de intentos de conexión sospechosos.

        -- Ejemplo de Log de FortiGate:

            date=2024-12-02 time=14:15:30 log_id=0100040000 type=traffic subtype=deny  
            src=203.0.113.12 src_port=53245 dst=192.168.1.10 dst_port=3389  
            service=RDP action=deny msg="Blocked by policy 101"

            -- Importancia: Ayudan a detectar exploración de puertos, intentos de fuerza bruta y exfiltración de datos.

    3 - Logs de SIEM (e.g., Wazuh):

        -- Un SIEM recopila, normaliza y correlaciona logs de diversas fuentes para generar alertas.

        -- Ejemplo en Wazuh:

            Alert ID: 20002  
            Rule: Suspicious Login Attempt  
            Source: Windows Server  
            User: admin  
            Result: Failed  

            -- Importancia: Proporcionan visibilidad centralizada y priorizan eventos críticos.

    4 - Logs de Aplicaciones.

        Registran eventos relacionados con aplicaciones específicas, como errores, accesos y uso de recursos.

        -- Ejemplo:

            [2024-12-02 14:20:45] Error: Authentication failed for user 'john.doe'  

            -- Importancia: Identifican vulnerabilidades específicas de aplicaciones, como inyecciones SQL o fallos de autenticación.

    5 - Logs de Endpoint Detection and Response (EDR):

        Monitorean dispositivos finales (endpoints) para detectar comportamientos sospechosos.

        -- Ejemplo: 

            Event: File Modification  
            File: C:\Users\Public\malware.exe  
            Action: Quarantined  

            -- Importancia: Detectan malware, cambios no autorizados en archivos y conexiones a dominios maliciosos.


## Cómo Interpretar y Correlacionar Logs.

    -- Componentes Clave en un Log:

        1 - Timestamp: Fecha y hora del evento.
        2 - Fuente: Sistema, dispositivo o aplicación que generó el evento.
        3 - Mensaje del evento: Descripción detallada de lo ocurrido.
        4 - Prioridad o severidad: Nivel de criticidad del evento.

    -- Ejemplo de Correlación:

        Caso: Un atacante intenta realizar una conexión remota (RDP) seguida de intentos fallidos de inicio de sesión.

        -- Log del Firewall (FortiGate):

            date=2024-12-02 time=14:05:30 log_id=0100040000 type=traffic subtype=deny  
            src=203.0.113.20 dst=192.168.1.15 dst_port=3389 action=deny  

        -- Log de Windows Security (ID 4625):

            yaml
            Copiar código
            EventID: 4625  
            Account Name: administrator  
            Source Network Address: 203.0.113.20  
            Failure Reason: Unknown user name or bad password  

            -- Correlación:

                La misma IP (203.0.113.20) aparece en ambos logs, indicando un intento fallido de fuerza bruta hacia RDP.

## Retos en el Manejo de Logs.

    1 - Gran Volumen de Datos.

        Los entornos modernos generan miles de eventos por segundo, dificultando la detección de incidentes relevantes.

        Solución:

            Utilizar herramientas SIEM para filtrar y correlacionar eventos importantes.

    2 - Falsos Positivos.

        Muchos eventos pueden parecer sospechosos pero son legítimos.

        Solución:

            Ajustar reglas y políticas para reducir ruido.

    3 - Conservación y Gestión de Logs:

        Los logs deben almacenarse durante períodos prolongados para auditorías o análisis forense.

        Solución:

            Definir políticas de retención y utilizar soluciones escalables para almacenamiento.


## Buenas Prácticas en el Uso de Logs.

    1 - Centralizar Logs: Usa un SIEM para recopilar y analizar logs desde una única plataforma.

    2 - Establecer Reglas de Correlación: Configura alertas basadas en patrones de amenazas.

    3 - Auditar Regularmente: Revisa los logs para detectar configuraciones incorrectas o actividad anómala.

    4 -Cumplir Regulaciones: Asegúrate de que los logs cumplen con los requisitos legales y normativos aplicables.

    5 - Capacitar al Equipo: Proporciona formación a los analistas para interpretar y priorizar eventos correctamente.


## Actividad Práctica.

    Título: "Interpretación y Análisis de Logs en Ciberseguridad"

    Instrucciones:

        1 - Analiza los siguientes logs simulados:

            Log 1 (Firewall):

                date=2024-12-02 time=14:15:30 log_id=0100040000 type=traffic subtype=deny  
                src=203.0.113.50 src_port=52345 dst=192.168.1.100 dst_port=22  
                action=deny msg="Blocked by policy 102"

            Log 2 (Windows):

                EventID: 4625  
                Account Name: admin  
                Source Network Address: 203.0.113.50  
                Failure Reason: Unknown user name or bad password  

            1 - Responde:

                ¿Qué evento está ocurriendo?
                ¿Qué patrones sospechosos detectas?
                ¿Qué acciones tomarías para mitigar el posible incidente?

                -- Entrega esperada.

                    -- Un breve informe que incluya:

                        Descripción del evento.
                        Correlación de logs.
                        Acciones propuestas.

        
## Conclusión del Módulo.

    Los logs son una herramienta esencial en la ciberseguridad, proporcionando datos críticos para la detección de amenazas y análisis forense. Dominar su interpretación y uso en un entorno SOC es clave para cualquier analista de seguridad.




# Técnicas de Análisis de Logs para Identificar Actividades Maliciosas.