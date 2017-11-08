 
# Comandos git más usados:

1) Clonar repositorio, copia un repositorio desde una dirección remota (URL) en la maquina local.

```{r, engine='bash'}
git clone {url}
```

Ejemplo:

```{r, engine='bash'}
git clone https://github.com/numpy/numpy.git
```

Este comando clona (copia) el repositorio _numpy_ localmente.

2) Listar los commits en un repositorio:

```{r, engine='bash'}
git log
```

** Nota: Este comando es importante que se ejecute desde la carpeta en la cual se creó o clonó el repositorio.

3) Añadir cambios para próximo commit:

```{r, engine='bash'}
git add {FILENAME}
```

Ejemplo:

```{r, engine='bash'}
git add ejercicio.py
```

También se pueden añadir multiples archivos poniendo de esta forma:

```{r, engine='bash'}
git add ejercicio.py ejercicio2.py imagenes/logo.png
```
En el ejemplo anterior se agregaron 3 archivos:

- ejercicio.py (en la misma carpeta)
- ejercicio2.py (en la misma carpeta)
- logon.png (que se encuentra en la carpeta imagenes dentro de la actual carpeta)

4) Consultar el estado 

```{r, engine='bash'}
git status 
```

Este comando lista el estado actual localmente, nos indica que cambios hemos hecho, que archivos están siendo manejados por git y cuales no, cuales han sido añadidos para un futuro commit y cuales no.

5) Commit

El comando _commit_ es utilizado para crear un nuevo commit basado en los cambios que se han agregado previamente con el comando _add_.

```{r, engine='bash'}
git commit -m {FRASE_COMMIT} 
```

Ejemplo:

```{r, engine='bash'}
git commit -m "Agrega la solucion al ejercicio de maximos (ejercicio.py)" 
```

La frase que se indica en el commit es muy importante para entender que cambios se han agregado, en idioma español conviene comenzar la frase con un verbo en tiempo indicativo presente, por ejemplo "Agrega", "Elimina", "Arregla", "Modifica", etc. En idioma inglés se suele usar un verbo infinitivo por ejemplo "Add", "Delete", "Fix" o "Modify", etc. 
En idioma español conviene no usar acentos ni caracteres especiales para evitar potenciales problemas de encoding.

6) Branch

Este comando nos indica cual es la _rama_ o _branch_ en la cual estamos trabajando. La rama por defecto que tienen todos los repositorios es _master_ pero es posible crear nuevas ramas.

```{r, engine='bash'}
git branch
```

7) Consultar repositorios remotos

Git soporta trabajar con múltiples repositorios remotos simultáneamente por lo cual cuenta con un comando que nos permite listar los repos.

```{r, engine='bash'}
git remote
```

Si se le agrega la opción "-v" nos indica la URL de cada repositorio:

```{r, engine='bash'}
git remote -v
```

8) Push

Una vez que tenemos nuestros cambios en un commit podemos enviar los mismos a un repositorio remoto, para eso tenemos que saber a que repositorio y a que branch (o rama) en ese repositorio queremos subirlos.

```{r, engine='bash'}
git push {REPOSITORIO} {BRANCH}
```

Ejemplo:

```{r, engine='bash'}
git push origin master
```

Subirá los cambios en el repositorio que tenemos con el nombre _origin_ en la branch (rama) que tenemos con el nombre _master_

Este comando nos puede dar un error si existe un conflicto, por ejemplo que alguien haya subido un cambio desde el último commit que nos bajamos hasta el momento en que hacemos el push. En ese caso debemos bajarnos los cambios y resolver los conflictos en caso de que existan.

9) Bajar cambios del repositorio

Para bajar todos los cambios desde el repositorio en nuestro local podemos usar el comando _fetch_, este comando baja los cambios para que luego los integremos en nuestra branch.

```{r, engine='bash'}
git fetch {REPOSITORIO} {BRANCH}
```

Ejemplo: 

```{r, engine='bash'}
git fetch origin master
```

Recupera todos los cambios desde el repositorio _origin_ y la branch _master_, si obviamos el parámetro _BRANCH_ el comando traerá los cambios de todas las ramas del repositorio y por otro lado si obviamos el parámetro _REPOSITORIO_ traerá los cambios de todos los repos.

10) Integrar los cambios

Una vez que los cambios están localmente en nuestro cliente Git, el paso siguiente es integrarlos con nuestros cambios. Para eso existen dos comandos _merge_ y _rebase_ (recomendado). Merge crea una nuevo commit basado en ambos cambios, rebase por su parte agrega nuestro cambios por encima de los cambios descargados, está última opción es recomendable dado que mantiene la historia en el repositorio consistente.

```{r, engine='bash'}
git rebase {REPOSITORIO}/{BRANCH}
```

Al comando _rebase_ es necesario indicarle el repositorio y el branch con el que queremos integrar.

Si existe algún conflicto durante el rebase que debemos resolver entonces el comando fallará y nos indicará que el rebase no finalizó. Lo que debemos hacer en ese caso es lo siguiente:

- Usar el comando _status_ (indicado en 4) para visualizar cuales son los archivos en conflicto.
- Abrir cada uno de los archivos y buscamos los conflictos, git indica los conflictos usando una sintaxis que nos permite visualizar cuales son nuestros cambios en el archivo y cuales son los que estaban en el HEAD (es decir los que descargamos.
- Resolver los conflictos, es decir decidir cual es el cambio que va, el nuestro, el que descargamos o una combinación de ambos.
- Agregar los archivos en conflicto que hemos reparado usando el comando _add_ (indicado en 3).
- Una vez que se resolvieron todos los conflictos indicarle a git que puede continuar el rebase con el comando:

```{r, engine='bash'}
git rebase --continue
```

Si por cualquier motivo queremos suspender el rebase, en otras palabras dejar nuestro repositorio con nuestros cambios locales sin integrarlos con lo descargado, podemos indicarle a git que aborte el rebase

```{r, engine='bash'}
git rebase --abort
```

11) Crear un nuevo branch

Para crear un nuevo branch local podemos usar el comando _checkout_

```{r, engine='bash'}
git checkout {BRANCHNAME}
```

Ejemplo:

```{r, engine='bash'}
git checkout otrobranch
```

Creará un nuevo branch que inicializado con los cambios presentes en el branch actual. Luego si se realiza un push utilizando este nuevo branch, el nuevo branch será incluído en el repositorio remoto.
