# Docker_hyperledger_fabric
Descripción del Yaml para la creacrión de nodos con Docker en hyperledger Fabric
```yaml
version: '2'
```
Esto establece la versión del formato de archivo docker-compose. En este caso, utilizamos la versión 2.

```yaml
networks:
  fabric:
```
Define una red llamada fabric que se utilizará para la comunicación entre los servicios de Hyperledger Fabric.


```yaml
services:
  orderer.example.com:
```
Define un servicio llamado orderer.example.com que representa el ordenador (orderer) de Hyperledger Fabric.

```yaml
container_name: orderer.example.com
```
Establece el nombre del contenedor como orderer.example.com.
