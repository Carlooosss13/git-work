PRÁCTICA: TRABAJO COLABORATIVO, GESTIÓN DE PULL REQUESTS Y RESOLUCIÓN DE CONFLICTOS EN GITHUB

svg

Nombre: Rodrigo García Delgado y Carlos Estévez González [1] Curso: 2º de Ciclo Superior de Desarrollo de Aplicaciones Web. [1]

ÍNDICE

svg

Introducción
Objetivos
Material empleado
Desarrollo
Conclusiones
Introducción.

svg

En el desarrollo de aplicaciones web, el uso de sistemas de control de versiones distribuidos como git y plataformas de alojamiento de código como GitHub es fundamental. El flujo de trabajo profesional se basa en la colaboración multiusuario mediante forks, feature branches, e hilos de revisión de código conocidos como Pull Requests.

Uno de los desafíos más comunes en los equipos de desarrollo es la integración de código concurrente, lo que a menudo genera conflictos de fusión. Estos ocurren cuando dos desarrolladores modifican las mismas líneas de un mismo archivo en diferentes ramas. Git no puede determinar automáticamente cuál es el cambio correcto, por lo que exige una intervención manual para auditar, limpiar y consolidar la versión final del software antes de su despliegue o etiquetado de producción.

Objetivos.

svg

Establecer roles de trabajo (user1 como propietario del upstream y user2 como colaborador externo) simulan un flujo de contribución de código abierto o interdepartamental.
Dominar el flujo de Pull Requests (PR) mediante la bifurcación de proyectos, la creación de ramas independientes, la revisión remota de código y la retroalimentación directa en el hilo del repositorio.
Gestionar el ciclo de vida de Issues, vinculando ramas y confirmaciones locales para automatizar el cierre de tareas pendientes en GitHub.
Resolver conflictos de código de manera manual en local, seleccionando la lógica de negocio adecuada y actualizando el repositorio original de forma segura.
Versionar el software mediante el uso de etiquetas semánticas y la publicación formal de una Release en entornos remotos.
Material empleado.

svg

Software de control de versiones: Git instalado localmente en las estaciones de trabajo.
Plataforma Cloud: Dos cuentas activas en GitHub.
Entorno de desarrollo: Editor de código y una terminal (Nano / Visual Studio Code / Terminal de Linux y Bash).
Archivos base de la práctica: index.html, bootstrap.min.css y cover.css.
Desarrollo.

svg

Para la correcta ejecución de esta práctica, se asignan los siguientes identificadores de usuario basados en las cuentas reales empleadas en los laboratorios:

User 1: Carlooosss13 [3]
User 2: Rodrigo-44 [4]
1. Inicialización en GitHub (User 1)

svg

User 1 inicia sesión en su cuenta de GitHub y crea un nuevo repositorio público llamado git-work. Durante el asistente de configuración, marca obligatoriamente las casillas para incluir un archivo README.md y añade una licencia MIT.

2. Descarga y subida de la estructura base (User 1)

svg

En su máquina local, User 1 abre la terminal y clona el repositorio recién creado. Posteriormente, introduce los archivos requeridos y los envía a la rama principal.

# CLONAR EL REPOSITORIO
git clone https://github.com

# CREAR LOS ARCHIVOS
touch index.html bootstrap.min.css cover.css

# SUBIMOS LOS CAMBIOS
git add .
git commit -m "Initial project files"
git push origin main

svg

[Aquí se incluye la captura de pantalla de la creación del repositorio e inicialización] [3]

3. Bifurcación del proyecto (User 2)

svg

User 2 accede a la URL pública del repositorio de User 1 en GitHub y hace clic en el botón Fork situado en la esquina superior derecha. Esto genera una copia idéntica del repositorio bajo el espacio de nombres de User 2. Acto seguido, lo descarga en su propia máquina local:

user2@maquina-local:~$ git clone https://github.com
user2@maquina-local:~$ cd git-work

svg

4. Apertura del primer Issue y desarrollo en rama (User 1 y User 2)

svg

User 1 se dirige a la sección Issues de su repositorio original y crea una nueva con el título exacto: Add custom text for startup contents. El sistema le asigna el identificador #1.

User 2, al ver la incidencia abierta, crea una rama local llamada custom-text para realizar la tarea, modifica el archivo index.html con contenido personalizado para una supuesta startup (NovaTech) y sube la rama a su fork:

# Comandos ejecutados en la máquina de User 2
git checkout -b custom-text

# [User 2 edita aquí el fichero index.html personalizándolo para NovaTech]
git add index.html
git commit -m "Añadido texto corporativo para la startup"
git push origin custom-text

svg

[Aquí se incluye la captura del editor de código index.html con las etiquetas de NovaTech e Issue #1 abierta] [4, 5]

Una vez subido, User 2 accede a GitHub y abre un Pull Request (PR) apuntando desde su rama USER2:custom-text hacia la rama USER1:main.

5. Revisión remota e inserción de cambios (User 1)

svg

Para probar los cambios en su máquina local antes de aceptarlos, User 1 añade el repositorio de User 2 como un origen remoto secundario llamado upstream. Estando en esa rama, User 1 realiza cambios adicionales sobre el archivo index.html local y los sube directamente al mismo PR a través de su enlace remoto:

# Comandos en la máquina de User 1
git fetch upstream custom-text
git checkout custom-text

# [User 1 realiza modificaciones adicionales sobre index.html]
git add index.html
git commit -m "User 1: Corrección menor de formato en landing"
git push upstream custom-text

svg

6. Conversación en GitHub e integración final

svg

En la interfaz web de GitHub, dentro del hilo del PR, ambos alumnos mantienen una breve conversación técnica. Cada usuario realiza al menos una modificación adicional en sus respectivos entornos locales sobre la rama custom-text y la vuelve a subir para actualizar de forma dinámica la vista del Pull Request.

Finalmente, User 1 aprueba el PR en GitHub haciendo clic en Merge Pull Request. Para cerrar el issue número 1 de forma limpia, se añade en el mensaje de fusión la sintaxis Closes #1.

7. Sincronización de ramas principales

svg

Tras la fusión, ambos alumnos deben actualizar sus ramas principales en local:

User 1:
git checkout main
git pull origin main

svg

User 2 vincula el repositorio original de User 1 para actualizar su propia copia:
git remote add upstream https://github.com
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

svg

8. Creación del segundo Issue y commit aislado (User 1)

svg

User 1 abre una segunda issue titulada Improve UX with cool colors (identificador asignado automáticamente por GitHub como #3 según capturas del sistema). A continuación, modifica de forma local el archivo cover.css, cambiando la línea 10 a color: purple;. Registra el cambio localmente pero no realiza el comando git push:

# Entorno local de User 1
mint@mint:~/git-work$ nano cover.css
mint@mint:~/git-work$ git add cover.css
mint@mint:~/git-work$ git commit -m "Change color to purple in cover.css"
[main 9736b2a] Change color to purple in cover.css
 1 file changed, 1 insertion(+), 1 deletion(-)

svg

9. Modificación concurrente y envío de PR (User 2)

svg

Simultáneamente, User 2 crea una rama llamada cool-colors, edita la línea 10 del mismo archivo cover.css asignando el valor color: darkgreen; y realiza la subida para solicitar integración:

# Entorno local de User 2
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git checkout -b cool-colors
# [User 2 cambia la línea 10 de cover.css a color: darkgreen;]
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git add cover.css
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git commit -m "Change color to darkgreen in cover.css"
[cool-colors 939e110] Change color to darkgreen in cover.css
PS C:\Users\Usuario\Trabajo_Carlos\git-work> git push origin cool-colors

svg

User 2 envía el correspondiente Pull Request a User 1. GitHub notificará de inmediato que el archivo posee cambios incompatibles y no se puede fusionar automáticamente.

10. Gestión del conflicto en el entorno local (User 1)

svg

User 1 descarga la rama del conflicto a su entorno local para solventar el bloqueo:

git fetch upstream cool-colors
git checkout main
git merge upstream/cool-colors

svg

La terminal arrojará el siguiente aviso de error: CONFLICT (content): Merge conflict in cover.css. Automatic merge failed; fix conflicts and then commit the result.

11. Edición del conflicto y cierre de Issue

svg

User 1 abre el archivo cover.css con su editor. Se encontrarán los delimitadores estándar de conflicto de Git:

<<<<<<< HEAD
color: purple;
=======
color: darkgreen;
>>>>>>> upstream/cool-colors
