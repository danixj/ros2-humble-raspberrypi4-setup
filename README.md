# 🧠 ROS 2 Humble Setup on Raspberry Pi 4
ROS 2 Humble installation on Raspberry Pi 4 using Ubuntu 22.04 LTS

---

## 📌 Overview

This repository provides a complete, step-by-step guide to install Ubuntu 22.04 Desktop (64-bit) and ROS 2 Humble Hawksbill on a Raspberry Pi 4.

This setup is suitable for:
- Robotics students and educators
- Beginners learning ROS 2
- Mobile robot projects
- LiDAR, SLAM, and navigation applications

---

## 🧰 Hardware Requirements

- Raspberry Pi 4 (4GB or 8GB recommended)
- microSD Card (32GB minimum, 64GB preferred – A1 / UHS-I)
- HDMI Monitor
- USB Keyboard & Mouse
- Internet connection (Wi-Fi / Ethernet)
- Power Supply: 5V ⎓ 3A

---

## 💻 Software Requirements

- Raspberry Pi Imager
- Ubuntu Desktop 22.04 LTS (64-bit)

---

## 🐧 Ubuntu 22.04 Installation

1. Open Raspberry Pi Imager
2. Select:
   - Device: Raspberry Pi 4
   - OS: Ubuntu → Ubuntu Desktop 22.04 LTS (64-bit)
3. Select SD card and click Write
4. Insert SD card into Raspberry Pi and power ON
5. Complete the Ubuntu first-boot setup

---

## ⚙️ Basic System Setup

Open Terminal (Ctrl + Alt + T) and run:

```bash
sudo apt update
sudo apt upgrade -y
sudo reboot
```

Verify Ubuntu version:

```bash
lsb_release -a
```

Expected:
```
Release: 22.04
Codename: jammy
```

Verify system architecture:

```bash
uname -m
```

Expected:
```
aarch64
```

---

## 🤖 ROS 2 Humble Installation

### Install required system tools

```bash
sudo apt install -y \
  curl \
  gnupg2 \
  lsb-release \
  software-properties-common \
  build-essential
```

---

### Configure locale (important)

```bash
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

---

### Add ROS 2 repository

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
-o /usr/share/keyrings/ros-archive-keyring.gpg
```

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

```bash
sudo apt update
```

---

### Install ROS 2 Humble Desktop

```bash
sudo apt install -y ros-humble-desktop
```

---

### Source ROS automatically

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

Verify installation:

```bash
ros2 --help
```

---

## ✅ Test ROS 2 Installation

Open two terminals.

Terminal 1:

```bash
ros2 run demo_nodes_cpp talker
```

Terminal 2:

```bash
ros2 run demo_nodes_cpp listener
```

If messages are exchanged, ROS 2 is working correctly.

---

## 🏗️ Create a ROS 2 Workspace

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
```

Source the workspace:

```bash
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 🧭 Next Steps

After completing this setup, the system is ready for:
- Keyboard teleoperation (/cmd_vel)
- Motor driver or ESP32 integration
- LiDAR driver setup
- SLAM (mapping)
- Autonomous navigation

---

## 👤 Author

**Dani Johnson**  
Robotics Engineer & Robotics Educator  
Evolve Robotics  

📍 Ernakulam, Kerala, India  
🔗 LinkedIn: https://www.linkedin.com/in/dani-johnson-955424190  

---

## 📜 License

This project is licensed under the MIT License.  
Free to use for educational and research purposes.

---

## ⭐ Acknowledgements

- ROS 2 Community  
- Open Source Robotics Foundation (OSRF)  
- Ubuntu & Raspberry Pi communities
