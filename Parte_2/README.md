# Gestión de Alertas.


-- Entender como los sistemas SIEM (Security Information and Event Management) recopilan, correlacionan y 
generan alertas a partir de eventos de seguridad y aprender las mejores prácticas para gestionar estas alertas 
de manera eficiente.



## Qué es un SIEM y por qué es fundamental?.

    Es una solución clave en la ciberseguridad moderna, su propósito principal es recopilar y analizar eventos 
    de seguridad de múltiples fuentes en tiempo real, permitiendo a los analistas tener uan visión completa 
    de la postura de seguridad de la organización.


-- Funciones principales de un SIEM:

    Recopilación de datos: Obtiene logs y eventos de dispositivos, aplicaciónes y redes.

    Normalización: Estandariza los datos para facilitar su análisis.

    Correlación: Identifica patrones y relaciona eventos aparentemente aislados.

    Generación de alertas: Notifica actividades sospechosas o incidentes.

    Reportes y auditorias: Ofrece informes para cumplimiento y análisis post-incidente.


-- Ejemplos de sistemas SIEM populares:


    -> Splunk

    -> Wazuh

    -> Elastic SIEM

    -> IBM QRadar

    -> ArcSight


-- Importancia de un SIEM:

    Son esenciales para detectar amenazas avanzadas que podrian pasar desapercibidas en sistemas individuales 
    y permiten una respuesta rápida y centralizada.



## Qué son las alertas en un SIEM?.

    Una alerta en un SIEM es una notificación generada cuando un evento o conjunto de eventos cumple con 
    criterios predefinidos que indican una posible actividad sospechosa o maliciosa.


-- Fuentes de eventos comunes:

    Intentos de accesos fallidos.

    Conexiones a IPs maliciosas.

    Actividad anómalas en cuentas privilegiadas.

    Transferencias de datos no autorizados.


-- Ejemplo de un evento correlacionado:

    Un usuario inicia sesión desde una ubicación inusual.

    Minutos después, se detecta la transferencia de grandes volúmenes de datos a una IP externa.

    el SIEM correlaciona ambos eventos y genera una alerta critica de posible exfiltración de datos.



## Gestión de alertas (Priorización y Respuesta).


-- Clasificación de alertas:

    Para manejar eficientemente las alertas, es crucial clasificarlas según su nivel de criticidad.

    
    Baja: Actividad sospechosaque no representaun riesgo inmediato, ejemplo: Acceso fallido único.

    Media: Eventos con potencial de ser maliciosos, ejemplo: Varias conexiones fallidas desde una 
    misma IP.

    Alta: Amenazas confirmadas o de alto impacto, ejemplo: Malware detectado en un servidor critico.


-- Criterios de priorización:

    Impacto potencial: Qué tan critico es el sistema o dato afectado?.

    Probabilidad de ocurrencia: Cuán probable es que el evento sea malicioso?.

    Contexto del evento: Qué otros eventos están ocurriendo simultáneamente?.


-- Protocolo básico de respuesta.

    Confirmar la alerta: Revisar los datos para asegurarse de que no sea un falso positivo.

    Aislar la amenaza:  Bloquear accesos, detener procesos o desconectar dispositivos afectados.

    Investigar:  Analizar el origen y causa raiz.

    Responder: Tomar medidas correlativas y prevenir incidentes futuros.



## Falsos positivos (Un desafio comun).

    Uno de los mayores desafios en la gestion de alertas es lidiar con 'falsos positivos', que pueden 
    generar ruido y consumir recursos innecesariamente.


-- Causas comunes de falsos positivos:

    Configuración incorrecta de reglas en el SIEM.

    Comportamientos legitimos interpretados como anómalos.

    Herramientas o dispositivos que generan eventos redundantes.


-- Cómo reducir falsos positivos:

    Ajustar y optimizar las reglas del SIEM.

    Implementar listas blancas para excluir eventos legitimos.

    Capacitar a los analistas en el uso efectivo del SIEM.



## Actividad práctica (Análisis de alertas).

-- Objetivo: 

    Desarrollar habilidades para clasificar y priorizar alertas reales en un entorno simulado.



-- Instrucciones:

-- Leer los siguientes eventos generados por un SIEM:

    1: Un intento de acceso fallido desde una IP desconocida.

    2: Tres intentos fallidos de inicio de sesion en una cuenta privilegiada desde ubicaciones diferentes.    

    3: Transferencia de 2GB de datos a una IP externa clasificada como maliciosa.

    4: Inicio de sesion en un servidor critico fuera del horario laboral.


-- Clasificar cada evento en 'baja', 'media' o 'alta prioridad':

    1: Baja prioridad.

    2: Media prioridad.

    3: Alta prioridad.

    4: Media prioridad.

-- Responde:

    Qué evento priorizarias primero?.

        3: Transferencia de 2GB de datos a una IP externa clasificada como maliciosa (Alta prioridad).

    Qué medidas tomarias para investigar y responder a este evento?.

        Horario de inicio de sesion, IP de inicio de sesion, cuenta donde se inicio sesion y aislamiento de la cuenta 'posiblemente infectada', Horario de transferencia de datos, que datos se trasfirieron y a que 
        IP, rastreo de IP.



-- Realiza un informe breve de tus decisiones.

    Evento prioritario:

        Se priorizó la 'Transferencia de 2GB' de datos a una IP externa clasificada como maliciona, 
        dado que representa una posible exfiltración de información y constituye una amenaza de 'Alta 
        prioridad' para la seguridad de la organización.


    Medidas tomadas para la investigación y respuesta:

        1 - Revisión de registros de inicio de sesión:

            Se analizó el 'horario de inicio de sesión', la 'IP de origen', y la 'cuenta involucada' 
            para identificar el punto de acceso inicial del posible atacante.

        2 - Aislamiento de la cuenta comprometida:

            Se procedió al 'aislamiento inmediato de la cuenta posiblemente infectada' para detener 
            cualquier actividad maliciosa en curso y evitar una mayor filtración de datos.

        3 - Análisis de la transferencia:

            Se revisaron los 'logs de transferencia', incluyendo 'la hora exacta', el 'volumen de datos', 
            el 'contenido transferido' y 'la IP de destino' para determinar la naturaleza y alcanece de 
            la fuga.

        4 - Rastreo y análisis de la IP externa:

            Se realizó un 'rastreo de la IP maliciosa' para identificar su geolocalización, histórico de 
            amenazas asociadas y posibles relaciones con actores conocidos.



## Conclusión.

    La gestión de alertas en sistemas SIEM es un componente critico para la seguridad de cualquier 
    organización, al aprender a priorizar, investigar y responder a alertas de manera efectiva, los 
    analistas CyberSOC pueden mejorar significativamente la capacidad de respuestas frente a 
    amenazas.





# Identificación y priorización de alertas.