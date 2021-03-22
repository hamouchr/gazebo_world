# gazebo_world

## Chargement d'un monde dans gazebo

roslaunch my_worlds world1.launch

ou bien 

roslaunch my_worlds world1.launch world:=world02
roslaunch my_worlds world1.launch world:=world03

## Chargement d'un modele de robot dans gazebo 

 <arg name="model" default="m2wr"/>
  <arg name="x" default="0.0"/>
  <arg name="y" default="0.0"/>
  <arg name="z" default="0.0"/>
  
<param name="robot_description" command="$(find xacro)/xacro --inorder $(find turtlebot3_description)/urdf/turtlebot3_$(arg model).urdf.xacro" />

<node name="mybot_spawn" pkg="gazebo_ros" type="spawn_model" output="screen"
          args="-urdf -param robot_description -model m2wr -x $(arg x) -y $(arg y) -z $(arg z)" />


## send vers RVIZ
<!-- send fake joint values -->
  <node name="joint_state_publisher" pkg="joint_state_publisher" type="joint_state_publisher">
    <param name="use_gui" value="true"/>
  </node>
  
  
  <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" output="screen">
    <param name="publish_frequency" type="double" value="50.0" />
  </node>

  <node name="rviz" pkg="rviz" type="rviz" args="-d $(find turtlebot3_fake)/rviz/turtlebot3_fake.rviz"/>
