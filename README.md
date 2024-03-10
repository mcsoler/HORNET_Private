##HORNET - Nodo IOTA
Hornet es un software de nodo diseñado para ser ligero y con una configuración y operación relativamente sencilla, está escrito en Go y optimizado para el ecosistema de IOTA. IOTA es una tecnología de contabilidad distribuida (DLT, por sus siglas en inglés) que se diferencia de las blockchains tradicionales por su estructura llamada Tangle, una red de transacciones que permite que el sistema escale de manera más eficiente y elimine las tarifas por transacción, haciendo posible la transferencia de datos y valores sin costos.
Los nodos Hornet en la red de IOTA juegan un papel crucial en la validación y confirmación de transacciones. Cada nodo contribuye al consenso de la red al aprobar dos transacciones previas cada vez que desea realizar una nueva transacción. Este mecanismo de validación colectiva asegura la seguridad y la finalidad de las transacciones en el Tangle.

##Al ejecutar su nodo privado, tiene los siguientes beneficios:
•	Hornet está diseñado para ser ligero, lo que significa que consume menos recursos de hardware en comparación con otras implementaciones de nodos. 
•	Hornet está diseñado para manejar un alto volumen de transacciones, lo que es crucial para la escalabilidad de la red IOTA. Esto asegura que la red pueda procesar transacciones de manera eficiente, incluso durante períodos de alta demanda.
•	La seguridad es una prioridad en el diseño de Hornet, con varias características implementadas para proteger contra ataques y asegurar la integridad de la red.
•	Los nodos de Hornet participan en el mecanismo de consenso de IOTA, validando transacciones y asegurando que solo las transacciones legítimas sean confirmadas en el Tangle.
•	Hornet se mantiene al día con las últimas actualizaciones y características de la red IOTA, asegurando compatibilidad con nuevas funcionalidades y mejoras en el protocolo.


##Requerimientos del sistema para la instalación del nodo privado Hornet.
##Para manejar una tasa potencialmente alta de bloques por segundo, los nodos necesitan suficiente potencia computacional para funcionar de manera confiable y deben tener las especificaciones mínimas:
•	4 cores or 4 vCPU.
•	8 GB RAM.
•	SSD storage.
•	A public IP address.

##La cantidad de almacenamiento que necesita dependerá de si planea eliminar datos antiguos de su base de datos local y con qué frecuencia.
•	Una versión reciente de Docker Enterprise o Community Edition
1. Ejecute el siguiente comando para desinstalar todos los paquetes conflictivos:
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
2. Instale docker usando el repositorio con los siguientes comandos:

sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

3. Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

4. Instale los paquetes de docker con el siguiente comando:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

5. Verifique que docker engine este instalado correctamente con el siguiente comando:
docker --version
Docker version 25.0.3, build 4debf41

•	Docker Compose CLI plugin.
1. Instale docker compose plugin usando el repositorio con los siguientes comandos:
sudo apt-get update
sudo apt-get install docker-compose-plugin
2. Verifique la versión de docker-compose instalada
docker compose version
Docker Compose version v2.24.5
 
•	curl
1. Instale curl usando el repositorio con los siguientes comandos:
apt-get install ca-certificates curl gnupg
curl --version
•       rustc
1. Instale rustc usando el repositorio con los siguientes comandos:
apt  install rustc
rustc --version tc 1.75.0 (82e1608df 2023-12-21) (built from a source tarball)

##HORNET expone diferentes funcionalidades en diferentes puertos y hay que configurarlos en el firewall:
•	15600 TCP: puerto del protocolo Gossip.
•	14626 UDP: puerto de emparejamiento automático (opcional).
•	14265 TCP: puerto API REST HTTP (opcional).
•	80 TCP: utilizado para HTTP
•	443 TCP - utilizado para HTTPS
•	4000 TCP/UDP: utilizado para wasp gossip

##Una vez cumplidos los requisitos previos, procedemos a instalar el software del nodo Hornet, en este caso vamos a utilizar un servidor con un sistema operativo Ubuntu 20.04.6 LTS.
1.	Clonamos el repositorio que contiene el software del nodo Hornet en GitHub con el siguiente comando:
gitclone https://github.com/iotaledger/hornet.git
2.	Ingresamos al directorio private_tangle y ejecutamos el script de shell ./bootstrap.sh build, esto iniciará los contenedores docker con las imágenes que contienen la Tangle privada creando la captura de génesis y los archivos requeridos.
3.	Ejecutamos el script Shell:
./run.sh para ejecutar dos nodos.
./run.sh 3 para ejecutar tres nodos.
./run.sh 4 para ejecutar cuatro nodos.

4. ./cleanup.sh para limpiar todos los archivos generados y empezar de nuevo.

##Los nodos serán entonces accesibles a través de estos puertos:

- inx-faucet:
    - Faucet: http://localhost:8091
    - pprof: http://localhost:6024/debug/pprof
- Hornet-1:
    - API: http://localhost:14265
    - External Peering: 15611/tcp
    - Dashboard: http://localhost:8011 (username: admin, password: admin)
    - Prometheus: http://localhost:9311/metrics
    - pprof: http://localhost:6011/debug/pprof
    - inx: localhost:9011
- Hornet-2:
    - API: http://localhost:14266
    - External Peering: 15612/tcp
    - Dashboard: http://localhost:8012 (username: admin, password: admin)
    - Prometheus: http://localhost:9312/metrics
    - pprof: http://localhost:6012/debug/pprof
    - inx: localhost:9012
- Hornet-3:
    - API: http://localhost:14267
    - External Peering: 15613/tcp
    - Dashboard: http://localhost:8013 (username: admin, password: admin)
    - Prometheus: http://localhost:9313/metrics
    - pprof: http://localhost:6013/debug/pprof
    - inx: localhost:9013
- Hornet-4:
    - API: http://localhost:14268
    - External Peering: 15614/tcp
    - Dashboard: http://localhost:8014 (username: admin, password: admin)
    - Prometheus: http://localhost:9314/metrics
    - pprof: http://localhost:6014/debug/pprof
    - inx: localhost:9014
- inx-coordinator:
    - pprof: http://localhost:6021/debug/pprof
- inx-indexer:
    - pprof: http://localhost:6022/debug/pprof
    - Prometheus: http://localhost:9322/metrics
- inx-mqtt:
    - pprof: http://localhost:6023/debug/pprof
    - Prometheus: http://localhost:9323/metrics
- inx-participation:
    - pprof: http://localhost:6025/debug/pprof
- inx-spammer:
    - pprof: http://localhost:6026/debug/pprof
    - Prometheus: http://localhost:9326/metrics
- inx-poi:
    - pprof: http://localhost:6027/debug/pprof
- inx-dashboard-1:
    - pprof: http://localhost:6031/debug/pprof
    - Prometheus: http://localhost:9331/metrics
- inx-dashboard-2:
    - pprof: http://localhost:6032/debug/pprof
    - Prometheus: http://localhost:9332/metrics
- inx-dashboard-3:
    - pprof: http://localhost:6033/debug/pprof
    - Prometheus: http://localhost:9333/metrics
- inx-dashboard-4:
    - pprof: http://localhost:6034/debug/pprof
    - Prometheus: http://localhost:9334/metrics

## Inicie el coordinador en caso de falla.
El contenedor `inx-coordinator` siempre comienza junto con los otros contenedores si ejecuta el comando `./run.sh`.
Puede suceder que el inicio del nodo tarde más de lo esperado debido a bases de datos más grandes o máquinas host lentas. En eso >

Si desea reiniciar el `inx-coordinator` por separado, ejecute el siguiente comando:
```sh
docker compose start inx-coordinator
```
