# multi_lslidar_c16

ROS driver for multiple lslidar_c16

## 安装
 - 建立工作空间并拷贝这个库
   ```Shell
   mkdir -p ros_ws/src
   cd ros_ws/src
   git clone https://github.com/shangjie-li/multi_lslidar_c16.git
   cd ..
   catkin_make
   ```

## 参数配置
 - 修改`lslidar_c16_multi/lslidar_c16_decoder/launch/lslidar_c16.launch`
   ```Shell
	<launch>
	<group ns="ls_left">
	  <arg name="device_ip" default="192.168.1.201" />
	  <arg name="msop_port" default="2368" />
	  <arg name="difop_port" default="2369" />
	  <arg name="return_mode" default="1" />
	  <arg name="time_synchronization" default="true" />
	  <node pkg="lslidar_c16_driver" type="lslidar_c16_driver_node" name="lslidar_c16_driver_node" output="screen">
	    <param name="device_ip" value="$(arg device_ip)" />
	    <param name="msop_port" value="$(arg msop_port)" />
	    <param name="difop_port" value="$(arg difop_port)"/>
	    <param name="frame_id" value="laser_link_left"/>
	    <param name="add_multicast" value="false"/>
	    <param name="group_ip" value="224.1.1.1"/>
	    <param name="rpm" value="600"/>
	    <param name="return_mode" value="$(arg return_mode)"/>
	    <param name="time_synchronization" value="$(arg time_synchronization)"/>
	  </node>
	  <node pkg="lslidar_c16_decoder" type="lslidar_c16_decoder_node" name="lslidar_c16_decoder_node" output="screen">
	    <param name="calibration_file" value="$(find lslidar_c16_decoder)/params/lslidar_c16_db.yaml" />
	    <param name="min_range" value="0.15"/>
	    <param name="max_range" value="150.0"/>
	    <param name="cbMethod" value="true"/>
	    <param name="config_vert" value="true"/>
	    <param name="print_vert" value="false"/>
	    <param name="return_mode" value="$(arg return_mode)"/>
	    <param name="config_vert_file" value="false"/>
	    <param name="distance_unit" value="0.25"/>
	    <param name="time_synchronization" value="$(arg time_synchronization)"/>
	    <param name="scan_start_angle" value="0.0"/>
	    <param name="scan_end_angle" value="36000.0"/>
	  </node>
	</group>

	<group ns="ls_right">
	  <arg name="device_ip" default="192.168.1.202" />
	  <arg name="msop_port" default="2370" />
	  <arg name="difop_port" default="2371" />
	  <arg name="return_mode" default="1" />
	  <arg name="time_synchronization" default="true" />
	  <node pkg="lslidar_c16_driver" type="lslidar_c16_driver_node" name="lslidar_c16_driver_node" output="screen">
	    <param name="device_ip" value="$(arg device_ip)" />
	    <param name="msop_port" value="$(arg msop_port)" />
	    <param name="difop_port" value="$(arg difop_port)"/>
	    <param name="frame_id" value="laser_link_right"/>
	    <param name="add_multicast" value="false"/>
	    <param name="group_ip" value="224.1.1.1"/>
	    <param name="rpm" value="600"/>
	    <param name="return_mode" value="$(arg return_mode)"/>
	    <param name="time_synchronization" value="$(arg time_synchronization)"/>
	  </node>
	  <node pkg="lslidar_c16_decoder" type="lslidar_c16_decoder_node" name="lslidar_c16_decoder_node" output="screen">
	    <param name="calibration_file" value="$(find lslidar_c16_decoder)/params/lslidar_c16_db.yaml" />
	    <param name="min_range" value="0.15"/>
	    <param name="max_range" value="150.0"/>
	    <param name="cbMethod" value="true"/>
	    <param name="config_vert" value="true"/>
	    <param name="print_vert" value="false"/>
	    <param name="return_mode" value="$(arg return_mode)"/>
	    <param name="config_vert_file" value="false"/>
	    <param name="distance_unit" value="0.25"/>
	    <param name="time_synchronization" value="$(arg time_synchronization)"/>
	    <param name="scan_start_angle" value="0.0"/>
	    <param name="scan_end_angle" value="36000.0"/>
	  </node>
	</group>
	</launch>
   ```
## 运行
 - 启动多个激光雷达
   ```Shell
   roslaunch lslidar_c16_decoder lslidar_c16.launch
   ```

## 案例
 - 机械安装
    - 针对C16-121B-3120110001，安装在车身左侧，雷达尾部端子朝上。
    - 针对C16-121B-3020060009，安装在车身右侧，雷达尾部端子朝上。
 - 建立局域网
    - 针对C16-121B-3120110001，IP：192.168.1.201，Data Port：2368，Device Port：2369，对应的电脑静态IP：192.168.1.102。
    - 针对C16-121B-3020060009，IP：192.168.1.202，Data Port：2370，Device Port：2371，对应的电脑静态IP：192.168.1.102。
 - 连接计算机和多个激光雷达
    - 计算机的以太网口“Ethernet (enp2s0)”连接交换机“上联口”，交换机的任意2个“Poe端口”分别连接2个激光雷达的接线盒，建立以太网“LeiShen_switch”。


