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

    Aprender a identificar, categorizar y priorizar las alertas generadas por sistemas SIEM, optimizando 
    la capacidad de respuesta frente a incidentes de seguridad.



## Qué es la identificación de alertas?.

    La identificación de alertas de reconocer eventos de seguridad relevantes generados por el SIEM y 
    diferenciarlos de aquellos que no representan riesgos reales, esto implica analizar patrones, 
    correlaciones y datos contextuales para determinar si una alerta debe ser investigada.


-- Pasos para la identificación de alertas:

    Revisión inicial de alertas: Examinar los eventos generados por el SIEM.

    Análisis de contexto: Evaluar el origen, destino, hora y tipo de evento.

    Validación preliminar: Confirmar si la alerta corresponde a un comportamiento anomalo o 
    malicioso.


-- Ejemplo de validación exitosa: 

    Alerta: Inicio de sesión desde una ubicación geográfica inusual.

    Análisis: Verificar si el usuario esta viajando o si las credenciales fueron comprometidas.

    Resultado: Decidir si se escala la alerta o se descarta como un evento legitimo.



## La importancia de la priorización de alertas.

    No todas als alertas tienen el mismo nivel de urgencias, sin una priorización adecauada, el equipo 
    de seguridad podria perder tiempo en falsos positivos o eventos irrelevantes, descuidando 
    amenazas criticas.


-- Factores para priorizar alertas:

    Impacto en la organización: Qué tan critico es el sistema o dato afectado?.

    Probabilidad de amenazas: Basadas en comportameinto anómalo, patrones conocidos o inteligencia 
    de amenazas.

    Contexto: Correlacion con otros eventos relevantes.


-- Clasificación de prioridades:

    Baja: Eventos que no presentan riesgos inmediatos, por ejemplo, intentos de escaneo de puertos.

    Media: Eventos que podrian escalar en amenazas, por ejemplo, actividad sospechosa de cuentas privilegiadas.

    Alta: Amenazas confirmadas o con impacto critico, por ejemplo, malware detectado en un servidor.



## Metodologías para la priorización de alertas.



-- Análisis basado de impacto y probabilidad:

    Este metodo evalúa 2 factores:

        Impacto potencial: Qué tan grave seria el daño si la amenaza se materializa.

        Probabilidad de ocurrencia: Basada en patrones historicos y comportamientos.


-- Uso de inteligencia de amenazas:

    Integrar feeds de inteligencia de amenazas para enriquecer las alertas, por ejemplo, una alerta 
    vinculada a una IP marcada como maliciosa tiene mayor prioridad.


-- Score de alertas (Sistema Automático):

    Algunos SIEM asignan automáticamente un puntaje a las alertas basado en criterios predefinidos, por 
    ejemplo, Wazuh con reglas OSSEC (Open Souce Security Event Correlator).


## Actividad práctica (Priorización de alertas.)


-- Objetivo:

    Aprender a clasificar y priorizar alertas en un entorno simulado.


-- Escenario simulado:

    El SIEM ha generado las siguientes alertas, clasificadas en baja, media o alta prioridad, y define 
    el protocolo de respuesta.

    Alerta 1: Intentos de inicio de sesion fallidos desde una misma IP durante 2 minutos.

    Alerta 2: Transferencia de datos a una dirección IP clasificada como maliciosa.

    Alerta 3: Instalación de un programa no autorizado en un endpoint.

    Alerta 4: Inicio de sesion de un servidor critico desde una ubicacion no habitual.


-- Instrucciones para la actividad:

    1: Evalúa cada alerta con base en su impacto y probabilidad

    2: Clasifica la alerta según la prioridad (baja, merdia, alta).

    3: Escribe un protocolo de respuesta para la alerta mas critica.


-- Entrega esperada:

    -- Un informe breve que detalle:

        1: Clasificación de cada alerta.

        2: Razón detras de la clasificación.

        3: Respuesta inmediata sugerida sugerida para alerta de mayor prioridad.


-- Entrega completa:

    Alerta 1:
        Impacto y probabilidad 'baja/alta' (depende a que cuenta intente acceder la IP).
        Prioridad 'baja'.
        Protocolo de respuesta: Rastreo/geolocalización de IP, verificación/rastreo de cuenta a la cual se intenta iniciar sesion.

    Alerta 2:
         Impacto y probabilidad: 'Alta'.
         Prioridad: Alta.
         Protocolo de respuesta: Aislar el servidor comprometido, verificación de los datos transferidos (con 
         fecha y hora del suceso), rastrear/geolocalizar IP y los implicados en el servidor comprometido.

    Alerta 3:
        Impacto y probabilidad: 'medio/alta' (depende el software instalado).
        Prioridad: 'Media'
        Protocolo de respuesta: Verificación del programa/software instalado y su alcance.

    Alerta 4: 
        Impacto y probabilidad: 'medio/alta' (depende si hay conocimiento previo de dicho inicio de sesion, 
        es decir, si se a avisado que tal inicio de sesion ocurriria).
        Prioridad: 'Media/alta'
        Protocolo de respuesta: Rastreo y verificación de la IP, verificación del servidor critico (Si hubo 
        algun movimiento sospechoso como transferencias de datos), aislamiento del servidor (de ser necesario), Fecha y hora del inicio de sesion.



## Falsos positivos y como gestionarlos.

    Los falsos positivos son alertas que, tras investigarse, se determinan inofensivas, estos pueden 
    consumir recursos y distraer a los análisis.


-- Ejemplo de falso positivo:

    Alerta: Inicio de sesion desde una ubicación inusual.

    Investigación: Se verifica que el usuario estaba de viaje.

    Resultado: Se clasifica como un evento legitimo.


-- Cómo reducir falsos positivos:

    Ajustar reglas SIEM para evitar sensibilidad excesivas.

    Implementar listas blacnas para eventos recurrentes y conocidos.

    Capacitar a los analistas para interpretar alertas de forma eficiente.


-- Tarea:

    Diseñar un protocolo de priorización de alertas:

        Investigar cómo diferentes organizaciones priorizan alertas en sus SIEM.

        Diseña un flujo de trabajo que detalle cómo clasificar y priorizar alertas, incuyendo 
        roles y resposabilidades.


-- Formato de entrega breve que explique:

    Los criterios que utilizaste para priorizar las alertas.

    El flujo de trabajo sugerido para gestionarlas.



-- Entrega de tarea (Investigación):

    Cada organización configura sus alertas según sus necesidades, utilizando reglas predefinidas, aprendizaje 
    automático y análisis contextual para identificar patrones anómalos, ademas los 'SIEM' pueden integrarse 
    con otras herramientas de seguridad para mejorar la respuesta a incidentes.

    -- Flujo de trabajo:

        1: Recepción de alertas : El 'SIEM' detecta una actividad sospechosa.
        2: Filtrado básico: Se descartan alertas irrelevantes (Analista SOC 1).
        3: Clasificación: Se analiza la amenaza y se asigna categoria (Analista SOC 2).
        4: Priorización: Se evalúa el nivel de riesgo y urgencia (Especialista en Ciberseguridad).
        5: Respuesta y escalamiento: Si es grave, se activa acción inmediata (CSIRT, Computer Segurity 
        Incident Response Team).
        6: Cierre y mejora: Se documenta el incidente y se ajustan reglas (Gestion de riesgos).

        -- De esta forma, este proceso asegura eficiencia y rapidez.


## Conclusión.

    La correcta identifiación y priorización de alertas es fundamental para una gestión eficiente de 
    la seguridad en un SOCm has aprendido a diferenciar alertas según su importancia y a priorizar recursos 
    para responder de manera efectiva a las amenazas mas criticas.