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

    Violaciones de datos(data breaches): Accesos no autorizados a información sensible.

    Ataques de ransomware: Secuestro de datos mediante cifrado a cambio de un rescate.

    Phishing: Robos de credenciales mediante engaño.

    Intrusiones en redes: Accesos no autorizados a infraestructura.


-- Factores que desencadenan incidentes:

    Errores humanos (Click en enlaces maliciosos, configuraciones incorrectas).

    Software desactualizado o con vulnerabilidades conocidas.

    Uso de contraseñas débiles o reutilizadas.

    Ataques dirigidos (APT, Amenazas Persistentes Avanzadas o Advanced Persistent Threat).



## Ciclo de vida de un incidente.

    -- Gestionar un incidente no se limita a contener el daño, es un proceso estructurado que incluye varias 
    etapas.


-- Identificación:

    Detectar el incidente mediante herramientas como SIEM, EDR o logs.

    Analizar eventos sospechosos y detectar su impacto.

-- Contención:

    Aislar sistemas comprometidos para evitar la propagación.

    Aplicar medidas temporales, como bloquear direcciopnes IP o desconectar dispositivos.

-- Erradicación:

    Eliminar la causa raiz del incidente (malware, accesos no autorizados, etc).

    Actualizar configuraciónes y aplicar parches.

-- Recuperación:

    Restaurar sistemas y datos afectados.

    Verificar la seguridad antes de reanudar las operaciónes normales.

-- Lecciones aprendidas:

    Analizar el incidente para prevenir eventos similares en el futuro.

    Documentar las acciones tomadas y realizar actualizaciónes en los procedimientos.



## Clasificación de un incidente.

    No todos los incidentes tienen el mismo nivel de gravedad, por ello es importante clasificarlos 
    según su impacto.

-- Baja prioridad:

    Falsos positivos o incidentes sin impacto tangible.

-- Media prioridad:

    Compromisos limitados que no afectan operaciónes criticas.

-- Alta prioridad:

    Ataques que comprometen datos sensibles o interrumpen operaciónes clave.



-- Ejemplo:

    Un intento de acceso fallido puede ser clasificado como de baja prioridad, pero si proviene de múltiples
    ubicaciones simultáneamente, podria escalar a alta prioridad (ataque de fuerza fruta).



## Indicadores de compromisos (IoCs, Indicators of Compromises).


    Son pistar que ayudan a detectar y responder a incidentes.


-- Estos incluyen:

    Archivos malisiosos: Por ejemplo, '.exe' sospechosos

    Direcciónes IP: Conexiones desde ubicaciónes conocidas por realizar ataques.

    Dominios sospechosos: Utilizados para phishing o C2 (comando y control).

    Registros anómalos: Accesos inusuales a horas no laborales o desde ubicaciónes inesperadas.



## Trabajo de investigación.

    Investigar un incidente de ciberseguridad y como fue gestionado.


-- Incidente:

    Ataque de ransomware a colonial Pipeline (2021).


-- Qué ocurrio?:

    Entre el jueves 6 de mayo y el viernes 7 de mayo de 2021, Colonial Pipeline (Empresa que transporta 
    gasolina, diésel y combustible para aviones desde Texas hasta lugares tan lejanos como New York), 
    sufrió un ataque de 'malware' que los obligó a cerrar su sistema, ya que detuvo todas las operaciónes 
    del oleoducto, Colonial Pipeline dijo que el ataque afectó a algunos  de sus sistemas de información.


-- Cuál fue la causa raiz?:

    No se establecieron las medidas de protección necesarias, a pesar de que se afirmo que los ataques 
    eran prevenibles segun los expertos.


-- Qué impacto tuvo?:

    Escasez de conbustible en el Aeropuerto Internacional de Charlotte-Douglas American, American Airlines 
    cambió temporalmente los horarios de vuelo, al menos 2 vuelos (a Honolulu y Londres) tenian paradas de 
    combustible o cambios de avión agregados a sus horarios durante un periodo de 4 dias, tambien requirió 
    que el Aeropuerto Internacional Hartsfield-Jackson de Atlanta utilizara otros proveedores de combustible.


-- Cómo fue gestionado?:

    El presidente de los Estados Unidos 'Joe biden', declaró estado de emergencia el 9 de mayo, la declaración 
    eliminó los limites al transporte por carretera, en un intento de paliar cualquier escasez del cierre del 
    Oleoducto.
    Colonial Pipeline declaró que planeaban reparar sustancialmente y restaurar las operaciónes del Oleoducto 
    para el fin de la semana.