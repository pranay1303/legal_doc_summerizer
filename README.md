# Legal Document Summarizer - CCA PBL Submission

**Group Number:** 13  
**Year/Division:** TY/A  

### Group Members
1. Pranay Dabhade: 371072
2. Dhimahi Patel: 371046
3. Niraj Pandit: 371043
4. Vaishnavi Kadam: 371064

---

## Project Overview

The **Legal Document Summarizer** is a cloud-native web application developed using Python and Streamlit to generate concise summaries of legal documents in PDF, DOCX, or TXT formats. Users can customize summary length (Short, Medium, or Long) to suit their needs, leveraging Google’s Gemini model API for advanced natural language processing.

The application is containerized using **Docker**, ensuring consistent performance across various environments. This containerization enables easy portability, quick updates, and seamless integration into the cloud. It is deployed on **AWS EC2 instances**, which provide scalable compute power, high availability, and secure cloud infrastructure. The use of EC2 ensures that the app can handle increasing user demands by allowing auto-scaling and flexible resource management.  

This robust architecture simplifies deployment, enhances performance, and reduces downtime. Designed for legal professionals and researchers, the **Legal Document Summarizer** combines cutting-edge NLP, Docker's portability, and EC2’s scalability to deliver a highly efficient document analysis solution.

### Key Features
- **Flexible Summary Options**: Users can choose from short, medium, or long summaries.
- **File Support**: Supports PDF, DOCX, and TXT document formats.
- **Text Extraction and Preview**: Allows previewing the extracted text before summarization.
- **Download and Clipboard Options**: Users can download the summary as a text file or copy it directly to the clipboard.
- **User-Friendly Interface**: Built with Streamlit for an intuitive and responsive UI.
- **Docker Deployment**: Includes a Dockerfile for streamlined deployment across compatible environments.

---

## Prerequisites

### For EC2 Deployment
1. **AWS Account**: Ensure you have an AWS account to launch an EC2 instance.
2. **EC2 Security Group**: Allow inbound traffic on port **8501** (default for Streamlit apps).
3. **SSH Access**: Ensure you can SSH into the EC2 instance.
4. **GitHub Repository**: Have the project repository ready to clone (replace `"Your-repository-url"` with the actual URL).
5. **Python 3.7+ and pip**: Required to run Streamlit and other dependencies.
6. **Docker (Optional)**: For Docker-based deployment.

---

## Deployment Guide

### Option 1: Deploying the Streamlit App on an EC2 Instance (Without Docker)

1. **Launch EC2 Instance**: Log in to your AWS Console, launch an EC2 instance, and SSH into it.

2. **Update the System**:
   ```bash
   sudo apt update && sudo apt-get update
   sudo apt upgrade -y
   ```

3. **Install Required Packages**:
   ```bash
   sudo apt install git curl unzip tar make sudo vim wget -y
   ```

4. **Clone the Project Repository**:
   ```bash
   git clone "Your-repository-url"
   ```

5. **Install Python3 and pip**:
   ```bash
   sudo apt install python3-pip
   ```

6. **Install Project Dependencies**:
   Navigate to the cloned project directory, then run:
   ```bash
   pip3 install -r requirements.txt
   ```

7. **Run the App (Temporary)**:
   This will launch the app in the foreground:
   ```bash
   python3 -m streamlit run app.py
   ```

8. **Run the App (Permanent)**:
   To keep the app running in the background after closing SSH:
   ```bash
   nohup python3 -m streamlit run app.py &
   ```

> **Note:** The app will be accessible at `http://<EC2-Instance-IP>:8501`.

---

### Option 2: Deploying with Docker on EC2

1. **Launch an EC2 Instance** and SSH into it.

2. **Install System Updates**:
   ```bash
   sudo apt-get update -y
   sudo apt-get upgrade -y
   ```

3. **Install Docker**:
   ```bash
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo usermod -aG docker ubuntu
   newgrp docker
   ```

4. **Clone the Project Repository**:
   ```bash
   git clone "your-project-url"
   ```

5. **Build Docker Image**:
   Navigate to the project directory, then build the Docker image:
   ```bash
   docker build -t pranay1303/stapp:latest .
   ```

6. **Verify Docker Image**:
   Check that the image is available:
   ```bash
   docker images -a
   ```

7. **Run the Docker Container**:
   ```bash
   docker run -d -p 8501:8501 pranay1303/stapp
   ```

8. **Check Running Containers**:
   ```bash
   docker ps
   ```

9. **Stop a Container (if needed)**:
   ```bash
   docker stop <container_id>
   ```

10. **Remove All Containers (optional)**:
    ```bash
    docker rm $(docker ps -a -q)
    ```

11. **Push Image to Docker Hub (optional)**:
    ```bash
    docker login
    docker push pranay1303/stapp:latest
    ```

12. **Remove Local Docker Image (optional)**:
    ```bash
    docker rmi pranay1303/stapp:latest
    ```

> **Note:** The Docker-based app will also be accessible at `http://<EC2-Instance-IP>:8501`.

---

## Troubleshooting

- **Port Accessibility**: Ensure the EC2 security group allows inbound traffic on port 8501.
- **Dependency Issues**: Verify that all dependencies are correctly installed by checking the requirements file and confirming installation with `pip3 list`.
- **Docker Permissions**: After installing Docker, if you encounter permissions errors, run `sudo usermod -aG docker $USER` and restart the session.

This concludes the deployment instructions for the **Legal Document Summarizer**.
