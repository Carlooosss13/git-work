# PRÁCTICA: TRABAJO COLABORATIVO, GESTIÓN DE PULL REQUESTS Y RESOLUCIÓN DE CONFLICTOS EN GITHUB

***Nombres:*** Rodrigo García Delgado y Carlos Estévez González  
***Curso:*** 2º de Ciclo Superior de Desarrollo de Aplicaciones Web.

### ÍNDICE

- [Introducción](#introducción)
- [Objetivos](#objetivos)
- [Material empleado](#material-empleado)
- [Desarrollo](#desarrollo)
- [Conclusiones](#conclusiones)

---

#### ***Introducción***

En el desarrollo de aplicaciones web, consideramos fundamental el uso de sistemas de control de versiones distribuidos como Git y plataformas de alojamiento de código como GitHub. Durante esta práctica hemos trabajado con un flujo de trabajo colaborativo basado en la utilización de forks, ramas independientes, Pull Requests y revisión de código.

Uno de los principales aspectos que hemos trabajado ha sido la integración de código desarrollado de forma simultánea. Cuando dos desarrolladores modificamos las mismas líneas de un archivo en diferentes ramas, pueden producirse conflictos de fusión. En estos casos, Git no puede determinar automáticamente qué cambio debemos conservar, por lo que tenemos que intervenir manualmente para revisar, solucionar y consolidar los cambios antes de integrarlos en la rama principal.

#### ***Objetivos***

- Establecer diferentes roles de trabajo, utilizando `User 1` como propietario del repositorio original y `User 2` como colaborador externo, simulando un flujo de contribución de código abierto o interdepartamental.
- Dominar el flujo de Pull Requests mediante la bifurcación de proyectos, la creación de ramas independientes, la revisión remota del código y la comunicación a través del repositorio.
- Gestionar el ciclo de vida de Issues, vinculando ramas y confirmaciones locales para automatizar el cierre de tareas pendientes en GitHub.
- Resolver conflictos de código manualmente en local, seleccionando los cambios que consideramos adecuados y actualizando el repositorio original de forma segura.
- Versionar el software mediante el uso de etiquetas semánticas y la publicación formal de una Release en un repositorio remoto.

#### ***Material empleado***

- **Software de control de versiones:** Git instalado localmente en nuestros equipos.
- **Plataforma Cloud:** Dos cuentas activas en GitHub.
- **Entorno de desarrollo:** Editor de código y una terminal (Nano / Visual Studio Code / Terminal de Linux y Bash).
- **Archivos base de la práctica:** `index.html`, `bootstrap.min.css` y `cover.css`.

#### ***Desarrollo***

Para realizar correctamente esta práctica, hemos utilizado los siguientes identificadores de usuario correspondientes a las cuentas empleadas:

- **User 1:** `Carlooosss13`
- **User 2:** `Rodrigo-44`

---

##### 1. Inicialización en GitHub (User 1)

En primer lugar, hemos iniciado sesión con la cuenta de User 1 en GitHub y hemos creado un nuevo repositorio público llamado `git-work`.

Durante el asistente de configuración, hemos seleccionado la opción para incluir un archivo `README.md` y hemos añadido una licencia `MIT`.

##### 2. Descarga y subida de la estructura base (User 1)

En nuestra máquina local, hemos abierto la terminal y hemos clonado el repositorio que acabábamos de crear. Posteriormente, hemos introducido los archivos requeridos y los hemos enviado a la rama principal.

```bash
git clone https://github.com/Carlooosss13/git-work.git

touch index.html bootstrap.min.css cover.css

git add .
git commit -m "Initial project files"
git push origin main
