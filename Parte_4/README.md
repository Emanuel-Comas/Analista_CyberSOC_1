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

    -- Objetivo del Módulo:

        Aprender a aplicar técnicas avanzadas de análisis de logs para identificar actividades maliciosas como la ejecución de malware, ataques de ransomware y exfiltración de datos. Este módulo incluye ejemplos prácticos y un ejercicio de investigación al final.


## Por Qué es Crucial el Análisis de Logs?

    Los logs son la principal fuente de información para detectar actividades maliciosas. Eventos que parecen inofensivos individualmente pueden formar patrones sospechosos cuando se correlacionan. Analizar estos eventos permite identificar ataques en curso, anticipar amenazas y responder eficazmente.


## Técnicas de Análisis de Logs.

    -- Análisis Basado en Patrones:

        -- Identifica patrones específicos en los logs, como múltiples intentos de inicio de sesión fallidos en poco tiempo.

        -- Herramientas como Wazuh o Kibana permiten configurar reglas para reconocer estos comportamientos.

    -- Correlación de Eventos:

        -- Relaciona eventos de diferentes sistemas, como un intento fallido de inicio de sesión en Windows seguido de actividad anómala en el firewall.

        -- Los SIEM como Wazuh o Splunk automatizan este proceso.

    -- Detección de Anomalías:

        -- Busca comportamientos fuera de lo común, como un usuario accediendo al sistema en horarios inusuales.

        -- Herramientas como Elastic SIEM permiten visualizar picos de actividad y tendencias anómalas.


## Ejemplo 1: Ejecución de Malware Detectada.

    -- Contexto:

        Un usuario descarga un archivo adjunto de un correo electrónico que contiene malware. Los logs capturan su actividad sospechosa.

    -- Logs Generados.

        -- Windows Event Log (ID 4688):

            EventID: 4688  
            New Process Name: C:\Users\User\Temp\malicious.exe  
            Command Line: malicious.exe -install  
            Account Name: user  
            Source Network Address: 203.0.113.50  

        -- Wazuh (File Integrity Monitoring):

            Alert ID: 30001  
            Rule: Suspicious File Created  
            File: C:\Users\User\Temp\malicious.exe  
            Hash: a1b2c3d4e5f67890  

        -- Análisis:

            -- El archivo malicious.exe se detectó en una ubicación temporal, indicando una posible instalación maliciosa.

            -- Usar VirusTotal para analizar el hash del archivo confirma que corresponde a un malware conocido.  

        -- Acciones Recomendadas.

            -- Aislar el sistema afectado.

            -- Eliminar el archivo detectado y realizar un análisis completo del sistema.

            -- Revisar el origen del archivo (correo o URL) para identificar otros usuarios potencialmente afectados.

        
## Ejemplo 2: Ataque de Ransomware.

    -- Contexto:
    
        Un ransomware encripta archivos críticos en el sistema tras ejecutarse.

    -- Logs Generados: 

        -- Wazuh Alert (File Integrity Monitoring):

            Alert ID: 40002  
            Rule: Mass File Modification Detected  
            Directory: C:\Users\User\Documents  
            Files Modified: 50  
            Action: Detected 

        -- Windows Event Log (ID 4624):

            EventID: 4624  
            Account Name: user01  
            Logon Type: 2 (Interactive)  
            Source Network Address: 192.168.1.10  

        -- Windows Security Log (ID 4688):

            EventID: 4688  
            New Process Name: C:\Windows\System32\encryptor.exe  
            Command Line: encryptor.exe -target "C:\Users\User\Documents"  

    
    -- Análisis:

        -- El proceso encryptor.exe comenzó a modificar masivamente archivos en la carpeta Documents.

        -- El usuario user01 accedió al sistema antes de que se iniciara el proceso, posiblemente ejecutando el ransomware.

    -- Acciones Recomendadas:

        -- Desconectar el sistema afectado de la red para evitar propagación.

        -- Identificar el origen del ransomware (correo, descarga).

        -- Restaurar archivos desde respaldos si están disponibles.

    
## Ejemplo 3: Exfiltración de Datos.

    -- Contexto:

        -- Un atacante utiliza una herramienta para transferir datos sensibles a un servidor remoto.

    -- Logs Generados:

        -- Firewall FortiGate:

            date=2024-12-02 time=14:25:32 log_id=0100040000 type=traffic subtype=allow  
            src=192.168.1.100 src_port=50234 dst=198.51.100.200 dst_port=443  
            data_transferred=50MB msg="Large data upload detected"

        -- Windows Security Log (ID 4769):

            EventID: 4769  
            Service Name: fileserver01  
            Client Address: 192.168.1.100  
            Action: Access Granted  

    -- Análisis:

        -- La IP interna 192.168.1.100 transfirió 50 MB de datos a un servidor externo (198.51.100.200).

        -- El acceso al recurso compartido fileserver01 coincide con la transferencia detectada.

    --Acciones Recomendadas:

        -- Bloquear la IP 198.51.100.200 en el firewall.

        -- Auditar los archivos accesados desde fileserver01 para determinar la información comprometida.

        -- Revisar los permisos de la cuenta utilizada para evitar futuros accesos indebidos.


## Buenas Prácticas en el Análisis de Logs.

    -- Automatización con SIEM: Utiliza herramientas como Wazuh o Splunk para configurar reglas de detección automáticas.

    -- Correlación Multifuente: Integra logs de servidores, firewalls y endpoints para obtener un panorama completo.

    -- Priorizar Eventos Críticos: Configura alertas para actividades como creación de procesos, modificaciones masivas de archivos y transferencias de datos.

    -- Capacitación Continua: Mantente actualizado sobre técnicas de análisis y nuevas amenaza


## Actividad Práctica.

    -- Título: "Investigación de Actividad Sospechosa en Logs".

    -- Instrucciones:

        -- Revisa los siguientes logs simulados:

            -- Log 1 (Wazuh):

                Alert ID: 30003  
                Rule: Suspicious File Created  
                File: C:\Temp\encryptor.exe  
                Hash: b1c2d3e4f5g67890  

            -- Log 2 (Firewall):

                date=2024-12-02 time=15:10:22 log_id=0100040000 type=traffic subtype=allow  
                src=192.168.1.15 src_port=53421 dst=203.0.113.50 dst_port=443  
                data_transferred=100MB msg="Large file upload detected"

            
    -- Responde:

        ¿Qué actividad sospechosa detectas?
        ¿Cómo correlacionarías los eventos entre ambos logs?
        ¿Qué acciones tomarías para mitigar el posible incidente?


    -- Entrega esperada:

            -- Un breve informe que incluya:

                Descripción de la actividad maliciosa detectada.
                Correlación entre logs.
                Acciones de mitigación recomendadas.

    
## Conclusión del Módulo.

    El análisis de logs es una habilidad crítica para identificar actividades maliciosas. Este módulo ha explorado cómo detectar ejecuciones de malware, ataques de ransomware y exfiltración de datos mediante técnicas avanzadas y ejemplos prácticos. Con la práctica, los analistas pueden optimizar la detección y respuesta a amenazas en tiempo real.




# Ejercicios prácticos de análisis de logs con herramientas especializadas.

    -- Objetivo del Módulo
    
        Desarrollar habilidades prácticas en el análisis de logs utilizando herramientas especializadas como Wazuh, VirusTotal, y ANY.RUN. Los ejercicios estarán orientados a identificar patrones maliciosos, correlacionar eventos y responder a incidentes.


## Introducción al Análisis de Logs con Herramientas Especializadas.

    El uso de herramientas específicas en el análisis de logs permite automatizar tareas, identificar patrones más rápidamente y enriquecer los datos con inteligencia de amenazas. Esto es clave para mejorar la precisión y la rapidez en la respuesta a incidentes.

    -- Beneficios de Usar Herramientas Especializadas:

        1 - Automatización: Reducen el esfuerzo manual al correlacionar eventos automáticamente.

        2 - Detección avanzada: Identifican patrones complejos que podrían pasar desapercibidos en análisis manuales.

        3 - Enriquecimiento de datos: Proporcionan contexto adicional a eventos sospechosos, como reputación de IPs o hashes maliciosos.

    -- Herramientas que Utilizaremos:
        Wazuh: SIEM para correlación y generación de alertas.
        VirusTotal: Para análisis de archivos, hashes, IPs y URLs.
        ANY.RUN: Sandbox interactivo para evaluar comportamientos de archivos sospechosos.


## Ejercicios Prácticos.

    -- Ejercicio 1: Identificación de un Archivo Sospechoso.

        -- Escenario:

            El SIEM Wazuh genera una alerta indicando que un archivo desconocido fue creado en un endpoint. Se sospecha que puede ser un malware.

        -- Logs generados:

            Wazuh (File Integrity Monitoring)

                Alert ID: 60001  
                Rule: Suspicious File Detected  
                File: C:\Users\Public\invoice2024.exe  
                Hash: f7e2d7b0b8a8b0c3d5a8977f80c9ad55  

        -- Pasos del Análisis:

            Revisión del log en Wazuh:

                Confirma el origen del archivo y la cuenta asociada.

                Identifica el hash (f7e2d7b0b8a8b0c3d5a8977f80c9ad55) para buscarlo en VirusTotal.

            Investigación avanzada con ANY.RUN:

                Sube el archivo al sandbox.

                Observa el comportamiento del archivo, como conexiones a dominios externos, modificación de archivos o creación de procesos.


        Resultado Esperado:

            El archivo es identificado como malware por múltiples motores de VirusTotal y ANY.RUN revela que intenta conectarse a un servidor externo.


        Acciones Recomendadas:

            Aislar el endpoint afectado.

            Eliminar el archivo sospechoso.

            Revisar las conexiones realizadas desde el sistema afectado para identificar posibles exfiltraciones.


    -- Ejercicio 2: Correlación de Eventos para Detectar Escaneo de Red.

        -- Escenario:

            Un atacante utiliza una herramienta como Nmap para escanear puertos abiertos en una red corporativa. Los logs del firewall y del SIEM reflejan la actividad sospechosa.

        -- Logs Generados:

            Firewall FortiGate:

                date=2024-12-03 time=10:25:45 log_id=0100040000 type=traffic subtype=deny  
                src=203.0.113.45 src_port=45234 dst=192.168.1.100 dst_port=22  
                action=deny msg="Port scan detected"


            Wazuh (Suspicious Activity):

                Alert ID: 60002  
                Rule: Port Scanning Activity  
                Source IP: 203.0.113.45  
                Scanned Ports: 22, 80, 443, 3389  



        Pasos del Análisis:

            Revisión del log en FortiGate:

                Identifica la fuente del tráfico (203.0.113.45).

                Observa que se intentaron varias conexiones en puertos críticos (SSH, HTTPS, RDP).

            Correlación en Wazuh:

                Confirma que la misma IP está escaneando múltiples puertos en distintos dispositivos.

            Análisis en VirusTotal:

                Busca la IP en VirusTotal para verificar si está catalogada como maliciosa o parte de una botnet.


        -- Resultado Esperado:

            La IP 203.0.113.45 aparece en listas negras en VirusTotal, confirmando que está asociada con actividades maliciosas.


        Acciones Recomendadas:

            Bloquear la IP en el firewall para evitar accesos futuros.
            Revisar si otros sistemas han recibido tráfico desde la misma IP.
            Configurar alertas automáticas en el SIEM para detectar patrones similares en el futuro.


    -- Ejercicio 3: Detectando Exfiltración de Datos.

        -- Escenario:

            Un atacante utiliza una cuenta comprometida para transferir grandes volúmenes de datos a un servidor externo.

        -- Logs Generados:

            Wazuh (Unusual Activity Detected):

                Alert ID: 70003  
                Rule: Large Data Transfer  
                User: compromised_user  
                Destination: 198.51.100.50  
                Data Size: 500MB  

            Firewall FortiGate:

                date=2024-12-03 time=11:15:30 log_id=0200020000 type=traffic subtype=allow  
                src=192.168.1.10 src_port=50234 dst=198.51.100.50 dst_port=443  
                service=https data_transferred=500MB msg="Large file upload detected"

        Pasos del Análisis:

            Revisión del log en Wazuh:

                Identifica al usuario y el tamaño de la transferencia.

                Confirma que los datos fueron enviados a 198.51.100.50.

            Revisión en el firewall:

                Verifica el tráfico asociado a la IP de destino.

            Investigación en VirusTotal:

                Busca la IP del servidor externo en VirusTotal para determinar si está relacionada con actividades maliciosas.


        Resultado Esperado:

            El servidor 198.51.100.50 está identificado como parte de un esquema de exfiltración de datos.


        Acciones Recomendadas:

            Bloquear la IP en el firewall.
            Revocar las credenciales del usuario comprometido.
            Realizar una auditoría para identificar qué datos fueron exfiltrados.


## Actividad Práctica.

    -- Título: "Análisis Integral de un Incidente con Wazuh y VirusTotal"

    Instrucciones:

        Revisa los siguientes logs:

            Log 1 (Wazuh):

                Alert ID: 80001  
                Rule: Suspicious Process Detected  
                File: C:\Temp\suspicious.exe  
                Hash: b2c3d4e5f67890123456789abcdef123 

            Log 2 (FortiGate):

                date=2024-12-03 time=12:20:45 log_id=0100040000 type=traffic subtype=allow  
                src=192.168.1.15 src_port=54321 dst=203.0.113.75 dst_port=443  
                data_transferred=200MB msg="File upload detected"

        Analiza los eventos utilizando:

            Wazuh para correlacionar las actividades.
            VirusTotal para verificar el hash del archivo y la IP del servidor externo.

        Documenta tus hallazgos en un informe breve, incluyendo:

            Descripción del incidente detectado.
            Herramientas utilizadas y resultados.
            Acciones recomendadas para mitigar el riesgo.


## Conclusión del Módulo.

    Este módulo ha proporcionado ejercicios prácticos para analizar logs utilizando herramientas especializadas, permitiendo a los estudiantes aplicar técnicas avanzadas para detectar y responder a incidentes. Estas habilidades son esenciales para trabajar en entornos SOC modernos.