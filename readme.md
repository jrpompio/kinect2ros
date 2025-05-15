# Kinect2 ROS 2 Driver

This repository contains a ROS 2 driver for the Kinect 2 sensor.

## Prerequisites

Before you begin, ensure you have ROS 2 Humble installed on your system. You can follow the official [ROS 2 installation guide](https://docs.ros.org/en/humble/Installation.html).

## Installation

### Step 1: Install libfreenect2

To use the Kinect 2 sensor, you need to install the `libfreenect2` library. Follow these steps:

```bash
git clone https://github.com/OpenKinect/libfreenect2.git
cd libfreenect2 && mkdir build && cd build
cmake ..
sudo make install
```

You can customize the build with various options. For example:

```bash
cmake .. -DENABLE_CXX11=ON -DENABLE_OPENCL=ON -DENABLE_CUDA=OFF -DENABLE_OPENGL=ON -DCMAKE_INSTALL_PREFIX=/usr
```

### Step 2: Add udev Rules for Kinect2

Copy the existing udev rules file from the cloned `libfreenect2` repository to allow the system to recognize and configure the Kinect 2 device properly:

1. Copy the rules file to the udev rules directory:

   ```bash
   sudo cp libfreenect2/platform/linux/udev/90-kinect2.rules /etc/udev/rules.d/
   ```

2. Reload the udev rules to apply the changes:

   ```bash
   sudo udevadm control --reload-rules
   sudo udevadm trigger
   ```

### Step 3: Clone the Repository

Clone this repository into the `src` directory of your ROS 2 workspace:

```bash
mkdir -p kinect2_ws/src
cd kinect2_ws/src
git clone https://github.com/ZachDaChampion/kinect2ros
```

### Step 4: Install Dependencies

Ensure `rosdep` is initialized and updated, then install the necessary dependencies. Make sure to run this from the root of your workspace:

```bash
cd ..
rosdep update
rosdep install -i --from-path src --rosdistro humble -y
```

### Step 5: Build the Workspace

Navigate to the root of your workspace and build the package:

```bash
colcon build
```

### Step 6: Source the Workspace

Source the setup file to include the workspace in your environment:

```bash
source install/local_setup.bash
```

## Running the Kinect2 Driver

To run the Kinect2 driver, use the following command:

```bash
ros2 run kinect2ros kinect2ros
```

## Additional Information

- Ensure your Kinect 2 sensor is properly connected to your computer.
- You may need to adjust the permissions for USB devices if you encounter any issues.

## Troubleshooting

If you encounter any issues, please refer to the [official ROS 2 troubleshooting guide](https://docs.ros.org/en/humble/Troubleshooting.html) or open an issue in this repository.
