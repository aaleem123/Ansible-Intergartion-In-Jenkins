**🚀 Jenkins + Ansible CI/CD Pipeline for AWS EC2**
- Deployment of a Node.js application to AWS EC2 instances using Jenkins, Ansible, and Docker.

**Project Components**
- **Jenkins Server (DockerMaster)**  
  - Runs in a Docker container on a dedicated EC2 instance  
  - Executes CI/CD pipeline  
- **Ansible Control Node**  
  - Configures and manages EC2 Worker Nodes  
  - Runs Ansible playbooks  
- **Two EC2 Worker Nodes**  
  - Host the deployed Dockerized Node.js application


## 🔧 **Pipeline Workflow**
- Jenkins pulls latest application code from GitHub  
- Builds application archive (`app.tar.gz`) dynamically  
- Copies Ansible configurations and archive to the Ansible Control Node  
- Ansible installs Docker, Docker Compose on Worker Nodes  
- Ansible deploys the Node.js application using Docker Compose  
- Application accessible via Worker Node public IPs

 **Screenshots Below**

![Screenshot 2025-07-02 191412](https://github.com/user-attachments/assets/584238cf-ec9c-40a9-a117-ddbdb62a13d1)

![Screenshot 2025-07-02 153042](https://github.com/user-attachments/assets/df781cda-6192-4c99-bfb1-6b24ba0e4b79)

![Screenshot 2025-07-02 155349](https://github.com/user-attachments/assets/ead2e4ad-3d87-46c5-9a39-b8c8ee7ae229)

![Screenshot 2025-07-02 190559](https://github.com/user-attachments/assets/9549ea7f-a847-4e74-8091-212570fbffeb)

![Screenshot 2025-07-02 190623](https://github.com/user-attachments/assets/078233a0-4d51-4046-ae62-f0e9e9835725)

![Screenshot 2025-07-02 191031](https://github.com/user-attachments/assets/ca142400-5c21-4a1c-89bd-fd0487b99230)

![Screenshot 2025-07-02 191041](https://github.com/user-attachments/assets/a97ca6f2-60d0-4963-834e-d2c347e44056)






