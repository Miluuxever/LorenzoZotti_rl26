# Robotics Lab 2026 - Classwork 0

Repository for the Robotics Lab 2026 course. The objective of this project is to set up a local development environment based on **Linux**, **Git**, and **Docker**, preparing a container configured for ROS 2 (Humble).

[Guide designed for Ubuntu Linux 26.04 LTS (Resolute Racoon)]

---

## Prerequisites

To properly execute this project, you need to have:
- A **Linux** operating system (e.g., native Ubuntu, WSL2, or virtual machine).
- **Git** installed on the host machine.

---

## Installing Git

`(Skip to Docker installation if you already have a configured Git environment)`

To install Git on your operating system, simply run the following command in any open terminal:

    sudo apt install git

If everything went well, you can check the installed version of Git with:

    git --version

Set up your GitHub account credentials:

    git config --global user.name <username>
    git config --global user.email <email>

---

## Installing Docker

If you do not have Docker installed on your Linux system, run these steps from the terminal to install it:

1. Update the package list and install the required dependencies:
   ```bash
   sudo apt update
   sudo apt install apt-transport-https curl gnupg-agent ca-certificates software-properties-common -y
2. Create the directory for security keyrings and download the official Docker GPG key:
    ```bash
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
3. Add the official Docker repository to the apt sources:
    ```bash
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
4. Update the package index again and proceed with installing Docker Engine:
    ```bash
    sudo apt update
    sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
---

## Configuring and Running the Docker Workspace

In your workspace, create a new folder for the project and navigate into it:

    mkdir -p <desired_name>
    cd <desired_name>/

Clone the repository:

    git clone <repo_URL>

Run the following commands to make the scripts executable:

    chmod +x LorenzoZotti_rl26/docker_scripts/ros2_docker_scripts/*.sh

or simply:

    chmod +x *.sh

if you are already inside `ros2_docker_scripts`.
Following the same logic, proceed with building the image:

    ./LorenzoZotti_rl26/docker_scripts/ros2_docker_scripts/docker_build_image.sh <image_name>
Choose `<image_name>` as you prefer. Then run the container:

    ./LorenzoZotti_rl26/docker_scripts/ros2_docker_scripts/docker_run_container.sh

selecting (via "number" + enter) the Docker image corresponding to `<image_name>`. Follow the remaining steps by defining `[CONTAINER_NAME]` and `[FOLDER_NAME]`.
---
## Verifying the Correct Installation

While the container is running, you can verify that ROS 2 is correctly installed by running:

    echo $ROS_DISTRO   # Expected output: humble
    ros2 pkg list      # Verifies the list of available ROS 2 packages
To exit the container and terminate operations, simply use the command:

    exit