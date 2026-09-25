# PRÁCTICA: TRABAJO COLABORATIVO, GESTIÓN DE PULL REQUESTS Y RESOLUCIÓN DE CONFLICTOS EN GITHUB

**Autores:** Rodrigo García Delgado y Carlos Estévez González  
**Curso:** 2º de Ciclo Superior de Desarrollo de Aplicaciones Web  

---

## ÍNDICE

1. [Introducción](#introducción)
2. [Objetivos](#objetivos)
3. [Material empleado](#material-empleado)
4. [Desarrollo](#desarrollo)
5. [Conclusiones](#conclusiones)

---

## Introducción

En el desarrollo de aplicaciones web, consideramos fundamental el uso de sistemas de control de versiones distribuidos como Git y plataformas de alojamiento de código como GitHub. Nuestro flujo de trabajo profesional se basa en la colaboración multiusuario mediante forks, ramas de características (*feature branches*) e hilos de revisión de código conocidos como *Pull Requests* (PR).

Uno de los desafíos más comunes con los que nos enfrentamos en los equipos de desarrollo es la integración de código concurrente, lo que a menudo genera conflictos de fusión. Estos ocurren cuando dos desarrolladores modificamos las mismas líneas de un mismo archivo en diferentes ramas. Git no puede determinar automáticamente cuál es el cambio correcto, por lo que exige nuestra intervención manual para auditar, limpiar y consolidar la versión final del software antes de su despliegue o etiquetado de producción.

---

## Objetivos

* **Establecer roles de trabajo:** Asignamos a *User 1* como propietario del *upstream* y a *User 2* como colaborador externo para simular un flujo de contribución de código abierto o interdepartamental.
* **Dominar el flujo de Pull Requests:** Practicamos la bifurcación de proyectos, la creación de ramas independientes, la revisión remota de código y la retroalimentación directa en el hilo del repositorio.
* **Gestionar el ciclo de vida de Issues:** Vinculamos ramas y confirmaciones locales para automatizar el cierre de tareas pendientes en GitHub.
* **Resolver conflictos de código:** Enfrentamos y solucionamos conflictos de manera manual en entorno local, seleccionando la lógica de negocio adecuada y actualizando el repositorio original de forma segura.
* **Versionar el software:** Aplicamos etiquetas semánticas y publicamos formalmente una *Release* en entornos remotos.

---

## Material empleado

* **Software de control de versiones:** Git instalado localmente en nuestras estaciones de trabajo.
* **Plataforma Cloud:** Dos cuentas activas en GitHub.
* **Entorno de desarrollo:** Editor de código y terminal (Nano / Visual Studio Code / Terminal de Linux y Bash).
* **Archivos base de la práctica:** `index.html`, `bootstrap.min.css` y `cover.css`.

---

## Desarrollo

Para la correcta ejecución de esta práctica, asignamos los siguientes identificadores basados en nuestras cuentas reales empleadas en el laboratorio:

* **User 1:** Carlooosss13
* **User 2:** Rodrigo-44

### 1. Inicialización en GitHub (User 1)

User 1 inicia sesión en su cuenta de GitHub y crea un nuevo repositorio público llamado `git-work`. Durante el asistente de configuración, marca obligatoriamente las casillas para incluir un archivo `README.md` y añadir una licencia MIT.

### 2. Descarga y subida de la estructura base (User 1)

En su máquina local, User 1 abre la terminal y clona el repositorio recién creado. Posteriormente, creamos e introducimos los archivos requeridos y los subimos a la rama principal.

```bash
# Clonamos el repositorio
git clone https://github.com/Carlooosss13/git-work.git
cd git-work

# Creamos los archivos base
touch index.html bootstrap.min.css cover.css

# Subimos los cambios a la rama principal
git add .
git commit -m "Initial project files"
git push origin main
```


### 3. Bifurcación del proyecto (User 2)

User 2 accede a la URL pública del repositorio de User 1 en GitHub y hace clic en el botón **Fork**. Esto genera una copia idéntica del repositorio bajo su propia cuenta. Acto seguido, clonamos esta copia en la máquina local de User 2:

```bash
user2@maquina-local:~$ git clone https://github.com/Rodrigo-44/git-work.git
user2@maquina-local:~$ cd git-work
```

### 4. Apertura del primer Issue y desarrollo en rama (User 1 y User 2)

User 1 se dirige a la sección **Issues** de su repositorio original y crea una nueva incidencia con el título exacto: `Add custom text for startup contents`. El sistema le asigna el identificador `#1`.

User 2, al ver la incidencia abierta, crea una rama local llamada `custom-text` para realizar la tarea, modifica el archivo `index.html` con contenido personalizado para una supuesta startup (**NovaTech**) y sube la rama a su fork:

```bash
# Comandos ejecutados en la máquina de User 2
git checkout -b custom-text

# Modificamos el fichero index.html personalizándolo para NovaTech
git add index.html
git commit -m "Añadido texto corporativo para la startup"
git push origin custom-text
```


Una vez subido el código, User 2 accede a GitHub y abre un *Pull Request* (PR) apuntando desde su rama `USER2:custom-text` hacia la rama `USER1:main`.

### 5. Revisión remota e inserción de cambios (User 1)

Para probar los cambios en local antes de aceptarlos, User 1 añade el repositorio de User 2 como un origen remoto secundario llamado `upstream`. Estando en esa rama, User 1 realiza cambios adicionales sobre el archivo `index.html` local y los sube directamente al mismo PR a través de su enlace remoto:

```bash
# Comandos en la máquina de User 1
git fetch upstream custom-text
git checkout custom-text

# User 1 realiza modificaciones adicionales sobre index.html
git add index.html
git commit -m "User 1: Corrección menor de formato en landing"
git push upstream custom-text
```

### 6. Conversación en GitHub e integración final

En la interfaz web de GitHub, dentro del hilo del PR, mantenemos una breve conversación técnica. Realizamos modificaciones adicionales en nuestros respectivos entornos locales sobre la rama `custom-text` y las volvemos a subir para actualizar de forma dinámica la vista del Pull Request.

Finalmente, User 1 aprueba el PR en GitHub haciendo clic en **Merge Pull Request**. Para cerrar el issue `#1` de forma limpia, añadimos en el mensaje de fusión la sintaxis `Closes #1`.

### 7. Sincronización de ramas principales

Tras la fusión, ambos nos encargamos de actualizar nuestras ramas principales en local:

**User 1:**
```bash
git checkout main
git pull origin main
```

**User 2 (vincula el repositorio original de User 1 para actualizar su copia):**
```bash
git remote add upstream https://github.com/Carlooosss13/git-work.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### 8. Creación del segundo Issue y commit aislado (User 1)

User 1 abre una segunda issue titulada `Improve UX with cool colors` (identificador asignado automáticamente por GitHub como `#3`). A continuación, modifica de forma local el archivo `cover.css`, cambiando la línea 10 a `color: purple;`. Registra el cambio localmente pero no realiza el `git push`:

```bash
mint@mint:~/git-work$ nano cover.css
mint@mint:~/git-work$ git add cover.css
mint@mint:~/git-work$ git commit -m "Change color to purple in cover.css"
[main 9736b2a] Change color to purple in cover.css
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### 9. Modificación concurrente y envío de PR (User 2)

Simultáneamente, User 2 crea una rama llamada `cool-colors`, edita la línea 10 del mismo archivo `cover.css` asignando el valor `color: darkgreen;` y realiza la subida para solicitar la integración:

```powershell
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git checkout -b cool-colors
# User 2 cambia la línea 10 de cover.css a color: darkgreen;
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git add cover.css
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git commit -m "Change color to darkgreen in cover.css"
[cool-colors 939e110] Change color to darkgreen in cover.css
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git push origin cool-colors
```

User 2 envía el correspondiente *Pull Request* a User 1. GitHub nos notifica de inmediato que el archivo posee cambios incompatibles y no se puede fusionar automáticamente.

### 10. Gestión del conflicto en el entorno local (User 1)

User 1 descarga la rama del conflicto a su entorno local para solventar el bloqueo:

```bash
git fetch upstream cool-colors
git checkout main
git merge upstream/cool-colors
```

La terminal nos muestra el siguiente aviso de error:  
`CONFLICT (content): Merge conflict in cover.css. Automatic merge failed; fix conflicts and then commit the result.`

### 11. Edición del conflicto y cierre de Issue

User 1 abre el archivo `cover.css` con su editor. Nos encontramos con los delimitadores estándar de conflicto de Git:

```css
<<<<<<< HEAD
color: purple;
=======
color: darkgreen;
>>>>>>> upstream/cool-colors
```

---

2. Experimentar la resolución manual de conflictos de código, aprendiendo a auditar las diferencias y tomar decisiones de integración sin perder cambios clave.
3. Automatizar la gestión de tareas mediante la vinculación de *Issues* y mensajes de *commit* enriquecidos (`Closes #ID`).
