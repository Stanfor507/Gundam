Estudiante
Jone Van Stan
8-952-2284

GUNDAM_RX78

Entre los requisitos tenemos 
Los Paquetes de ROS para robots de GUNDAM 

original: https://github.com/gundam-global-challenge/gundam_robot.git

![GUNDAM Gazebo Simulation](imgs/gundam_AKG.jpg)

Se Utilizo el sistema operativo Ubuntu 18.04.6. ROS el cual es un software que nos provee la libertad de hacer multiples cosas relacionada con robotica,  debe estar instalado y el sistema operativo configurado. Puede ver los pasos de instalación y configuración en:
```
 http://wiki.ros.org/melodic/Installation/Ubuntu
```

----------------------
Con el ROS debidamente implementado, seguí las instrucciones en los archivos GUNDAM, con la ayuda de un archivo alojado en Github.

```
$ mkdir -p catkin_ws/src
$ cd catkin_ws
$ wstool init src
$ wstool merge -t src https://raw.githubusercontent.com/gundam-global-challenge/gundam_robot/.gundam.rosinstall
$ wstool update -t src
$ source /opt/ros/$ROS_DISTRO/setup.bash
$ rosdep install -y -r --from-paths src --ignore-src
$ catkin build
$ source devel/setup.bash
```

URDF

Seguimos poniendo la línea de comando para ejecutar el archivo URDF de GUNDAM 
 en rviz, puedes usar `display.launch`.
```
$ roslaunch gundam_rx78_description display.launch
```

simulación 
============================
Ejecutando la simulación de la torre de observación, gazebo.
```
$ roslaunch gundam_rx78_gazebo gundam_rx78_world.launch
```

Para ajustar los ángulos de las articulaciones
------------

Puede realizar una caminata tipo "robot" en la simulación

```
$ roslaunch gundam_rx78_gazebo gundam_rx78_walk.launch
```

```
# aqui realiza un paso
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/step.csv
# aqui Camina hacia adelante
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-forward.csv
# aqui Camina hacia atráshttps://youtu.be/hVrQR7l3-CA
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-backward.csv
# aqui Camina a la derecha
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-to-right.csv
# aqui Camina a la izquierda
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/walk-to-left.csv
# aqui Voltea a la derecha
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/turn-right.csv
# aqui Voltea a la izquierda
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/turn-left.csv
```

```
# Aqui levanta los brazos y camina
$ rosrun gundam_rx78_control joint_trajectory_client_csv.py `rospack find gundam_rx78_control`/sample/csv/up.csv


![Simulation](imgs/gundamAKG.gif)

Tenga en cuenta que actualmente existen varias limitaciones en esta simulación, solo hay un controlador de posición, entre otros.

También se pueden encontrar ejemplos de archivos de control de movimiento  en la carpeta `gundam_rx78_control/sample`.

joint_trajectory_client_csv.py
----------------------

Usando el control de Gundam con joint_tajectory_client_csv.py e importando un archivo .csv

Utiliza los patrones declarados en el archivo para simular el movimiento del gundam según los valores angulares de cada componente.




