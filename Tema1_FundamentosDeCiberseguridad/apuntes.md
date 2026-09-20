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

## 2. La tríada CID: ¿qué protegemos?
Toda medida de seguridad sirve, en el fondo, a uno de estos tres objetivos:
- **Confidencialidad** → garantiza que a la información solo acceda quien está autorizado
- **Integridad** → garantiza que la información no se altere sin autorización
- **Disponibilidad** → garantiza que la información esté accesible cuando se necesita

<br>

## 3. Amenazas activas y pasivas
Según cómo actúan, las amenazas se clasifican en dos grandes grupos:

| Tipo | Qué hace | Ejemplo | Rompe principalmente |
|---|---|---|---|
| **Amenaza pasiva** | Observa la información sin alterarla; intenta pasar desapercibida | Interceptar tráfico de red para leer contraseñas (sniffing) | **Confidencialidad** |
| **Amenaza activa** | Modifica, destruye o interrumpe la información o los sistemas | Cifrar ficheros con ransomware, borrar una base de datos | **Integridad y disponibilidad** - porque se modifican o borran datos y se impide el acceso a ellos |

<br>

> La amenaza pasiva es más difícil de detectar y se combate principalmente con **cifrado**. La amenaza activa es más "aparatosa" y se combate con **detección y recuperación**

<br>

## 4. Programas maliciosos (malware)
**Malware** = software malicioso. Cualquier programa diseñado para dañar un sistema, robar información, extorsionar al usuario o usar sus recursos sin permiso

### 4.1 Familias principales
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
  
### 4.2 Ransomware
- **Ransomware:** malware diseñado para bloquear el acceso de la víctima a su sistema o a sus datos (normalmente cifrándolos) hasta que se paga un rescate, habitualmente en criptomoneda
- **Características típicas:**
  - Cifra archivos con algoritmos fuertes (difíciles o imposibles de romper sin la clave)
  - Suele incluir una nota de rescate con instrucciones de pago y un plazo límite
  - Cada vez más combina la extorsión "clásica" con la **doble extorsión**: además de cifrar, roban los datos y amenazan con publicarlos si no se paga
  - Se propaga habitualmente por phishing, RDP mal protegido o explotando vulnerabilidades sin parchear
  - Pagar el rescate **no garantiza** recuperar los datos ni evita que se filtren igualmente

<br>

## 5. Ingeniería social, ataques a la red y a apps web
### 5.1 Ingeniería social: los fraudes más habituales
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

### 5.2 Ataques a la red
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

### 5.3 Ataques a aplicaciones web
| Ataque | Qué hace |
|---|---|
| **Inyección SQL (SQLi)** | Se introduce código SQL malicioso en un campo de entrada (formulario, buscador...) para manipular la base de datos: leer, modificar o borrar datos sin autorización |
| **Cross-Site Scripting (XSS)** | Se inyecta código (normalmente JavaScript) en una web que luego se ejecuta en el navegador de otros usuarios, permitiendo robar sesiones o cookies |
| **Cross-Site Request Forgery (CSRF)** | Engaña al navegador de una víctima autenticada para que realice, sin saberlo, una acción no deseada en una web donde tiene sesión iniciada |


---
>_Estela de Vega Martín | IES Ribera de Castilla 26/27._
