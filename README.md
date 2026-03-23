### 🌐 Actividad: Fundamentos entre redes

### ¿Qué es cada dispositivo?



|Dispositivo|Definición simple|Nivel técnico del modelo OSI|Ejemplo real|
|-|-|-|-|
|Router|Dispositivo que conecta diferentes redes entre sí (por ejemplo, tu casa e Internet)|Opera en capa 3, usa direcciones IP para enrutar paquetes entre redes|El router WiFi de tu casa que te conecta a Internet|
|Switch|Dispositivo que conecta varios equipos dentro de una misma red local|Opera en capa 2, utiliza direcciones MAC para enviar datos al dispositivo correcto|Un switch en una oficina conectando computadores e impresoras|
|Hub|Dispositivo básico que conecta varios equipos y envía datos a todos por igual|Opera en capa 1, por cables fisicas y señales electricas|Un hub antiguo conectando varios PCs en una red pequeña|





### ¿Que hace el router con los paquetes de datos?



Un router toma decisiones sobre cómo mover los paquetes de datos entre redes. En términos simples, hace lo siguiente:



#### 🔹 ¿Qué hace con los paquetes?

* Recibe el paquete desde un dispositivo (como tu PC o celular) o desde otra red.
* Lee la dirección IP de destino.
* Analiza distintas rutas para dónde debe ir el paquete.
* Decide la mejor ruta para dónde enviarlo (la más rápida, disponible o eficiente).
* Reenvía el paquete
* Lo manda al siguiente dispositivo en el camino hacia su destino final.



#### 🧠Un ejemplo concreto:

Cuando entras a una página web:

* Tu computador envía un paquete al router
* El router ve que el destino está en Internet
* Lo envía a tu proveedor de Internet
* Y así va saltando entre routers hasta llegar al servidor



👉 En resumen, el router dirige el tráfico, como si fuera un GPS de datos, asegurando que cada paquete llegue a su destino correcto.



### ¿Como decide un switch a donde enviar la informacion?



Un switch decide a dónde enviar la información utilizando direcciones MAC que son identificadores únicos de cada dispositivo en la red.



#### 🔹 ¿Cómo lo hace?

* Recibe el paquete desde un dispositivo conectado
* Lee e identifica la dirección MAC de origen y destino
* Aprende automáticamente: guarda la MAC de origen junto al puerto por donde llegó (esto forma su tabla MAC)
* Consulta su tabla MAC para ver en qué puerto está el destino
* Envía el paquete solo a ese puerto, en lugar de a todos



👉 En simple: el switch aprende y recuerda dónde está cada dispositivo, y así envía los datos de forma directa y eficiente.



### ¿Por qué el hub es considerado obsoleto?



El hub es considerado obsoleto porque es muy ineficiente comparado con dispositivos modernos como el switch.



#### 🔹 Principales razones:

* Genera un broadcast: envía el paquete a todos los puertos aunque solo un dispositivo sea el destino
* Sin inteligencia: no aprende direcciones (ni MAC ni IP), a diferencia del switch o router
* Menor seguridad: cualquier dispositivo puede “ver” el tráfico de los demás
* Genera colisiones: varios equipos pueden enviar datos al mismo tiempo, causando interferencias



👉 En corto: el hub es obsoleto porque es lento, inseguro y poco eficiente, mientras que el switch hace el mismo trabajo de forma mucho más inteligente.



### ¿Que rol cumple el router cuanto tu haces una peticion a una API?



**Cuando haces una petición:**

* Tu aplicación genera la solicitud HTTP hacia api.miapp.com
* Esa solicitud sale desde tu computador y llega a tu router
* El router lee la dirección IP de destino
* Decide que ese destino está fuera de tu red local
* Reenvía el paquete a tu proveedor de Internet (ISP)
* Desde ahí, el paquete viaja por varios routers hasta llegar al servidor de la API



Cuando el servidor responde el proceso se invierte y tu router recibe los datos y los entrega a tu dispositivo



👉 En corto: el router actúa como puerta de salida y entrada de tu red, enviando tu petición hacia Internet y trayendo la respuesta de vuelta.



### ¿Por qué un switch es importante en un backend o data center?



Un switch es clave en un backend o data center porque permite que los servidores se comuniquen de forma rapida, eficiente y sin interferencias.



#### 🔹 ¿Por qué es importante?

* **Comunicación directa entre servidores:**
  Envía datos solo al servidor correcto usando direcciones MAC → menos tráfico innecesario

* **Alto rendimiento:**
  Cada conexión tiene su propio ancho de banda, evitando colisiones y cuellos de botella

* **Baja latencia:**
  Fundamental para APIs, microservicios y bases de datos que necesitan respuestas rápidas

* **Escalabilidad:**
  Permite conectar muchos servidores, contenedores y servicios dentro de la misma red

* **Soporte para redes internas (LAN):**
  Todo el tráfico interno del backend (por ejemplo entre API y base de datos) pasa por switches



##### 🔹 Ejemplo concreto



En un data center:

* Un servidor backend hace una consulta a una base de datos
* El switch envía esa solicitud directamente al servidor
* La respuesta vuelve por el mismo camino, rápido y sin afectar a otros equipos



👉 En simple: el switch es importante porque optimiza la comunicación interna del backend, haciendo que todo sea más rápido, estable y eficiente.



### ¿Que problemas de red podrian afectar tu aplicacion aunque tu codigo este "correcto"?



Aunque tu código esté perfecto, hay varios problemas de red que pueden afectar tu aplicación:



#### 🔹 Problemas comunes

* **Alta latencia**
Las respuestas tardan mucho → tu app se siente lenta

* **Pérdida de paquetes**
Algunos datos no llegan → errores, timeouts o respuestas incompletas

* **Congestión de red**
Demasiado tráfico → caídas de rendimiento o interrupciones

* **Fallas de DNS**
No se puede resolver el dominio (ej: api.miapp.com) → la petición nunca sale

* **Problemas de enrutamiento**
Los paquetes toman rutas incorrectas o se pierden entre routers

* **Switch saturado o mal configurado**
Lentitud en la comunicación interna entre servicios

* **Firewall o reglas de seguridad**
Bloqueo de puertos o peticiones → la API no responde

* **Caídas del servidor o del ISP**
El servicio simplemente no está disponible



#### 🔹 Ejemplo concreto

Tu fetch("https://api.miapp.com") puede fallar aunque el código esté bien porque:

* El DNS no responde
* La red está lenta
* El servidor no puede ser alcanzado



👉 En simple: tu app depende de la red, y si la red falla, tu aplicación también falla, aunque el código sea correcto.



#### 🔹 ¿Podría ser problema de router? ¿Por qué?



Podría ser. El router es el que conecta tu red con Internet. Si falla:

* No hay salida ni entrada de tráfico
* Los usuarios no pueden llegar a tu servidor



👉 Ejemplos:



* Mala configuración de rutas
* Caída del router o del ISP



➡️ Resultado: nadie puede acceder a la app desde fuera



#### 🔹 ¿Podría ser problema de switch? ¿Por qué?



Sí, pero afecta más a la red interna. El switch conecta servidores dentro del data center.



👉 Ejemplos:



* Un servidor (API o base de datos) no responde
* Hay lentitud entre servicios
* Un puerto está caído



➡️ Resultado:



La app puede estar “arriba”, pero funciona mal o no responde correctamente



#### 🔹¿Cómo distinguir si es problema de red o de código?






* Si nadie puede acceder → probablemente red (router, DNS, firewall)
* Si responde con errores (500, etc.) → probablemente código
* Si no hay logs de peticiones → problema de red
* Si hay logs con errores → problema de backend


**👉 En corto:**

* Router → problemas de acceso desde Internet
* Switch → problemas internos entre servidores
* Código vs red → revisa logs, conectividad y alcance del fallo



### Analogia de comprender lo que es Router, Switch \& Hub



#### 🏙️ Analogía: tráfico en una ciudad

**Router 🌐**

Es como una salida de autopista o peaje

👉 Decide por qué carretera enviar los autos hacia otras ciudades

(conecta tu red con Internet)

**Switch 🚦**

Es como un cruce inteligente dentro de la ciudad

👉 Sabe exactamente qué calle tomar para llegar a una dirección específica

(envía los datos directamente al dispositivo correcto)

**Hub 🚨**

Es como un cruce sin semáforos donde todos avanzan a la vez

👉 Todos reciben el tráfico, aunque no les corresponda

(genera desorden y posibles choques = colisiones)



👉 En simple:

* Router = decide cómo salir a otras ciudades
* Switch = dirige el tráfico correctamente dentro
* Hub = caos, todos reciben todo



### ¿Dónde entra un Load Balancer en todo esto?



Siguiendo la analogía de la ciudad 🏙️:



* Router → te saca hacia otras ciudades
* Switch → organiza el tráfico dentro de la ciudad
* Load Balancer ⚖️ → es como un policia que reparte autos entre varios edificios iguales



**👉 Su función:**

* Recibe muchas solicitudes (usuarios)
* Decide a qué servidor enviarlas
* Distribuye la carga para que ninguno colapse



**El load balancer:**

* Evita que un solo servidor se sobrecargue
* Mejora rendimiento y disponibilidad
* Puede detectar servidores caídos y dejar de enviarles tráfico



#### 🔹 Ejemplo concreto



Tu app hace:



fetch("https://api.miapp.com")



👉 Lo que pasa:



La petición llega al load balancer

Este decide:

Usuario A → Servidor 1

Usuario B → Servidor 2

El servidor responde normalmente

👉 En corto

Router = conecta redes

Switch = organiza dentro de la red

Load Balancer = reparte el tráfico entre varios servidores



### ¿Que relacion tiene esto con cloud (como AWS, Azure, etc)?



Tiene una relación directa: En cloud todos estos componentes existen como servicios gestionados.



#### 👉 Ejemplos:

* Router → redes virtuales (VPC, Virtual Network)
* Switch → redes internas (subnets) dentro del cloud
* Load Balancer → servicios como Elastic Load Balancer (AWS) o Azure Load Balancer

#### 

#### 🔹 ¿Qué significa esto?

* No configuras el hardware físico, el proveedor cloud lo maneja por ti
* Tú solo defines reglas, escalado y comportamiento



👉 **En simple:** el cloud virtualiza y automatiza router, switch y load balancer para que puedas escalar tu aplicación fácilmente sin preocuparte por la infraestructura física.

