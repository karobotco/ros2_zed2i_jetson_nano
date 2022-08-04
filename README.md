# Proyecto MIAD
## Director de proyecto: Olmer García
### Presenta: Karolina Ladino Puerto

------
## 🦊 Foxy en Docker - Desktop

### ⚒️ Construcción de la imagen de Docker (Linux Desktop)

El Dockerfile se construye a partir de la imagen base de Stereolabs. 
En [https://hub.docker.com/r/stereolabs/zed/](https://hub.docker.com/r/stereolabs/zed/) se pueden consultar todas las disponibles.

[Dockerfile]()

Para construir la imagen se debe ejecutar el siguiente comando en la carpeta donde se encuentre el Dockerfile:

```bash
docker build . -t karozedfoxy
```

La compilación tomará varios minutos. ⌚

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
⚠️ Si ya se ejecutó previamente y se instalaron paquetes diferentes, es posible que sea necesario reiniciar la compilación.

---------------------
## 🐢 Eloquent en Docker - Desktop

### ⚒️ Construcción de la imagen de Docker (Linux Desktop)

El Dockerfile se construye a partir de la imagen base de Ubuntu 18.04 LTS de Stereolabs. 

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

⚠️ Si ya se ejecutó previamente y se instalaron paquetes diferentes, es posible que sea necesario reiniciar la compilación.

Para correr el visualizador, ejecutar el contenedor con:
```bash
docker run -it --net=host --privileged --gpus all \
        -v $(pwd)/build/:/usr/local/zed/ros2ws/build \
        -v $(pwd)/install/:/usr/local/zed/ros2ws/install \
        -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
jetsonkaro
```
```bash
Dentro del contenedor ejecutar:
source install/local_setup.bash
ros2 launch zed_display_rviz2 display_zed2.launch.py
```
-------------

## 🐢 Eloquent en Docker - Jetson Nano

### ⚒️ Construcción de la imagen de Docker (Jetson Nano)

El Dockerfile se construye a partir de la imagen base de Jetson de Stereolabs. 

En [https://hub.docker.com/r/stereolabs/zed/](https://hub.docker.com/r/stereolabs/zed/) se pueden consultar todas las disponibles.

[Dockerfile]()

Se corre el contenedor con el siguiente comando:

```bash
docker run -it --net=host --privileged --gpus all \
        -v $(pwd)/build/:/usr/local/zed/ros2ws/build \
        -v $(pwd)/install/:/usr/local/zed/ros2ws/install \
        -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
jetsonkaro
```

Se ejecuta dentro del contenedor:
```bash
run_zednode
```

----------------

# 🎥 ZED

## 🐢 Ejecutar el nodo de ZED (Jetson Nano)

El nodo de ZED se ejecuta en la maquina a la que está conectada **físicamente** la cámara ZED, en este caso la Jetson Nano.

Para ejecutarlo, ejecutar dentro del contenedor:
```bash
run_zednode
```

---------------

# 👁️ RVIZ

## 🦊 Ejecutar rviz (Desktop Foxy)

Para ejecutar rviz cuando ya hay un nodo corriendo, hay que modificar el ejemplo para especificar que no se debe autoiniciar el nodo.

Antes de ejecutar el contenedor, ejecutar:

```bash
xhost +si:localuser:root
```

Luego, correr el contenedor corriendo:

```bash
docker run -it --net=host --privileged --gpus all \
	-v $(pwd)/build/:/usr/local/zed/ros2ws/build \
	-v $(pwd)/install/:/usr/local/zed/ros2ws/install \
	-e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
karozedfoxy
```

Para ejecutarlo, ejecutar dentro del contenedor:

```bash
source install/local_setup.bash
ros2 launch zed_display_rviz2 display_zed2i.launch.py
```

-------------

## 🐢 Ejecutar rviz (Desktop Eloquent)

Para ejecutar rviz cuando ya hay un nodo corriendo, hay que modificar el ejemplo para especificar que no se debe autoiniciar el nodo.

Antes de ejecutar el contenedor, ejecutar:

```bash
xhost +si:localuser:root
```

Luego, correr el contenedor corriendo:

```bash
docker run -it --net=host --privileged --gpus all \
        -v $(pwd)/build/:/usr/local/zed/ros2ws/build \
        -v $(pwd)/install/:/usr/local/zed/ros2ws/install \
        -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix \
jetsonkaro
```

Para ejecutarlo, ejecutar dentro del contenedor:
```bash
ros2 launch zed_display_rviz2 display_zed2.launch.py
```

![RViZ Screenshot](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10bf0473-9615-4e18-8b26-be20e005b318/Untitled.png)
