# Docker

### ## COMANDOS RAPIDOS DE DOCKER

### ##  | Basicos de ejecución  |

**Containers en ejecución**

```bash
docker ps
```

Containers existentes

```bash
docker ps -a
```

**Ejecución de contenedores**

```bash
docker run "nombre_del_contenedor"
```

**Asignación de nombre al contenedor**

```bash
docker run --name "nombre_del_contenedor" "nombre_imagen"
```

Ejemplo

```bash
docker run --name mi_contenedor ubuntu
```

**Cambio de nombres del contenedor**

```bash
docker rename "nombre_del_contenedor" "nombre_nuevo"
```

**Ejecutar contenedor como demonio oculto**

```bash
docker run -d --name "nombre_del_contenedor" nginx
```

**Eliminar contenedores**

```bash
docker rm "nombre_del_contenedor"
```

Eliminar varios todos los contenedores:

```bash
docker rm $(docker ps -aq)
```

**Entrar en modo interactivo a un contenedor**

```bash
docker run -it --name prueba ubuntu
```

**Entrar en modo interactivo a un contenedor en ejecución**

```bash
docker exec -it prueba /bin/bash
```

### ##| Basicos de Networking  |

**Abrir puertos de un contenedor**

```bash
docker run -d -p 80:80 --name server_web nginx
```


### ##| Basicos de Datos  |

Crear la carpeta donde se va a almacenar los datos

```bash
mkdir mongodata
pwd
/home/deimergrueso/mongodata
```

Agragarla como volumen fijo a nuestro contenedor(la notación que indica el patch de montaje del volumen esta despues de los dos puntos)

```bash
docker run --name mongodb -d -v /home/deimergrueso/mongodata:/data/db mongo`
```

Verificar que los datos estan siendo guardados fuera del contenedor

```bash
docker exec -it mongodb bash
mongo
use deimer
db.users.insert({"name": "Deimer"})
    WriteResult({ "nInserted" : 1 })
db.users.find()
  { "_id" : ObjectId("5cb3a76edea9a4451f789d44"), "name" : "Deimer" }

```

Eliminar el contenedor

```bash
docker rm -f mongodb
```

Generar el segundo contenedor asociado al volumen pre-existente

```bash
docker run --name mongodbII -d -v /home/deimergrueso/mongodata:/data/db mongo
```

```bash
docker exec -it mongodbII bash
mongo
use deimer
db.users.find()
  { "_id" : ObjectId("5cb3a76edea9a4451f789d44"), "name" : "Deimer" }
```



** Visualizar los volumenes existentes**

```bash
docker volume ls
```

**Limpiar los volumes no utilizados por ningun contenedor**

```bash
docker volume prune
```

**Crear un volumen**

```bash
docker volume create datodb
```

**Montar el volumen**

```bash
docker run -d --name mongoIII --mount src=datodb,dst=/data/db mongo
docker exec -it mongoIII bash
mongo
use deimer
db.users.insert({"name": "Deimer"})
    WriteResult({ "nInserted" : 1 })
db.users.find()
  { "_id" : ObjectId("5cb3a76edea9a4451f789d44"), "name" : "Deimer" }

docker rm -f mongoIII 

docker run -d --name mongoIV --mount src=datodb,dst=/data/db mongo
docker exec -it mongoIV bash
mongo
db.users.find()
use deimer
db.users.find()
	{ "_id" : ObjectId("5cb50e83b510b6a7303ade1a"), "name" : "Deimer" }

```
