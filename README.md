# Proyecto MIAD
## Director de proyecto: Olmer García
### Presenta: Karolina Ladino Puerto

### ⚒️ Construcción de la imagen de Docker (Jetson Nano)

El Dockerfile se construye a partir de la imagen base de Jetson de Stereolabs. 
En [https://hub.docker.com/r/stereolabs/zed/](https://hub.docker.com/r/stereolabs/zed/) se pueden consultar todas las disponibles.

[Dockerfile]()

### 🏗️ Compilar los paquetes

Actualmente los paquetes quedan compilados en la maquina host, aunque su compilación se ejecute dentro del contenedor.

Para correr la compilación, dentro de la carpeta donde se desee dejar los compilados, ejecutar:

```bash
docker run -it --net=host --privileged --gpus all -v $(pwd)/build/:/usr/local/zed/ros2ws/build -v $(pwd)/install/:/usr/local/zed/ros2ws/install karozedfoxy
```

Esto abrirá una consola dentro del contenedor.

Dentro de ella ejecutar:

```bash
compile.sh
```

<aside>
⚠️ Si ya se ejecutó previamente y se instalaron paquetes diferentes, es posible que sea necesario reiniciar la compilación.

</aside>

Para correr el visualizador, ejecutar el contenedor con:

```bash
docker run -it --net=host --privileged --gpus all \
        -v $(pwd)/build/:/usr/local/zed/ros2ws/build \
        -v $(pwd)/install/:/usr/local/zed/ros2ws/install \
        -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
jetsonkaro
```

Dentro del contenedor ejecutar:
