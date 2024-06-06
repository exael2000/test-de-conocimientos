## Sección 3: Git

1. **Pregunta Teórica:**
- ¿Qué es Git y para qué se utiliza en el desarrollo de software?
    Git: Es un sistema de control de versiones distribuido utilizado para rastrear cambios en el código fuente durante el desarrollo de software. Permite a los equipos colaborar, manejar versiones y revertir cambios cuando sea necesario.

1. **Pregunta de Comandos:**
- ¿Cuál es el comando para clonar un repositorio de Git?
    git clone <url-del-repositorio>


1. **Pregunta Teórica:**
- Explica qué es un "branch" (rama) en Git y para qué se utiliza.
    Branch (Rama): Es una línea de desarrollo independiente en un repositorio de Git. Se utiliza para desarrollar características, corregir errores o experimentar de manera aislada del código principal.

1. **Pregunta de Comandos:**
- Proporciona los comandos necesarios para crear una nueva rama llamada feature-xyz, cambiar a esa rama, y luego fusionarla con la rama main.
    git branch feature-xyz
    git checkout feature-xyz
    # Realizar cambios y commits en la rama feature-xyz
    git checkout main
    git merge feature-xyz


1. **Pregunta Teórica:**
- ¿Qué es un "merge conflict" y cómo se resuelve?
    Merge Conflict: Ocurre cuando Git no puede fusionar automáticamente cambios en una rama porque los cambios conflictúan. Se resuelve editando manualmente los archivos en conflicto para decidir qué cambios conservar y luego realizando un commit.

1. **Pregunta de Comandos:**
- ¿Cuál es el comando para visualizar el estado actual del repositorio en Git?
    git status


1. **Pregunta Teórica:**
- Explica la diferencia entre git pull y git fetch.
    git pull: Obtiene cambios del repositorio remoto y los fusiona automáticamente en la rama actual.
    git fetch: Obtiene cambios del repositorio remoto pero no los fusiona automáticamente. Permite revisar los cambios antes de fusionarlos manualmente.

1. **Pregunta de Comandos:**
- ¿Cuál es el comando para revertir el último commit en Git?
    git revert HEAD


1. **Pregunta Teórica:**
- ¿Qué es un "remote repository" y cómo se configura en Git?
    Remote Repository: Es una copia del repositorio almacenada en un servidor remoto. Permite la colaboración entre desarrolladores. Se configura con git remote add <nombre> <url>.
    * git remote add origin https://github.com/usuario/repositorio.git


1.  **Pregunta de Comandos:**
- Proporciona los comandos para añadir todos los cambios en los archivos al staging area y luego realizar un commit con el mensaje "Initial commit".
    git add .
    git commit -m "Initial commit"