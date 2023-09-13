# Dummy Controller

## Özet 

Path Planning algoritmalarını test etmek için geliştirilmiş kontrolcüdür.
**Kinematic Bicycle Model**'e dayalı olarak throotle kontrolcüsü olarak
**PID** ve steer kontrolcüsü olarak **Pure Pursuit** kullanılmıştır.

config/params.yaml dosyasından parametreleri tune edebilirsiniz.

Simülasyonu başlattıktan sonra araç son noktaya `goal_threshold_` kadar yakın bir noktada duracaktır.

## Input & Output

### Input Topics

| Name                                  | Type                                  | Description                                               |
| --------------------------------------| --------------------------------------| --------------------------------------------------------- |
| `/carla/ego_vehicle/waypoints`        | nav_msgs::msg::Path                   | Carla simulation waypoint path                            |
| `/carla/ego_vehicle/odometry`         | nav_msgs/msg/Odometry                 | Carla simulation ego vehicle odometry                     |
| `/carla/ego_vehicle/vehicle_status`   | carla_msgs/msg/CarlaEgoVehicleStatus  | Carla simulation ego vehicle status                       |

### Output Topics

| Name                                     | Type                                    | Description                                               |
| -----------------------------------------| ----------------------------------------| --------------------------------------------------------- |
| `/carla/ego_vehicle/vehicle_control_cmd` | carla_msgs::msg::CarlaEgoVehicleControl | Ego vehicle control over steer, throttle and brake        |

## Kurulum

```bash
cd ~/colcon_ws/src
git clone git@github.com:BMC-VURAN-OTONOM/dummy_controller.git -b vuran-dev
cd ..
colcon build --packages-select dummy_controller
```

## Dependencies

### Packages
- map_visualizer
- ros-bridge

### Messages
- carla_msgs
- nav_msgs
- geometry_msgs
- tf2

## Nasıl Çalıştırılır

### Sadece paket çalıştırma
```bash
ros2 launch dummy_controller dummy_controller.py
```

### Simülasyon ile çalıştırma

```bash
# terminal açın ve CARLA simulasyonunu başlatın.
cd /opt/carla-simulator && bash CarlaUE4.sh
```
```bash
# yeni bir terminal açıp CARLA-ROS bridge ile ego vehicle'ı spawn edin.
ros2 launch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch.py
```
```bash
# [OPTIONAL] hd map görselleştirmek için osm_visualizer node'unu başlatın.
ros2 run map_visualizer osm_visualizer
```
```bash
# [OPTIONAL] RViz'i açın.
rviz2
```
```bash
# dummy_controller'ı başlatın.
ros2 launch dummy_controller dummy_controller.py
```
```bash
# hemen ardından path publish eden carla_waypoint_publisher'ı başlatın.
ros2 launch carla_waypoint_publisher carla_waypoint_publisher.launch.py
```

## Referanslar
* [Algorithms for Automated Driving](https://thomasfermi.github.io/Algorithms-for-Automated-Driving/Control/ControlOverview.html)
