# Actividad: Seguridad 🔐

### 🧩 1. Conceptos base

|Concepto|Definición simple|Nivel técnico breve|Ejemplo real|
|-|-|-|-|
|Permissions|Reglas que definen qué puede hacer un usuario|Control de acceso (RBAC, ACL) en sistemas y apps|Usuario puede ver datos pero no eliminarlos|
|Password segura|Contraseña difícil de adivinar o romper|Uso de hash, salting y políticas de complejidad|"G7#kP!92xQ" en vez de "123456"|
|Vulnerabilidad|Debilidad que puede ser explotada|Fallas en código, config o dependencias|Input sin validar permite inyección SQL|
|Intrusión|Acceso no autorizado a un sistema|Uso de exploits o credenciales robadas|Hacker entra con contraseña filtrada|
|Seguridad de red|Protección de datos y sistemas en una red|Firewalls, cifrado (TLS), segmentación|HTTPS protege datos al usar banca online|

---

### 🔑 2. Permissions (accesos en sistemas)

#### 🔐 Autenticación vs Autorización

##### ¿Qué es Autenticación?

Verifica **quién eres**.  
Ej: usuario + contraseña o token (JWT).

##### ¿Qué es Autorización?

Define **qué puedes hacer**.  
Ej: permisos para leer, crear o eliminar datos.

##### 🔑 Diferencia clave

* **Autenticación → identidad**
* **Autorización → permisos**

Primero te identificas, luego el sistema decide tus acciones.



##### 💻 Ejemplo developer

##### Login → ¿qué es?

Proceso de **autenticación** donde el usuario valida su identidad y recibe una sesión o token.

##### Roles (admin/user) → ¿qué es?

Parte de la **autorización**; define permisos según el rol.

---

### 🔒 3. A Good Password (lo mínimo obligatorio)

##### 🔐 ¿Qué hace que una contraseña sea segura?

* Larga (12+ caracteres)
* Mezcla de letras, números y símbolos
* Difícil de adivinar (sin datos personales)



##### ❌ ¿Por qué NO guardar contraseñas en texto plano?

* Si hay filtración, quedan \*\*expuestas directamente\*\*
* Cualquier persona puede leerlas
* Compromete todas las cuentas del usuario



##### 🔑 ¿Qué es hashing?

Proceso que convierte una contraseña en un valor irreversible.  No se puede volver al texto original (ej: bcrypt, SHA-256).


##### 💻 Ejemplo developer (Backend)

1. Usuario se registra:

   * Se aplica \*\*hash\*\* a la contraseña
   * Se guarda el hash en la base de datos
2. Usuario hace login:

   * Ingresa contraseña
   * Se hashea nuevamente
   * Se compara con el hash guardado

👉 Nunca se guarda la contraseña real, solo su versión protegida

---

### ⚠️ 4. Vulnerabilities (fallas reales)

#### ¿Qué es una vulnerabilidad?

Debilidad en un sistema que puede ser explotada para acceder, modificar o dañar información.



#### 🔓 Tipos comunes

* **SQL Injection**
Inyección de código SQL en inputs  → permite acceder o modificar la base de datos
* **XSS (Cross-Site Scripting)**
Inyección de scripts en páginas web  → roba sesiones o ejecuta código en el navegador
* **Exposición de datos**
Información sensible sin protección  → contraseñas, tokens o datos personales visibles



#### 💻 Ejemplo real (mala validación)

Un formulario de login **no valida inputs**:

´SELECT \\\* FROM users WHERE email = 'admin' OR '1'='1';


👉 **Resultado:**
- El sistema devuelve acceso sin validar correctamente la contraseña  
- Un atacante puede autenticarse como otro usuario (ej: admin)

#### 🧠 Idea clave
Una validación débil puede abrir la puerta a ataques que comprometen toda la aplicación

---

### 🚨 5. Intrusión (ataques)

#### ¿Qué es una intrusión?

Acceso no autorizado a un sistema o aplicación aprovechando vulnerabilidades o credenciales robadas.

#### 🎯 ¿Qué busca un atacante?

* Robar información (datos, contraseñas, tarjetas)
* Obtener acceso al sistema
* Interrumpir o dañar el servicio

#### ⚠️ ¿Qué pasa si una app es comprometida?

* Fuga de datos sensibles
* Pérdida de confianza de usuarios
* Caída del sistema o manipulación de información

#### 💻 Ejemplo

* **Robo de datos:** se filtran correos y contraseñas
* **Acceso no autorizado:** atacante entra como usuario o admin

---

### 🌐 6. Network Security (seguridad en red)

#### ¿Qué protege la seguridad de red?

Protege datos, dispositivos y sistemas contra accesos no autorizados y ataques.



#### 🔥 ¿Qué es un firewall?

Sistema que filtra el tráfico de red permitiendo o bloqueando conexiones según reglas.



#### 🔒 ¿Qué es HTTPS y por qué es importante?

Protocolo seguro que cifra la comunicación (TLS) → evita que terceros vean o modifiquen los datos.



#### 💻 Ejemplo developer

##### ¿Por qué usar HTTPS en APIs?

* Protege tokens y credenciales
* Evita ataques Man-in-the-Middle
* Garantiza integridad y confidencialidad de datos

---

### 💻 7. Conexión directa con desarrollo

#### ⚠️ ¿Qué errores comunes cometen los developers en seguridad?

* No validar inputs del usuario
* Guardar contraseñas sin hash
* Exponer APIs o rutas sin protección
* No usar HTTPS
* Confiar en datos del frontend



#### 🚨 ¿Qué pasaría si...?

##### ❌ No validas inputs

* Inyección de código (SQL Injection, XSS)
* Acceso o manipulación de datos

##### ❌ No proteges rutas

* Usuarios acceden a funciones restringidas
* Escalación de privilegios (ej: user → admin)

##### ❌ No usas HTTPS

* Datos viajan sin cifrar
* Pueden ser interceptados (tokens, passwords)

---

### 🌍 8. Caso práctico real: “Un usuario logra acceder a información que no le corresponde.”

#### ❌ ¿Qué falló?

* Falta de validación de permisos en el backend
* Confianza en datos del cliente (frontend)
* Posible endpoint expuesto sin control de acceso



#### 🔍 ¿Es problema de permisos, vulnerabilidad o intrusión?

* **Principal:** error de **permisos (autorización)**
* También es una **vulnerabilidad** explotada
* Puede considerarse **intrusión** si hubo intención maliciosa



#### 🛠️ ¿Cómo evitarlo como developer?

* Validar permisos en **cada endpoint** (backend)
* Implementar **roles y middleware de autorización**
* No confiar en el frontend
* Usar tokens seguros (JWT) y verificarlos
* Testear casos de acceso indebido (security testing)

---

### 🧪 9. Analogía: La seguridad como un edificio🏢

#### 🔐 Password (contraseña)

Es la **llave de la puerta principal**. Solo quien la tiene puede entrar



#### 🪪 Permissions (permisos)

Son las **tarjetas de acceso internas**. Definen a qué salas puedes entrar (admin / user)



#### ⚠️ Vulnerabilidad

Es una **puerta mal cerrada o ventana rota**. Alguien puede aprovecharla para entrar



#### 🚨 Intrusión

Es cuando alguien **entra sin permiso**. Usando una falla o robando una llave



#### 🌐 Seguridad de red

Son los **guardias, cámaras y alarmas.** Protegen el edificio y controlan accesos



#### 🧠 En resumen

* Password → entrar
* Permissions → qué puedes hacer
* Vulnerabilidad → debilidad
* Intrusión → acceso indebido
* Seguridad de red → protección total

---

### 🧠 BONUS: Conceptos clave

#### ¿Qué es JWT?

**JSON Web Token**: Es un token firmado que contiene información del usuario y se usa para autenticación sin sesiones en el servidor.



#### 🔑 ¿Qué es autenticación con tokens?

Método donde el usuario recibe un **token** al hacer login y lo envía en cada request para validar su identidad.



#### 🚦 ¿Qué es rate limiting?

Control que limita la cantidad de requests que un usuario o IP puede hacer en un tiempo determinado.




