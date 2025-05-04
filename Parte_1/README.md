# Introducción


## Ciberseguridad y rol de analista CyberSOC.


-- Que es la ciberseguridad:

    es el conjunto de prácticas, tecnologias y procesos deiseñados para proteger sistemas, redes y 
    datos de accesos no autorizados, atques y daños.



-- Principales objetivos CID/CIA:

    Confidencialidad/Confidentiality: Garantizar que solo las personas autorizadas accedan a la información.

    Integridad/Integrity: Asegurar que los datos no sean alterados o manipulados sin autorización.

    Disponibilidad/Availability: Mantener lso sistemas y datos accesibles cuando se necesiten.


-- Tipos de amenazas comunes:

    Malware: Software malisioso que incluye virus, troyanos, ramsomware, etc.

    Phishing: Intentos de engaño para obtener información sensible mediante correos electrónicos falsos, 
    o páginas web fraudulentas.

    Ataques DDoS: Sobrecarga de sitemas mediante múltiples solicitudes para interrumpir sis funcionamientos.

    Exploits: Aprovechamiento de vulnerabilidades en sistemas o aplicaciones.





## Ecosistema de la Ciberseguridad.


    La ciberseguridad abarca varias disciplinas y roles, uno de ellos es el Analista CyberSOC, encargado de 
    monitorear, detectar y responder a incidentes de seguridad en tiempo real.


-- Centro de Operaciónes de Seguridad (SOC):

    Es el corazón de la ciberseguridad empresarial, es un centro especializado donde un equipo de expertos 
    monitoriea de forma continua los sistemas, analiza eventos sospechosos y responde a incidentes para 
    proteger la organización.



-- Rol del Analista CyberSOC:

    Los analistas en SOC son los 'detectives digitales' responsables de proteger la infraestructura tecnológica, este rol puede dividirse en 3 niveles, dependiendo de la experiencia y responsabilidades.

    Nivel 1 (L1): Primera linea de defensa, monitorea alertar generadas por herramientas de seguridad (SIEM), 
    escala incidentes sospechosos a niveles superiores.

    Nivel 2 (L2): Realiza análisis mas detallados de las amenazas detectadas, correlaciona eventos y busca 
    patrones en los datos para identificar ataques avanzados, coordina la respuesta a incidentes.

    Nivel 3 (L3): Investiga incidentes complejos y dirige esfuerzos en caza de amenazas (Threat Hunting), 
    desarrolla playbook y estrategias para mitigar futuras amenazas, realiza análisis forense digital y aporta 
    inteligencia accionable.



## Herramientas Esenciales para el Analista CyberSOC.

    SIEM (Security Information and Event Management): Herramientas que recopilan, analisan y correlacionan 
    datos de múltiples fuentes, (ejemplo: Wazuh, Splunk, Elastic).

    Firewalls y WAF (Web Application Firewall): Controlan y filtran tráfico de red para proteger contra 
    ataques externos.

    EDR (Endpoint Detection and Response): Monitorean dispositivos finales en busca  de comportamientos 
    sospechosos.

    Threat Intelligence: Plataformas como VirusTotal, QAlienVault y MISP (Malware Information Sharing 
    Platform): proporcionan información sobre amenazas conocidas.



## Retos del Analista CyberSOC.

    Ruidos de alertas: Gran volumen de falsos positivos que pueden dificultar la detección de amenazas reales.

    Amenazas avanzadas: Los atacantes utilizan técnicas sofisticadas para evadir las defensas tradicionales.

    Presión constante: Proteger sistemas  criticos requiere un monitoreo 24/7.


-- Habilidades clave del Analista:

    - Pensamiento critico y analitico.

    - Conocimiento técnico en redes, sistemas operativos y herramientas de seguridad.

    - Capacidad para trabajar bajo presión y tomar decisiones rapidas.



## Por qué es importante este rol?.

    Los Analistas CyberSOC son la primera linea de defensa en un mundo digital lleno de riesgos, sin ellos las 
    organizaciónes estarian indefensas ante ataques que podrian compromenter datos sensibles, interrumpir 
    operaciónes o causar pérdidas financieras significativas.



# Fundamentos de los incidentes de Ciberseguridad.


-- Qué es un incidente de Ciberseguridad?:

    Es cualquier evento que compromete la confidencialidad, integridad o disponibilidad de la información o 
    sistemas de la organización.


-- Tipos de incidentes de Ciberseguridad: