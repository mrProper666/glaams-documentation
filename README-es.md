# Instrucciones del proyecto GLAAMS

Este documento describe las instrucciones para trabajar con el proyecto GLAAMS, incluyendo la incorporación de especialistas, servicios, configuraciones y otras tareas administrativas. Cubre todo el proceso desde la configuración en cal.com hasta la creación de registros en GLAAMS CMS.

---

## 1. Añadir un especialista en cal.com (Admin)

**Lo realiza:** Administrador

El administrador añade al especialista en cal.com en el equipo **glaams** como **MEMBER**.

### Capturas de pantalla:

![Configuración](images/1-settings.png)

![Añadir miembro](images/2-add-member.png)

![Invitación](images/3-invite.png)

---

## 2. Registro del especialista en cal.com (Especialista)

**Lo realiza:** Especialista

El especialista se registra en cal.com mediante el enlace enviado por correo electrónico.

---

## 3. Configuración del perfil en cal.com (Especialista)

**Lo realiza:** Especialista

El especialista configura los campos necesarios en su perfil:

- **Nombre** (Name)
- **Email**
- **Idioma** (Language)
- **Zona horaria** (Timezone)
- **Formato de hora** (Time format)
- **Inicio de semana** (Start of week)
- **Google Calendar** – se selecciona para sincronización
- **Disponibilidad** (Availability) – se indican los días de la semana y los rangos horarios en los que el especialista ofrecerá sus servicios. Esta información aparece en la página del especialista como "Horario de trabajo" y tiene carácter general. Ausencias, vacaciones, compromisos personales, etc. pueden añadirse después mediante Google Calendar, de modo que el especialista define cuándo está realmente disponible.

### Capturas de pantalla:

![Perfil](images/4-profile.png)

![Configuración general](images/5-general.png)

![Disponibilidad](images/6-availability.png)

---

## 4. Crear Event Types en cal.com (Especialista)

**Lo realiza:** Especialista

El especialista añade sus propios Event Types:

### Pasos:

1. **Crear un nuevo Event Type:**
   - Añadir título
   - Añadir descripción
   - Establecer duración

2. **Configuración de ubicación:**
   - **Obligatorio:** seleccionar "**In Person (Attendee Address)**"
   - Esto significa que el servicio se realiza en la dirección del cliente

3. **Guardar configuración**

![Configuración de Event Type](images/8-event-type-settings.png)

---

## 5. Establecer límites en cal.com (Especialista)

**Lo realiza:** Especialista

El especialista establece los siguientes límites:

- **Tiempo de buffer antes del evento**
- **Tiempo de buffer después del evento**
- **Intervalo de franja horaria** (Time-slot interval) – las opciones de hora que se muestran en la página de servicios del especialista

![Límites de Event Type](images/9-event-type-limits.png)

---

## 6. Añadir especialista en GLAAMS (Admin)

**Lo realiza:** Administrador

### Pasos:

1. **Acceder al Content Manager:**
   - Content Manager → Specialist → Create new entry

2. **Rellenar campos obligatorios:**
   - Deben completarse todos los campos obligatorios
   - La mayor parte de la información debe ser proporcionada por el especialista o tomada de su perfil en cal.com

3. **Campos importantes:**
   - **Languages** – se usa para filtrar en el listado de especialistas
   - **Locations** – se usa para filtrar en el listado de especialistas
   - **Services** – se usa para filtrar en el listado de especialistas
     - ⚠️ **Importante:** Si el especialista ofrece un servicio que aún no está añadido, el Service debe añadirse primero

4. **Campo "calUsername":**
   - Rellenar con el **Username** del perfil del especialista en cal.com
   - Este campo es crítico para vincular GLAAMS y cal.com

5. **Campo "serviceConfigs":**
   - ⚠️ **No editar** – se rellenará automáticamente tras crear las configuraciones del especialista

6. **Guardar:**
   - Save
   - Publish

---

## 7. Crear configuraciones del especialista (Admin)

**Lo realiza:** Administrador

### Pasos:

1. **Acceder al Content Manager:**
   - Content Manager → Service Specialist Config → Create new entry

2. **Seleccionar especialista y servicio:**
   - Seleccionar el especialista (ya creado en el paso anterior)
   - Seleccionar el servicio

3. **Rellenar "Cal Event Type Id":**
   - ⚠️ **Campo crítico**
   - Rellenar con el valor tomado de cal.com
   - Es el ID del Event Type, que puede copiarse de la URL de la página:
     ```
     app.cal.com/event-types/XXXXXXX?tabName=setup
     ```
     - El número indicado como `XXXXXXX` en el ejemplo es el ID del Event Type
   - Este ID vincula la configuración en GLAAMS con el Event Type en cal.com

4. **Rellenar el resto de campos:**
   - **Duration** – puede tomarse de cal.com
   - **Title** – puede tomarse de cal.com
   - **Description** – puede tomarse de cal.com
   - **Price** – **se establece aquí**, no se toma de cal.com

5. **Imagen:**
   - Si no se añade imagen, se usará la del servicio vinculado

6. **Guardar:**
   - Save
   - Publish

---

## 8. Añadir servicio principal (Admin)

**Lo realiza:** Administrador

### Descripción:

Los servicios principales aparecen en:
- Las secciones "Treatments" del sitio
- El campo de filtro "All treatments"

Están pensados para tener sus propias páginas informativas.

### Campos a rellenar:

- **Page title** – se muestra en el frontend del servicio
- **Short description** – se muestra en el frontend del servicio
- **How It Works** (sección) – se muestra en el frontend del servicio
- **FAQ** (sección) – se muestra en el frontend del servicio
- **Benefits** (sección) – se muestra en el frontend del servicio
- **Sub-services** – seleccionar una o más opciones

### Campos que no deben editarse:

- **specialists** – no editar
- **specialistConfigs** – no editar

### Sub Service:

Sub Service se crea de forma similar a un servicio, con la diferencia de que:
- Los subservicios **no tienen páginas**
- Se añaden para enlazar con un servicio principal

---

## 9. Añadir usuario CMS para el especialista (Admin)

**Lo realiza:** Administrador

### Objetivo:

Se crea un usuario en Strapi vinculado al especialista. Así el especialista podrá:
- Iniciar sesión en el sistema GLAAMS
- Ver estadísticas de sus reservas
- Editar su información
- Cambiar su contraseña
- Añadir imágenes a la galería

### Pasos:

1. **Acceder al Content Manager:**
   - Content Manager → User → Create new entry

2. **Rellenar campos:**
   - **username** – nombre de usuario del especialista
   - **email** – el email con el que está registrado el especialista en cal.com
   - **password** – contraseña de acceso
   - **confirmed** – `true`
   - **role** – `Authenticated`
   - **specialist** – seleccionar del desplegable el especialista creado en el paso 6

3. **Guardar:**
   - Save
   - Publish

---

## Notas importantes

- Todos los pasos deben realizarse en el orden indicado
- El campo "Cal Event Type Id" es crítico para el correcto funcionamiento del sistema
- Los servicios deben crearse antes de añadir un especialista si este ofrece un servicio que aún no existe
- Tras crear las configuraciones, el campo "serviceConfigs" en el perfil del especialista se rellena automáticamente
