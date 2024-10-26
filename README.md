# Jetson Nano Docker Container for Nvidia Deep Learning Course 🚀

<h1 align="center">
    <img src="https://readme-typing-svg.herokuapp.com/?font=Righteous&size=35&center=true&vCenter=true&width=700&height=100&duration=4000&lines=Deep+Learning+on+Jetson+Nano!+🚀;" />
</h1>

## Overview
This repository provides a guide to setting up a Docker container on the Nvidia Jetson Nano for accessing and running deep learning course notebooks. The instructions are aimed at overcoming common network issues during Docker installation, specifically highlighting how to use a headless mode setup and SSH configuration for seamless remote access.

---

## 🚀 Quick Start Guide

### **Step 1: Ensure Fast Network Connectivity**
Make sure your Jetson Nano is connected to a stable 5G network or a fast LAN connection. Unstable networks can cause issues with Docker image downloads, leading to installation problems.

### **Step 2: Initial Setup (Headless Mode Recommended)**
To make your setup more efficient, follow these steps to enable headless mode and SSH:

1. **Connect Jetson Nano to a Screen Initially**
    - Start by connecting your Jetson Nano to a monitor to set up SSH. Once SSH is configured, you can manage your device remotely.

2. **Installing SSH on Jetson Nano**
    - Open a terminal on your Jetson Nano and run:
        ```bash
        sudo apt update
        sudo apt install openssh-server
        sudo systemctl start ssh
        sudo systemctl enable ssh
        sudo systemctl status ssh
        ```
    - Verify that SSH is running by checking its status. You can find your IP address using:
        ```bash
        ip addr show
        ```
    ![WhatsApp Image 2024-10-25 at 23 18 08_f5ecf6ec](https://github.com/user-attachments/assets/7df1b1c3-d191-4c3c-b470-64e9ddd67fa2)

    - Use the IP address with [PuTTY](https://www.putty.org/) or any SSH client to remotely connect to your Jetson Nano.
![Untitled design (2)](https://github.com/user-attachments/assets/f9253b43-5b1d-4837-ad06-4edc9d7564c4)



### **Step 3: Prepare Your Data Directory**
Create a directory for the deep learning course data:
```bash
mkdir -p ~/nvdli-data
```

### **Step 4: Verify JetPack Version**
Before proceeding, confirm your JetPack version:
```bash
dpkg-query --show nvidia-l4t-core
```
![image](https://github.com/user-attachments/assets/39510433-8f64-4bc4-b084-9ac2b904b3a0)

Ensure you are using a compatible version. You can find the corresponding Docker file version on [Nvidia's NGC website](https://ngc.nvidia.com/).

---

## 🐳 **Docker Container Setup**

### **Step 1: Create and Use a Reusable Docker Script**
1. Create a script to run the Docker container:
    ```bash
    echo "sudo docker run --runtime nvidia -it --rm --network host \
    --volume ~/nvdli-data:/nvdli-nano/data \
    --device /dev/video0 \
    nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1" > docker_dli_run.sh
    ```
2. Make the script executable:
    ```bash
    chmod +x docker_dli_run.sh
    ```
3. Run the script:
    ```bash
    ./docker_dli_run.sh
    ```

### **Step 2: Manual Docker Pull (If Needed)**
If the above method fails, try pulling the Docker image manually:
```bash
sudo docker pull nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1
```
Ensure your device is connected to a stable and fast internet connection for a smooth download.

### **Step 3: Run the Docker Container**
Once the image is installed, run the following command to launch the container:
```bash
sudo docker run --runtime nvidia -it --rm --network host nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1
```
![image](https://github.com/user-attachments/assets/29ab273a-8148-41c4-b692-def853d9723e)

After running, you'll receive a URL with an IP address to access Jupyter Notebook. Open this link in your browser, enter the password, and you should be able to access the deep learning course notebooks.
> Note: If you are facing problem while running the jupyter lab it is bacause this deep learning course is for camera so attach the camera with jetson nano and enter the ip address which you have entered in putty with :8888 like this below

```bash
192.168.XX.XX:8888
```
![image](https://github.com/user-attachments/assets/d2258841-2170-4dbb-bf22-e515b98d554a)
![e0ce5f0a3ef2d482d485e7f0df89aa0a](https://github.com/user-attachments/assets/04d6fc65-e759-4efa-aa29-b11f2055f481)

---

## 📝 **Notes**
- **Jetson Nano Compatibility:** Ensure your Docker file version matches your JetPack version. 
- **Network Requirements:** Stable and fast internet connectivity is crucial for smooth Docker image installation.

## 📚 **Additional Resources**
- [Nvidia Deep Learning Institute](https://developer.nvidia.com/dli)

---

By following this guide, you should be able to set up a functional Docker environment on your Jetson Nano, enabling you to work on Nvidia's deep learning courses efficiently.
