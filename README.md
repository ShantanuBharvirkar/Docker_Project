### **Nextcloud Docker Deployment**
What is Nextcloud Docker?
Nextcloud Docker is a containerized version of Nextcloud, an open-source platform for file storage, collaboration, and cloud computing. Using Docker to deploy Nextcloud simplifies the installation process by encapsulating the application and its dependencies into a portable container.

With Docker, users can:

Run Nextcloud in a consistent environment, regardless of the underlying system.
Avoid dependency conflicts by isolating Nextcloud and its components.
Manage updates and scaling with minimal effort.
Key Features of Nextcloud Docker
Quick Deployment: Simplifies the installation of Nextcloud and its dependencies (like MariaDB or PostgreSQL) using containerized services.
Data Persistence: Ensures user data and settings are stored securely outside the container, preventing loss during updates or restarts.
Scalability: Supports scaling by integrating additional services (e.g., Redis for caching, Collabora/OnlyOffice for document editing).
Portability: Allows easy migration between systems without reconfiguring the application.
Customization: Enables users to integrate third-party plugins and extend functionality.
Security: Provides isolation from the host system and simplifies SSL integration for secure data transmission.
When to Use Nextcloud Docker
Using Nextcloud Docker is ideal when:

You need a fast, reproducible deployment.
You want to avoid managing dependencies manually.
You're familiar with Docker and containerized environments.
You aim to maintain privacy by hosting your cloud storage locally or on a self-managed server.
Components of a Typical Nextcloud Docker Deployment
Nextcloud Application Container:

Provides the core functionalities of Nextcloud.
Handles user interface, file management, and backend operations.
Database Container (e.g., MariaDB or PostgreSQL):

Stores user data, settings, and application metadata.
Ensures reliable, persistent data management.
Optional Add-ons:

Redis: Enhances caching for improved performance.
Reverse Proxy (e.g., Nginx or Traefik): Manages SSL certificates and enables HTTPS access.
Collabora Online or OnlyOffice: Provides online document editing capabilities.
Volumes:

Used to persist data outside of the containers, ensuring files, settings, and database records are not lost when containers are restarted or updated.
Why Choose Nextcloud Docker?
Ease of Setup: Docker simplifies deployment by eliminating the need to manually configure web servers, databases, and dependencies.
Efficiency: Containers are lightweight and resource-efficient compared to virtual machines.
Flexibility: Docker allows you to experiment with configurations and reset quickly if needed.
Community Support: The Nextcloud Docker image is actively maintained, with regular updates and robust community support.

For comprehensive instructions, refer to the Docker | Nextcloud Documentation.

---

### **Project Report: Deploying Nextcloud Using Docker on Windows**

---

#### **1. Introduction**

This project outlines the deployment of Nextcloud, an open-source, self-hosted cloud storage and productivity platform, on a Windows platform using Docker. Utilizing Docker containers ensures a consistent and efficient setup process, enabling users to manage files, tasks, and collaborative tools privately and securely.

---

#### **2. About Nextcloud**

Nextcloud is a versatile, local-first cloud platform designed to give users full control over their data. Key features include:

- **File Storage and Sharing**: Securely store, access, and share files.
- **Collaboration Tools**: Integrate calendars, tasks, and communication tools.
- **Privacy**: Retain complete control over data without relying on third-party services.
- **Synchronization**: Sync files and data across multiple devices seamlessly.
- **Scalability**: Extendable with numerous plugins and integrations.

By focusing on self-hosting and data privacy, Nextcloud offers a robust alternative to commercial cloud services.

---

#### **3. Objectives**
- Deploy Nextcloud on a Windows system using Docker.
- Ensure data persistence and accessibility through proper volume configuration.
- Enable secure access to Nextcloud across devices.

---

#### **4. Prerequisites**

Before proceeding with the deployment, ensure the following are installed on your Windows system:

- **Docker Desktop**: Provides the Docker Engine and Docker Compose necessary for container management. [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)
- **Windows Subsystem for Linux 2 (WSL2)**: Enhances Docker's performance on Windows.

**Installing WSL2:**

1. **Enable the WSL Feature**:
   - Open PowerShell as Administrator.
   - Run:
     ```powershell
     dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
     ```

2. **Enable the Virtual Machine Platform Feature**:
   - In the same PowerShell window, run:
     ```powershell
     dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
     ```

3. **Update the WSL Kernel**:
   - Download the latest WSL2 kernel update from the Microsoft WSL2 Kernel Update.
   - Run the installer.

4. **Set WSL2 as the Default Version**:
   - In PowerShell, run:
     ```powershell
     wsl --set-default-version 2
     ```

5. **Install a Linux Distribution**:
   - Open the Microsoft Store.
   - Search for and install your preferred Linux distribution (e.g., Ubuntu).
   - Launch the distribution and complete the initial setup.

For detailed instructions, refer to the [Microsoft WSL Installation Guide](https://learn.microsoft.com/en-us/windows/wsl/install).

---

#### **5. Steps to Set Up Nextcloud Using Docker**

---

**Step 1: Install Docker Desktop**
- Download Docker Desktop from the [official website](https://www.docker.com/products/docker-desktop/).
- Run the installer and follow the on-screen instructions.
- Ensure Docker Desktop is configured to use WSL2 as the backend.

---

**Step 2: Create a Docker Compose File**

Prepare a `docker-compose.yml` file to define the Nextcloud and database services. Create a directory for the file, e.g., `C:\NextcloudSetup`.

Example `docker-compose.yml`:

```yaml
version: '3.7'

services:
  nextcloud:
    image: nextcloud
    container_name: nextcloud
    ports:
      - "8080:80"
    volumes:
      - nextcloud_data:/var/www/html
    environment:
      - MYSQL_HOST=db
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=securepassword
    depends_on:
      - db

  db:
    image: mariadb
    container_name: nextcloud_db
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=securepassword
    volumes:
      - db_data:/var/lib/mysql

volumes:
  nextcloud_data:
  db_data:
```

---

**Step 3: Deploy the Nextcloud and Database Containers**

1. Open Command Prompt or PowerShell.
2. Navigate to the directory containing the `docker-compose.yml` file:
   ```bash
   cd C:\NextcloudSetup
   ```
3. Start the services:
   ```bash
   docker-compose up -d
   ```

---

**Step 4: Access Nextcloud**

- Open a web browser and navigate to `http://localhost:8080`.
- Complete the Nextcloud setup wizard by providing the database credentials specified in the `docker-compose.yml` file:
  - Database: `nextcloud`
  - Username: `nextcloud`
  - Password: `securepassword`
  - Database host: `db`

---

#### **6. Conclusion**

Deploying Nextcloud using Docker on a Windows system provides a streamlined approach to managing personal and collaborative cloud storage with enhanced data privacy. The use of Docker containers ensures consistency across different environments and simplifies the deployment process.

---

#### **7. Future Enhancements**
- **SSL Configuration**: Set up SSL certificates to enable secure HTTPS access.
- **Automated Backups**: Schedule regular backups of data volumes to prevent data loss.
- **External Storage Integration**: Configure Nextcloud to integrate with external storage services like Google Drive or S3-compatible storage.
- **Mobile Access**: Adjust network settings to allow secure access from mobile devices outside the local network.

## Demo

https://github.com/user-attachments/assets/9681a1f2-83ca-40d5-87e0-7e39cbc58b79
