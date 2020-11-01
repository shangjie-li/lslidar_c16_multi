# 维护记录
## 2020.10.31
 - 安装激光雷达
   - 6008位于车身左侧，6009位于车身右侧，雷达尾部端子均朝上。
## 2020.11.01
 - 配置激光雷达IP
   - 6008的IP：192.168.1.201，Data Port：2368，device Port：2369，对应的电脑静态IP：192.168.1.102
   - 6009的IP：192.168.1.202，Data Port：2370，device Port：2371，对应的电脑静态IP：192.168.1.102
 - 连接激光雷达
   - 计算机的以太网口“Ethernet (enp2s0)”连接交换机“上联口”，交换机的任意2个“Poe端口”分别连接2个激光雷达的接线盒，建立以太网“LeiShen_switch”。
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
 - 启动
   ```Shell
   source devel/setup.bash
   roslaunch lslidar_c16_decoder lslidar_c16.launch
   ```
 - 记录rosbag
   `/home/seucat/ros_workspace/rosbag/2020-11-01/2020-11-01-16-03-12.bag`





