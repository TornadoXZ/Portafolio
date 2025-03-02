# Portafolio
# 📌 Configuración de un Balanceador de Carga en AWS para Dos Aplicaciones Web

Este repositorio contiene la documentación para configurar un **Application Load Balancer (ALB)** en AWS que distribuya tráfico entre dos instancias EC2 con aplicaciones web.

## 🌍 Requisitos Previos
- Cuenta en **AWS**.
- **Dos instancias EC2** en ejecución con aplicaciones web en **HTTP (puerto 80) o HTTPS (puerto 443)**.
- **Grupo de seguridad** configurado para permitir tráfico HTTP/HTTPS.

---

## 🚀 Paso 1: Crear un Balanceador de Carga (ALB)
1. **Accede a AWS Console** → Ve a **EC2**.
2. En el menú izquierdo, selecciona **Balanceadores de carga**.
3. Haz clic en **Crear balanceador de carga**.
4. **Selecciona** `Application Load Balancer (ALB)`.
5. **Configura:**
   - **Nombre:** `mi-balanceador`
   - **Esquema:** Público
   - **Protocolo:** HTTP / 80 (o HTTPS / 443 si tienes SSL)
   - **VPC:** La misma donde están las instancias
   - **Zonas de disponibilidad:** Elige al menos 2 subnets
6. **Siguiente: Configurar seguridad** (solo si usas HTTPS).

---

## 🎯 Paso 2: Crear un Grupo de Destino
1. En la sección **Grupos de destino**, haz clic en **Crear nuevo grupo**.
2. **Nombre:** `mis-instancias-web`
3. **Tipo de destino:** Instancia
4. **Protocolo y puerto:** HTTP / 80 (o el que use tu aplicación)
5. **Registrar instancias:**
   - Agrega las dos instancias EC2
   - Haz clic en **Agregar al grupo**

---

## ⚙️ Paso 3: Configurar la Regla de Enrutamiento
1. **Reglas de escucha** → Redirigir tráfico al **grupo de destino** `mis-instancias-web`.
2. Si usas **HTTPS**, agrega un certificado SSL en **AWS Certificate Manager**.

---

## 🔐 Paso 4: Configurar Seguridad y Permisos
1. **Abrir los puertos en el grupo de seguridad del ALB:**
   - Entrada HTTP (80) desde `0.0.0.0/0` (o HTTPS en 443).
2. **Abrir el puerto 80 en las instancias** (si aún no lo hiciste).

---

## 🛠️ Paso 5: Probar el Balanceador de Carga
1. Copia la **URL del balanceador** desde la consola de AWS.
2. Ábrelo en el navegador:
   ```
   http://mi-balanceador.elb.amazonaws.com
   ```
3. Refresca varias veces para ver si la carga se distribuye entre ambas instancias.

---

## 📌 Configuración Adicional: Rutas Específicas
Si cada instancia maneja una aplicación diferente, puedes configurar rutas:
1. **Editar Reglas de Escucha** en el ALB.
2. Agregar condiciones:
   - `/app1/*` → Redirigir a **instancia 1**
   - `/app2/*` → Redirigir a **instancia 2**

---

## 📢 ¡Listo! 🎉
Ahora tienes un **balanceador de carga en AWS** distribuyendo tráfico entre dos instancias con aplicaciones web. 🚀

Si necesitas ayuda con HTTPS, configuración avanzada o autoescalado, abre un issue en este repositorio. 😊
