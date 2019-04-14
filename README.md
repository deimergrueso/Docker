# Docker

### ## COMANDOS RAPIDOS DE DOCKER

  	  | Basicos de ejecución  |

**Containers en ejecución**

`$docker ps`

Containers existentes

`$docker ps -a`

**Ejecución de contenedores**
`$docker run "nombre_del_contenedor"`

**Asignación de nombre al contenedor**

`$docker run --name "nombre_del_contenedor" "nombre_imagen"`

Ejemplo

`$docker run --name mi_contenedor ubuntu`

**Cambio de nombres del contenedor**

`$docker rename "nombre_del_contenedor" "nombre_nuevo"`

**Ejecutar contenedor como demonio oculto**

`$docker run -d --name "nombre_del_contenedor" nginx`

**Eliminar contenedores**

`$docker rm "nombre_del_contenedor"`

Eliminar varios todos los contenedores:

`docker rm $(docker ps -aq)`

**Entrar en modo interactivo a un contenedor**

`$docker run -it --name prueba ubuntu`

**Entrar en modo interactivo a un contenedor en ejecución**

`docker exec -it prueba /bin/bash`



	| Basicos de Networking  |
