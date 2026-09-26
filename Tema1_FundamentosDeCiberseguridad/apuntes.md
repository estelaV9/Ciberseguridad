# Tema 1 - Fundamentos de Ciberseguridad

## 1. Conceptos básicos
Hay **4 conceptos clave** que hay que dominar desde el principio, porque todo el módulo gira en torno a ellos:

| Concepto | Definición |
|---|---|
| **Amenaza** | Cualquier hecho, deliberado o no, que puede causar daño a la información o a los sistemas |
| **Vulnerabilidad** | Debilidad del sistema que permite que una amenaza cause daño |
| **Riesgo** | Probabilidad de que una amenaza aproveche una vulnerabilidad, multiplicada por el impacto que tendría |
| **Impacto** | Consecuencia real (daño) si el incidente llega a ocurrir |

<br>

> **Idea clave:** sobre la amenaza no puedes hacer nada, no depende de ti (un atacante va a existir). Sobre la **vulnerabilidad sí puedes actuar** - ahí es donde se trabaja en seguridad (parcheando, formando, configurando bien, etc.)

### Ejercicio
**Caso:** una empresa encargada del mantenimiento de páginas en WordPress instala un plugin sin comprobar previamente su procedencia, reputación ni versión

| Elemento | Análisis |
|---|---|
| **Vulnerabilidad** | Instalación de un plugin desactualizado, sin verificar su procedencia ni la seguridad de su versión |
| **Amenaza** | Un atacante que aproveche un fallo del plugin para acceder o modificar la web, o que el propio plugin contenga código malicioso desde el origen |
| **Riesgo** | Posibilidad de que el plugin permita la entrada de malware o facilite un acceso no autorizado, comprometiendo los archivos y la información de la página |
| **Impacto** | - Hackeo de la web <br> - Daño a la imagen de la empresa ante el cliente <br> - Pérdida de confianza y posible pérdida del cliente <br> - Pérdida de posicionamiento SEO <br> - Pérdida de tiempo y recursos para detectar y eliminar el malware |

<br>

### 1.2. La tríada CID: ¿qué protegemos?
Toda medida de seguridad sirve, en el fondo, a uno de estos tres objetivos:
- **Confidencialidad** → garantiza que a la información solo acceda quien está autorizado
- **Integridad** → garantiza que la información no se altere sin autorización
- **Disponibilidad** → garantiza que la información esté accesible cuando se necesita

<br>

### 1.3. Amenazas activas y pasivas
Según cómo actúan, las amenazas se clasifican en dos grandes grupos:

| Tipo | Qué hace | Ejemplo | Rompe principalmente |
|---|---|---|---|
| **Amenaza pasiva** | Observa la información sin alterarla; intenta pasar desapercibida | Interceptar tráfico de red para leer contraseñas (sniffing) | **Confidencialidad** |
| **Amenaza activa** | Modifica, destruye o interrumpe la información o los sistemas | Cifrar ficheros con ransomware, borrar una base de datos | **Integridad y disponibilidad** - porque se modifican o borran datos y se impide el acceso a ellos |

<br>

> La amenaza pasiva es más difícil de detectar y se combate principalmente con **cifrado**. La amenaza activa es más "aparatosa" y se combate con **detección y recuperación**

<br>

## 2. Programas maliciosos (malware)
**Malware** = software malicioso. Cualquier programa diseñado para dañar un sistema, robar información, extorsionar al usuario o usar sus recursos sin permiso

### 2.1 Familias principales
| Familia | Cómo funciona | Ejemplo real |
|---|---|---|
| **Virus** | Se pega a un fichero legítimo y se ejecuta cuando alguien lo abre. Necesita acción humana para propagarse | Macro maliciosa en un documento de Office |
| **Gusano (worm)** | Similar al virus, pero se propaga solo por la red, sin necesidad de que un humano lo ejecute ni de "engancharse" a otro archivo | WannaCry, propagado explotando una vulnerabilidad de Windows |
| **Troyano** | Se oculta como software legítimo para engañar al usuario y que lo ejecute. No se replica solo | Un "crack" de un programa descargado que en realidad instala malware |
| **Ransomware** | Bloquea el acceso al sistema o a los datos (normalmente cifrándolos) hasta que se paga un rescate | WannaCry, LockBit |
| **Spyware** | Se oculta en el dispositivo y roba información confidencial (contraseñas, datos bancarios, actividad) sin que el usuario lo note | Puede venir empaquetado con software legítimo o dentro de un troyano |
| **Adware** | Muestra publicidad no deseada (a veces maliciosa), redirige búsquedas y recopila datos del usuario para venderlos a anunciantes | Barras de herramientas o extensiones que "bombardean" con anuncios |
| **Keylogger** | Tipo de spyware que registra todo lo que el usuario teclea (contraseñas, conversaciones, tarjetas...) | Captura de credenciales bancarias al escribirlas |
| **Botnet** | Red de dispositivos infectados ("bots" o "zombis") controlados remotamente para lanzar ataques masivos o enviar spam | Ataques DDoS masivos usando miles de dispositivos IoT infectados |
| **Rootkit** | Se oculta en lo más profundo del sistema operativo para esconder procesos/archivos maliciosos y evitar ser detectado por antivirus | Rootkits que modifican el propio kernel del sistema |
| **Bomba lógica** | Código malicioso que permanece inactivo hasta que se cumple una condición concreta (una fecha, una acción del usuario...) | Un empleado despedido deja código que borra archivos si su usuario se desactiva |
| **RAT (Remote Access Trojan)** | Troyano que da al atacante control remoto total del equipo infectado (como un TeamViewer malicioso) | Control de cámara, micrófono y archivos sin consentimiento |
| **Wiper** | Su único objetivo es destruir o borrar datos de forma irreversible, sin buscar rescate ni beneficio económico | Usado en ataques con motivación política o de sabotaje |
| **Cryptojacker** | Usa los recursos (CPU/GPU) del equipo infectado para minar criptomonedas sin permiso del usuario | Scripts de minado ocultos en páginas web comprometidas |
| **Fileless malware** | Malware que no se instala como archivo en disco; vive en la memoria RAM o abusa de herramientas legítimas del sistema (PowerShell, etc.), lo que dificulta su detección | Ataques que usan PowerShell para ejecutar código malicioso directamente en memoria |

<br>
  
### 2.2 Ransomware
- **Ransomware:** malware diseñado para bloquear el acceso de la víctima a su sistema o a sus datos (normalmente cifrándolos) hasta que se paga un rescate, habitualmente en criptomoneda
- **Características típicas:**
  - Cifra archivos con algoritmos fuertes (difíciles o imposibles de romper sin la clave)
  - Suele incluir una nota de rescate con instrucciones de pago y un plazo límite
  - Cada vez más combina la extorsión "clásica" con la **doble extorsión**: además de cifrar, roban los datos y amenazan con publicarlos si no se paga
  - Se propaga habitualmente por phishing, RDP mal protegido o explotando vulnerabilidades sin parchear
  - Pagar el rescate **no garantiza** recuperar los datos ni evita que se filtren igualmente

<br>

## 3. Ingeniería social, ataques a la red y a apps web
### 3.1 Ingeniería social: los fraudes más habituales
**Ingeniería social:** conjunto de técnicas de manipulación psicológica usadas para engañar a una persona y conseguir que revele información confidencial, realice una acción insegura o dé acceso a sistemas, explotando la confianza, el miedo o la urgencia en lugar de una vulnerabilidad técnica

| Fraude | Cómo funciona | Señal que lo delata |
|---|---|---|
| **Phishing** | Correo fraudulento que suplanta a una entidad de confianza (banco, empresa, servicio online) para robar credenciales o datos | Remitente sospechoso, faltas de ortografía, enlaces que no coinciden con el dominio oficial, tono de urgencia |
| **Spear phishing** | Igual que el phishing, pero dirigido y personalizado a una persona u organización concreta, usando información real sobre la víctima | Mensaje muy personalizado y creíble, pero pide algo inusual (datos, acceso, pago) |
| **Whaling** | Spear phishing dirigido específicamente a altos cargos ("peces gordos": directivos, CEO, CFO...) | Suplantación de un ejecutivo o dirigido a uno, con peticiones de alto impacto económico o estratégico |
| **Smishing** | Engaño por SMS. Muy usado para simular avisos de paquetería y bancos | SMS con enlace acortado que apunta a un dominio raro |
| **Vishing** | Engaño por llamada telefónica. Se hacen pasar por soporte técnico, banco o policía | Nadie legítimo pide credenciales ni códigos de verificación por teléfono |
| **Quishing** | Engaño mediante códigos QR fraudulentos | El QR lleva a un dominio que no es el del negocio real |
| **Fraude del jefe (CEO fraud / BEC)** | Correo aparentemente del director pidiendo una transferencia urgente y confidencial | Combinación de urgencia + secretismo + petición de saltarse el procedimiento habitual |
| **Cambio de IBAN** | Se intercepta la factura de un proveedor real y se cambia el número de cuenta antes de que llegue al cliente | El cambio de cuenta se comunica solo por correo, sin verificación telefónica o por otro canal |
| **Falso soporte técnico** | Llaman diciendo que tu equipo está infectado y piden acceso remoto para "solucionarlo" | Nadie te llama de oficio porque tu ordenador tenga un virus |
| **Baiting** | Se deja un pendrive infectado en el aparcamiento u otra zona con la esperanza de que alguien lo conecte por curiosidad | Aparecen pendrives sin dueño en zonas comunes de la empresa |

<br>

### 3.2 Ataques a la red
| Ataque | Qué hace |
|---|---|
| **Sniffing** | Captura e inspecciona el tráfico que circula por una red para robar información (contraseñas, datos) sin alterarlo. Es una amenaza pasiva |
| **Man-in-the-Middle (MitM)** | El atacante se sitúa entre dos partes que se comunican, interceptando y/o modificando la información sin que ninguna de las dos lo note |
| **Spoofing (IP/ARP/DNS)** | El atacante suplanta la identidad de un dispositivo, dirección o dominio para engañar a la red o a la víctima (ej. ARP spoofing para redirigir tráfico, DNS spoofing para llevar a webs falsas) |
| **Denegación de servicio (DoS)** | Satura un sistema o servicio con peticiones para dejarlo inaccesible a usuarios legítimos |
| **Denegación de servicio distribuida (DDoS)** | Igual que el DoS, pero lanzado desde muchos equipos a la vez (normalmente una botnet), lo que lo hace mucho más potente y difícil de bloquear |
| **Escaneo de puertos (port scanning)** | El atacante analiza qué puertos y servicios están abiertos en un sistema para identificar posibles puntos de entrada |
| **Ataque de fuerza bruta** | Se prueban de forma automática y masiva combinaciones de usuario/contraseña hasta dar con la correcta |

<br>

### 3.3 Ataques a aplicaciones web
| Ataque | Qué hace |
|---|---|
| **Inyección SQL (SQLi)** | Se introduce código SQL malicioso en un campo de entrada (formulario, buscador...) para manipular la base de datos: leer, modificar o borrar datos sin autorización |
| **Cross-Site Scripting (XSS)** | Se inyecta código (normalmente JavaScript) en una web que luego se ejecuta en el navegador de otros usuarios, permitiendo robar sesiones o cookies |
| **Cross-Site Request Forgery (CSRF)** | Engaña al navegador de una víctima autenticada para que realice, sin saberlo, una acción no deseada en una web donde tiene sesión iniciada |
| **Control de acceso roto** | Cambiando un identificador en la URL se accede a datos de otro usuario, porque no se verifica en el servidor a quién pertenece el recurso solicitado |
| **Inyección de comandos** | La aplicación ejecuta comandos del sistema con datos del usuario sin validar, por ejemplo formularios que acaban en `system()` o `exec()` |
| **Fallos criptográficos** | Datos sensibles guardados sin cifrar, algoritmos obsoletos o claves en el repositorio, por ejemplo guardar contraseñas con SHA-256 en lugar de bcrypt/Argon2 |
 
La lista completa de los diez riesgos más extendidos en aplicaciones web la publica y mantiene OWASP (Open Worldwide Application Security Project), en el conocido OWASP Top 10, referencia obligada para cualquiera que desarrolle una aplicación web

<br>

### 3.4 Categorías de ataques según su procedencia y su objetivo
Un mismo ataque técnico puede tener perfiles muy distintos según de dónde venga y a quién vaya dirigido
 
| Categoría | Definición | Ejemplo |
|---|---|---|
| **Interno** | El atacante está dentro de la organización: empleado, becario, exempleado con acceso vigente | Empleado descontento que copia una base de datos antes de irse |
| **Externo** | El atacante viene de fuera, sin credenciales legítimas de partida | Ataque de fuerza bruta a un servidor SSH expuesto a Internet |
| **Dirigido** | Se elige específicamente a la víctima y se prepara la campaña contra ella | Ataque a un ayuntamiento concreto tras un cambio político conflictivo |
| **Masivo** | Se lanza contra cualquiera que caiga, no hay una víctima elegida | Correos de phishing enviados a miles de direcciones a la vez |
 
Los ataques internos son estadísticamente los que más daño causan, aunque los externos se lleven todos los titulares. Los dirigidos son mucho más difíciles de parar que los masivos: si alguien te ha elegido con nombre y apellido, va a intentarlo varias veces y de distintas maneras

<br>

## 4 Clasificación de vulnerabilidades
### 4.1 De dónde salen las vulnerabilidades
- **De diseño**: el fallo está en el planteamiento del sistema o del protocolo (por ejemplo, un protocolo que envía las credenciales en claro es inseguro por diseño)
- **De implementación**: el diseño es correcto pero el código tiene errores (desbordamientos de búfer, validación de entrada que falta, condiciones de carrera)
- **De configuración**: el producto es bueno pero está mal puesto (credenciales por defecto, permisos abiertos, servicios de depuración activos en producción)
- **Humanas**: la persona es el vector (contraseñas reutilizadas, clics donde no se debe, información publicada en redes sociales que facilita un ataque dirigido)
- **De la cadena de suministro**: el fallo está en una biblioteca de terceros incluida en el proyecto; un proyecto medio arrastra cientos de dependencias, y es hoy una de las vías más peligrosas

<br>

### 4.2 Vulnerabilidades por dónde viven
| Ámbito | Vulnerabilidades típicas | Impacto probable |
|---|---|---|
| **Sistemas operativos** | Fallos del núcleo, servicios sin parchear, credenciales por defecto, permisos incorrectos, escalada de privilegios local | Toma de control del equipo, muy alto si es un servidor |
| **Redes** | Wifi con cifrado obsoleto o abierta, puertos innecesarios abiertos, protocolos sin cifrar (Telnet, FTP), electrónica de red con firmware antiguo, DNS sin protección | Escucha de tráfico, robo de credenciales, salto a la red interna |
| **Aplicaciones** | Fallos del OWASP Top 10 (inyección, XSS, control de acceso roto, fallos criptográficos, componentes vulnerables) y errores lógicos de negocio | Robo de datos, suplantación de usuarios, borrado o alteración masiva |

<br>

### 4.3 Cómo se identifican y se miden en la práctica
Cuando se publica una vulnerabilidad no se describe con un texto largo, se le asigna un código único y una puntuación numérica
 
| Sigla | Significado | Para qué sirve | Ejemplo |
|---|---|---|---|
| **CVE** | Common Vulnerabilities and Exposures | Identificador único y público de una vulnerabilidad concreta en un producto concreto | CVE-AAAA-NNNNN |
| **CWE** | Common Weakness Enumeration | Clasificación del tipo de fallo, con independencia del producto | CWE-79 (XSS) |
| **CVSS** | Common Vulnerability Scoring System | Puntuación de gravedad de 0 a 10 a partir de métricas objetivas | 9,8 · Crítica |
| **NVD** | National Vulnerability Database | Portal público que recoge los CVE con su análisis | nvd.nist.gov |
| **KEV** | Known Exploited Vulnerabilities | Catálogo público de CISA con las vulnerabilidades que se están explotando de verdad ahora | cisa.gov/known-exploited-vulnerabilities-catalog |
 
Tramos de gravedad del CVSS:
 
| Puntuación | Gravedad | Prioridad práctica |
|---|---|---|
| 0,0 | Ninguna | Informativa |
| 0,1 – 3,9 | Baja | Se corrige en el ciclo normal de mantenimiento |
| 4,0 – 6,9 | Media | Se planifica el parcheo a corto plazo |
| 7,0 – 8,9 | Alta | Prioritaria, se parchea en días |
| 9,0 – 10,0 | Crítica | Se para lo que estés haciendo, sobre todo si está expuesta a Internet |
 
**Idea clave**: un 9,8 en un servidor apagado en un armario no es urgente; un 6,5 en tu servidor web público, con exploit publicado, sí lo es. La puntuación es solo el punto de partida, quien decide la prioridad real es quien mira su propia exposición

<br>

## 5 Cómo se explota una vulnerabilidad
Los ataques serios no son un golpe único, son una campaña con fases. Conocerlas sirve para algo concreto: cada fase deja rastros distintos y se corta con medidas distintas

<br>

### 5.1 Fases habituales de un ataque
1. **Reconocimiento**: información pública de la organización, sus dominios, empleados, tecnología; no hay nada ilegal todavía y por eso casi no se detecta
2. **Enumeración y escaneo**: identificación activa de máquinas, puertos y servicios (por ejemplo con nmap); ya empieza a dejar huella
3. **Acceso inicial**: correo con adjunto malicioso, credencial comprada, servicio expuesto sin parchear
4. **Ejecución y persistencia**: se ejecuta el código y se asegura la vuelta aunque se reinicie el equipo (tareas programadas, servicios, cuentas nuevas)
5. **Escalada de privilegios**: de usuario normal a administrador
6. **Movimiento lateral**: se salta de un equipo a otro hasta llegar a lo que interesa
7. **Exfiltración**: se sacan los datos, normalmente disfrazados de tráfico legítimo
8. **Impacto**: cifrado, borrado, sabotaje o publicación de lo robado
Este esquema se conoce como **kill chain** (cadena de eliminación) y su versión más usada es la matriz MITRE ATT&CK, un catálogo público con miles de técnicas concretas por fase

<br>

### 5.2 El papel de los exploits y de las herramientas automatizadas
Un exploit es un programa o técnica que aprovecha una vulnerabilidad concreta. Cuando se publica un CVE grave, en pocos días aparece un exploit público, y a las pocas semanas aparece integrado en herramientas automatizadas
- **Metasploit**: marco de explotación más conocido, reúne miles de exploits clasificados y facilita su uso (con autorización)
- **Escáneres de vulnerabilidades** (Nessus, OpenVAS, Nikto): detectan automáticamente vulnerabilidades conocidas en una máquina o en una web
- **Herramientas de fuerza bruta** (Hydra, Medusa): prueban miles de contraseñas por segundo contra servicios accesibles
- **Automatización defensiva**: los IDS (sistemas de detección de intrusos) y los IPS (sistemas de prevención de intrusos) detectan estos patrones y alertan o bloquean

<br>

### 5.3 Vulnerabilidad de día cero y ventana de exposición
- **Vulnerabilidad de día cero (zero-day)**: la que se explota antes de que exista parche; el fabricante lleva cero días sabiéndola cuando ya se está usando en la calle
- **Ventana de exposición**: el tiempo que va desde que el parche está disponible hasta que se aplica; esa ventana la controla uno mismo por completo, y en las estadísticas de incidentes reales es responsable de mucho más daño que los días cero de verdad
**Aviso**: la mayoría de las intrusiones no aprovechan fallos desconocidos, sino fallos publicados y parcheados hace meses en sistemas que nadie actualizó. Actualizar es aburrido, pero es la medida más rentable que existe

<br>

## 6 Consecuencias sobre confidencialidad, integridad y disponibilidad
Hay que saber valorar las consecuencias de las amenazas sobre la tríada CID. Un ataque puede romper una dimensión de forma clara, o combinarlas

<br>

### 6.1 Impactos típicos de cada tipo de amenaza
| Amenaza | Confidencialidad | Integridad | Disponibilidad |
|---|---|---|---|
| **Ransomware** | Sí (doble extorsión: publican los datos) | Sí (los ficheros originales quedan inutilizables) | Sí (mientras dura el cifrado y la restauración) |
| **Phishing con robo de credenciales** | Sí (acceso a información confidencial) | Posible (según lo que hagan con la cuenta) | Posible |
| **DDoS** | No | No | Sí, muy alta |
| **Robo de portátil sin cifrar** | Sí, total | Posible | Sí (parcial, para el propietario) |
| **Inyección SQL con volcado de tabla** | Sí | Posible (si además borran o modifican) | Posible |
| **Empleado que altera facturas para defraudar** | Puede que no | Sí, plena | No |
| **Cifrado de disco perdido tras extraviar la clave** | No (nadie más lo lee) | Depende | Sí, plena |
 
El último caso es destacable: destruir la disponibilidad con tus propias manos por perder una clave es un incidente de seguridad, aunque no haya atacante

<br>

### 6.2 Otros impactos que no son técnicos
- **Económico**: coste del rescate, coste de recuperación, pérdida de ingresos por parada
- **Reputacional**: pérdida de confianza de clientes y de proveedores
- **Legal**: sanciones de la AEPD por brechas de datos personales, posibles responsabilidades penales por el artículo 197 del Código Penal
- **Operativo**: horas del equipo dedicadas a reconstruir en lugar de a producir
- **Humano**: estrés, culpabilidad, incluso despidos; es la parte que menos aparece en los informes técnicos y suele ser la que más marca a las personas

<br>

## 7 Señales y síntomas de un sistema comprometido
El malware moderno intenta pasar desapercibido, pero deja rastros. Reconocerlos a tiempo puede reducir mucho el impacto

<br>
 
### 7.1 Señales en un equipo individual
- Rendimiento muy inferior al habitual sin causa aparente
- Programas que se abren solos, ventanas emergentes que no venían de los programas propios
- Barras de herramientas nuevas en el navegador, buscador cambiado, redirecciones extrañas
- Ficheros con nombres raros o extensiones cambiadas (por ejemplo `.locked`, `.encrypted`)
- Consumo de datos muy alto sin explicación, o conexiones a IP en horarios extraños
- Antivirus deshabilitado sin haberlo tocado, actualizaciones bloqueadas
- Mensajes enviados a contactos que uno no ha escrito
- Cuentas de usuario nuevas no creadas por el propio usuario
- Tareas programadas o servicios no reconocidos
- Registros de acceso a horas inusuales

<br>

### 7.2 Señales en la red 
- Picos de tráfico saliente hacia direcciones desconocidas (posible exfiltración)
- Conexiones a dominios recién registrados o con nombres generados aleatoriamente (típico de C&C)
- Consultas DNS masivas sin patrón lógico
- Aumento súbito de tráfico entrante en un solo servicio (posible DoS)
- Escaneos de puertos entrantes
- Intentos repetidos de autenticación fallida en SSH, RDP, aplicaciones web
- Uso de protocolos raros o de puertos altos con volumen inusual

<br>

### 7.3 Dónde se buscan estas señales
La caza de estas señales se llama en el sector **caza de amenazas** (threat hunting)
 
| Fuente | Qué se busca ahí |
|---|---|
| **Registros del sistema (logs)** | Inicios de sesión, arranques de servicios, cambios de configuración |
| **Registros de aplicaciones** | Accesos anómalos, errores 500 repetidos, patrones raros |
| **Registros de red (NetFlow, IPFIX)** | Flujos de tráfico, orígenes, destinos, volúmenes |
| **IDS/IPS** | Alertas por patrones conocidos de ataque |
| **Antivirus/EDR** | Detecciones de malware y comportamientos sospechosos |
| **Servicios de reputación** | Comprobar si una IP o dominio están asociados a actividad maliciosa |

<br>

### 7.4 Indicadores de compromiso (IoC)
Un **indicador de compromiso** (Indicator of Compromise, IoC) es un dato observable que sugiere que un sistema ha sido comprometido
- **Basados en red**: direcciones IP, dominios, URL, huellas de peticiones
- **Basados en sistema**: nombres de fichero, hashes, claves de registro, rutas, procesos
- **Basados en registros**: patrones de inicio de sesión, cadenas concretas en los logs
 



<br>

---
>_Estela de Vega Martín | IES Ribera de Castilla 26/27._
