# MuSHR V4 build instructions (Draft).
##### Note: If you already have a [MuSHR](https://mushr.io/), you will be re-using a fair number of the components, so do not order the highlighted components from the BOM, as they represent the "overlapping components". Additionally, you may want to order the d455 if you don't have one and want to use that.

## [Bill of materials](https://docs.google.com/spreadsheets/d/12jod9aALWGB2n3a47guYzTRTLul8M2QtT9iCGtkBhws/edit?usp=sharing)

## Build steps:
The build steps are divided into 2 parts:
1. Setting up the computers -- flashing Jetpack and the ardupilot board
2. Setting up the HOUND hardware

### Setting up the Jetson Orin NX:

1. For this, you will require one Desktop, and the Orin NX, along with its corresponding parts (WiFi card, SSD, heat sink). After that, follow [this video](https://www.youtube.com/watch?v=Ucg5Zqm9ZMk) to flash the operating system onto the module, but flash jetpack 5.1.2.
2. Due to bugs in the SDK manager, the SDK manager will likely flash the operating system, but fail to properly install the jetpack. If this happens, you just need to do the following:
   ```bash
    sudo apt update
    sudo apt-get install nvidia-jetpack
    sudo usermod -aG docker $USER
    sudo pip install jetson-stats
    sudo reboot now
    ```

### Setting up the Hardware:
#### Setting up the base (These steps are a WIP and will be updated as we have people in our lab build more of these platforms while trying to follow these instructions). 
We re-use some of the build steps for the MuSHR to set up the low-level platform. Follow the instructions [here](https://mushr.io/hardware/build_instructions/#servo-motor-removal) for the following components:
1. [VESC Preparation](https://mushr.io/hardware/build_instructions/#vesc-preparation): Follow these steps to upload the VESC firmware. 
    - Instead of soldering the banana connectors, you will be soldering the IC3 connectors instead. Use the color of the wire to infer polarity, red for positive, black for negative.
    Pictures for reference (make sure to strip the wire down to 14-16 gauge):
    ![](content/wire_gauge.jpg)
    ![](content/IC3_connector.jpg)
    - Using the [BLDC tool](https://github.com/vedderb/bldc-tool/tree/master) (git clone, build), upload the [mushr_vesc_sensorless_config.xml](https://github.com/prl-mushr/vesc/blob/master/vesc_configs/mushr_vesc_sensorless_config.xml) parameter file.

2. [Servo removal](https://mushr.io/hardware/build_instructions/#servo-motor-removal) and [Servo installation](https://mushr.io/hardware/build_instructions/#servo-motor-installation): Instead of throwing away the servo mount that comes with the car, attach the new servo to the existing mount and attach the mount back into the car. (**TODO: reminder to center the servo!**)
3. [Brushed motor removal](https://mushr.io/hardware/build_instructions/#brushed-motor-removal): Follow the steps exactly.
4. [Brushless motor installation](https://mushr.io/hardware/build_instructions/#brushless-motor-installation): Follow the steps exactly

<p align="center">
  <img width="509" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/737714e1-9446-4b3a-a108-30f3b451fa0f">
</p>

5. Setting up the Remote controller with the Jetson: Follow the instructions in step 13 of the [Software setup](https://mushr.io/hardware/build_instructions/#software-setup).
Depending on your controller and exact servo spec, you may also need to follow steps 14 and 15.

7. Additionally, you may set up the Wi-Fi set up as indicated in steps 1-4 of the software setup.

#### Setting up the Lower Base:
1. First, the [front](https://github.com/prl-mushr/hound_hardware/blob/main/3D_files_MuSHR_V4/front_chassis_mount.stl) and [rear](https://github.com/prl-mushr/hound_hardware/blob/main/3D_files_MuSHR_V4/rear%20chassis%20mount.stl)
are mounted to the car using M3x10 screws. Then attach the front base and the rear base to the vehicle platform using the M3x40 screws as shown in the image.
(**TODO: this might need an image**)

<p align="center">
  <img width="624" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/3a3b47f5-0f63-481d-ae71-ba9499aeeff2">
</p>

2. Attach the front cover to the front base using the M4x40 screws
<p align="center">
  <img width="624" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/b62769a2-418f-45c4-8b34-b67db4796601">
</p>

3. Follow the following reference diagram for wiring
![connection_diagram](https://github.com/user-attachments/assets/099036ac-a08c-473d-a742-b87910d1a8a0)

4. Mount the VESC, exhaust fan on the rear base, and place the buck converters and R/C receiver using double sided tape as shown. Pass the motor cables through the whole marked on the right. Use the same hole to pass in the servo wires from underneath. Connect the VESC's USB wire, which will be attached to the Jetson later.
**TODO: insert image for how to mount VESC with the standoffs**.

<p align="center">
<img width="629" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/17885beb-6372-4b7d-b536-87377eba3e2c">
</p>

5. Mount the D455 to the front cover as shown using the M4x8 screws
<p align="center">
<img width="674" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/8fa1ea2e-c728-49cb-bbd0-3e02b77a77fa">
</p>

6. Mount the lidar_mount_left and lidar_mount_right to the YDLiDAR as shown using M3x10 screws. **TODO: this needs images**
<p align="center">
<img width="638" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/d56d6ba0-69eb-45fa-adcb-f25fb3892cbc">
</p>

7. Mount the LiDAR to the mid-section using M3x10 screws.
<p align="center">
<img width="730" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/b0b7821a-c6e2-470a-809d-7ad55e44280b">
</p>

8. Attach the mid-section to the front cover as shown
<p align="center">
  <img width="624" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/b62769a2-418f-45c4-8b34-b67db4796601">
</p>

9. Attach the rear cover to the rear base as shown.
<p align="center">
<img width="635" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/d4cb0a36-d078-4046-97d2-96c5b1dcfae3">
</p>

11. We use the latches and pins to attach the rear cover and the rear cover as shown. There are latch holders on the mid-section as well. (**TODO: this step needs more sub-steps with images as it is not obvious how to attach the spring in the latch to the pin.**)
<p align="center">
<img width="592" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/e7b3c627-493b-4261-b870-b9171e407588">
</p>

12. In the holes shown here, first screw in the M2.5x5 standoffs. Then, mount the Jetson Orin NX to the standoffs using M2.5x5 screws.
<p align="center">
<img width="532" alt="image" src="https://github.com/sidtalia/HOUND_hardware/assets/24889667/1e94ea48-deb5-490e-8505-451b74ef0224">
</p>

16. Connect the USB cables for all the devices.
