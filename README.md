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

**Abrir puertos de un contenedor**

`$docker run -d -p 80:80 --name server_web nginx`


	| Basicos de Datos  |

Crear la carpeta donde se va a almacenar los datos

```bash
mkdir mongodata
pwd
/home/deimergrueso/mongodata
```

Agragarla como volumen fijo a nuestro contenedor(la notación que indica el patch de montaje del volumen esta despues de los dos puntos)

`docker run --name mongodb -d -v /home/deimergrueso/mongodata:/data/db mongo`

Verificar que los datos estan siendo guardados fuera del contenedor

```bash
docker exec -it mongodb bash
mongo
use deimer
db.users.insert({"name": "Deimer"})
    WriteResult({ "nInserted" : 1 })
db.users.find()
  { "_id" : ObjectId("5cb3a76edea9a4451f789d44"), "name" : "Deimer" }
`
```

Eliminar el contenedor

`docker rm -f mongodb`

Generar el segundo contenedor asociado al volumen pre-existente

`docker run --name mongodbII -d -v /home/deimergrueso/mongodata:/data/db mongo``


```bash
docker exec -it mongodbII bash
mongo
use deimer
db.users.find()
  { "_id" : ObjectId("5cb3a76edea9a4451f789d44"), "name" : "Deimer" }
`
```
