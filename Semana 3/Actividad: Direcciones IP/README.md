
# 🌐 Guía Técnica: Redes e IPs para Developers

## 1. Conceptos Fundamentales
| Concepto | Definición simple | Nivel técnico breve | Ejemplo |
| :--- | :--- | :--- | :--- |
| **IP** | La "matrícula" o dirección de tu dispositivo en internet. | Protocolo de capa 3 (Red) del modelo OSI para direccionamiento. | `192.168.1.1` |
| **IPv4** | El estándar antiguo, usa números cortos. | Formato de 32 bits dividido en 4 octetos decimales. | `172.217.13.174` |
| **IPv6** | El estándar nuevo, casi infinito y con letras. | Formato de 128 bits en ocho grupos hexadecimales. | `2001:db8::ff00:42` |

---

## 2. Tipos de IP (Clave para Desarrollo)

### Comparativa Rápida
* **Pública vs. Privada:** La **Pública** es la cara visible hacia internet (tu router); la **Privada** es interna y solo existe en tu red local (tu laptop, tu impresora).
* **Estática vs. Dinámica:** La **Estática** es fija (servidores); la **Dinámica** cambia al reiniciar la conexión (usuarios finales).

| Tipo | ¿Qué es? | ¿Cuándo se usa? | Ejemplo real |
| :--- | :--- | :--- | :--- |
| **Pública** | Identificador visible en la WAN (internet). | Para que el mundo encuentre tu servidor o router. | IP asignada por tu ISP. |
| **Privada** | Identificador en la LAN (red local). | Conectar dispositivos dentro de una misma casa/oficina. | `192.168.0.15` |
| **Estática** | Una dirección fija que no cambia nunca. | Servidores web, bases de datos o servicios VPN. | IP de Google: `8.8.8.8` |
| **Dinámica** | Una IP temporal que cambia automáticamente. | Dispositivos domésticos para optimizar el uso de IPs. | IP de tu móvil en el Wi-Fi. |

---

## 3. Conexión y Desarrollo (CRÍTICO)

* **IP en Backend Local:** Se usa el *loopback* o `localhost` (`127.0.0.1`). Es una dirección que apunta a tu propia máquina.
* **IP en Producción:** Se utiliza una **IP Pública Estática** (o un dominio que apunte a ella) proporcionada por el servicio de nube.
* **El dilema del Localhost:** No puedes acceder al `localhost` de otro computador porque esa dirección no sale a la red; es interna. Para conectar dos PCs, necesitas usar sus **IPs Privadas**.
* **Base de Datos en la Nube:** Suelen tener IPs públicas protegidas por **Whitelists** (listas blancas) donde solo autorizas la IP de tu servidor de backend para conectarse.

---

## 4. Caso Práctico: Debugging de Conexión
> **Escenario:** El frontend funciona pero no logra conectarse al backend.

### ¿Qué revisar?
1.  **Variables de Entorno (.env):** Verifica que el frontend no apunte a `localhost` si el backend ya está en la nube.
2.  **Firewall/Puertos:** Asegúrate de que el puerto del servidor (ej: 8080) esté abierto en el panel de control de tu hosting (AWS, Azure, etc.).
3.  **CORS:** Revisa si el navegador bloquea la petición por seguridad (Cross-Origin Resource Sharing).
4.  **Estado 404/500:** Usa las **DevTools (F12)** -> Pestaña **Network** para ver si el error es de ruta (404) o de lógica interna (500).

---

## 5. DHCP y DNS: La Infraestructura Invisible

* **DHCP (Dynamic Host Configuration Protocol):** El "recepcionista". Asigna automáticamente IPs privadas a los dispositivos que se conectan a la red.
* **DNS (Domain Name System):** El "traductor". Convierte nombres como `google.com` en IPs como `142.250.190.46`.

### Flujo de navegación paso a paso:
1.  Escribes la URL en el navegador.
2.  Tu PC consulta al **DNS** para obtener la IP del dominio.
3.  El **DNS** devuelve la IP numérica del servidor.
4.  El navegador viaja a esa **IP** para solicitar los archivos de la web.

---

## 6. Analogía Obligatoria
* **IP** = Dirección física de tu casa (calle y número).
* **DNS** = Tu agenda de contactos (buscas el nombre, el teléfono se marca solo).
* **DHCP** = El conserje de un hotel que te asigna una habitación disponible al llegar.

---

## 🧠 Bonus: Nivel Bootcamp Pro

* **NAT (Network Address Translation):** Permite que muchos dispositivos en una red local salgan a internet usando una sola **IP Pública**.
* **Docker Networking:** Cada contenedor tiene su propia IP privada interna. Para ver la app desde tu PC, debes mapear el puerto del contenedor al puerto de tu `localhost` (`-p 8080:3000`).
* **AWS (Elastic IPs):** Son IPs públicas estáticas que no cambian aunque reinicies o apagues tu instancia (servidor) EC2.
