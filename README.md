# ROS 2 Humble Installation & Troubleshooting Report

This repository documents the step-by-step process of installing **ROS 2 Humble** on **Ubuntu 22.04 LTS** via Windows Subsystem for Linux (WSL), along with the challenges faced during the setup.


## 🛠️Installation Steps

1. **Enable and Install WSL & Ubuntu 22.04:**
Installed the Ubuntu 22.04 distribution directly through PowerShell:
```
wsl --install -d Ubuntu-22.04

```


Followed the prompts to set up the UNIX username and password.
2. **Update the System:**
Ensured all system packages were up to date:
```
sudo apt update && sudo apt upgrade -y

```


3. **Set Up Locales and Sources:**
Installed required utilities and added the ROS 2 GPG key:
```
sudo apt install software-properties-common curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

```


4. **Add the ROS 2 Repository:**
Added the official ROS 2 repository to the system sources:
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu jammy main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

```


5. **Install ROS 2 Desktop Package:**
Updated the package list and installed the core desktop environment:
```
sudo apt update
sudo apt install ros-humble-desktop -y

```


6. **Environment Setup:**
Configured the bash environment to automatically load ROS variables on startup:
```
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc

```


##  Challenges & Troubleshooting

During the installation process, a few issues were encountered and successfully resolved:

1. **Secure Channel / Network Connection Error (`0x80072f7d`):**
* **Problem:** An error occurred while downloading the Ubuntu distribution through PowerShell due to secure channel communication restrictions (often triggered by local firewall or network policies).
* **Solution:** Temporarily paused third-party security software interference, verified the network stability, and re-executed the installation command cleanly.


2. **Typo in the Keyring Command:**
* **Problem:** A minor syntax error occurred when running the `curl` command due to an attached `sudo` keyword (`-sSLsud`), causing a destination path write failure.
* **Solution:** Corrected the command structure by properly separating `sudo` and `curl` arguments with the correct `-o` flag output path.


3. **Missing File Directory Error (`No such file or directory`):**
* **Problem:** Attempting to source the environment before the ROS package was fully installed resulted in a missing file error.
* **Solution:** Ensured the `sudo apt install ros-humble-desktop -y` command completed its execution fully before setting up the bash environment variables.



---

انسخي هذا المحتوى وضعيه مباشرة في ملف الـ `README.md` الخاص بمشروعك على جيت هب، وبالتوفيق في التاسك!
