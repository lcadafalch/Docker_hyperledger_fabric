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

```yaml
image: hyperledger/fabric-orderer:2.3
```
Especifica la imagen de Docker que se utilizará para el ordenador. En este caso, se utiliza la imagen hyperledger/fabric-orderer de la versión 2.3.
```yaml
environment:
  - FABRIC_LOGGING_SPEC=INFO
  - ORDERER_GENERAL_LISTENADDRESS=0.0.0.0
  - ORDERER_GENERAL_GENESISMETHOD=file
  - ORDERER_GENERAL_GENESISFILE=/var/hyperledger/orderer/orderer.genesis.block
  - ORDERER_GENERAL_LOCALMSPID=OrdererMSP
  - ORDERER_GENERAL_LOCALMSPDIR=/var/hyperledger/orderer/msp
  - ORDERER_GENERAL_TLS_ENABLED=true
  - ORDERER_GENERAL_TLS_PRIVATEKEY=/var/hyperledger/orderer/tls/server.key
  - ORDERER_GENERAL_TLS_CERTIFICATE=/var/hyperledger/orderer/tls/server.crt
  - ORDERER_GENERAL_TLS_ROOTCAS=[/var/hyperledger/orderer/tls/ca.crt]
```
Establece las variables de entorno para la configuración del ordenador de Hyperledger Fabric. Estas variables incluyen opciones de registro, configuración de red, rutas de archivos y configuración TLS.
```yaml
working_dir: /opt/gopath/src/github.com/hyperledger/fabric/orderer
```
Establece el directorio de trabajo dentro del contenedor donde se encuentra el código fuente y los archivos de configuración del ordenador.
```yaml
command: orderer
```
Especifica el comando que se ejecutará cuando se inicie el contenedor. En este caso, se ejecutará el comando orderer.
```yaml
volumes:
  - ./channel-artifacts/genesis.block:/var/hyperledger/orderer/orderer.genesis.block
  - ./crypto-config/ordererOrganizations/example.com/orderers/orderer.example.com/msp:/var/hyperledger/orderer/msp
  - ./crypto-config/ordererOrganizations/example.com/orderers/orderer.example.com/tls:/var/hyperledger/orderer/tls
```
Configura los volúmenes de Docker para vincular los archivos necesarios desde tu sistema de archivos host al sistema de archivos del contenedor. En este caso, se vinculan los archivos genesis.block, las claves y los certificados necesarios para el ordenador.

```yaml
ports:
  - 7050:7050
```
Mapea el puerto 7050 del contenedor al puerto 7050 de tu máquina host, permitiendo así acceder al ordenador de Hyperledger Fabric desde el exterior.
```yaml
networks:
  - fabric
```
Asigna el servicio orderer.example.com a la red fabric que se definió anteriormente.
Las líneas siguientes siguen una estructura similar para configurar los servicios de los nodos adicionales (peer0.org1.example.com, peer1.org1.example.com, etc.). Puedes agregar más servicios de nodos según sea necesario.

Recuerda que este es solo un ejemplo básico y hay muchas más configuraciones y opciones disponibles en Docker Compose para personalizar tu entorno de Hyperledger Fabric según tus necesidades específicas.
