# Secure a Personal Website in the Cloud (English Version)

## Project by David

### Objective
Learn how to launch, configure, and secure a web server in the cloud using AWS, Ubuntu, and basic cybersecurity best practices. The goal was to gain hands-on experience with real-world tools and practices.

---

### Technologies Used
- AWS EC2 (Free Tier)
- Ubuntu Server 22.04
- Apache Web Server
- UFW Firewall
- Fail2Ban
- Let’s Encrypt + Certbot
- DuckDNS (free dynamic DNS)
- SSH (secure remote access)

---

### Steps Completed

1. **Launch EC2 Instance**
   - Ubuntu 22.04 LTS
   - t2.micro instance (free tier)
   - Public IPv4 address assigned
   - Opened ports: 22 (SSH), 80 (HTTP), 443 (HTTPS)

2. **Connect via SSH from Windows**
   - Used `.pem` key with PowerShell

3. **Update the System**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

4. **Install Apache Web Server**
   ```bash
   sudo apt install apache2 -y
   ```

5. **Create a New User**
   ```bash
   sudo adduser david
   sudo usermod -aG sudo david
   ```

6. **Enable Key Access for New User**
   ```bash
   sudo cp -r /home/ubuntu/.ssh /home/david/
   sudo chown -R david:david /home/david/.ssh
   ```

7. **Block SSH Access to Default User**
   - Edited `/etc/ssh/sshd_config`:
     ```
     DenyUsers ubuntu
     ```

8. **Enable and Configure UFW Firewall**
   ```bash
   sudo ufw allow OpenSSH
   sudo ufw allow 'Apache Full'
   sudo ufw enable
   ```

9. **Install Fail2Ban to Prevent Brute Force Attacks**
   ```bash
   sudo apt install fail2ban -y
   ```

10. **Scan for Unnecessary Services**
    ```bash
    sudo ss -tuln
    ps aux
    ```
    - Disabled and removed services not required for web hosting

11. **Setup DuckDNS for Free Domain**
    - Created subdomain and pointed to EC2 public IP

12. **Install Certbot and Enable HTTPS**
    ```bash
    sudo apt install certbot python3-certbot-apache -y
    sudo certbot --apache -d yourdomain.duckdns.org
    ```

13. **Force HTTP to HTTPS Redirect**
    - Done through Certbot during setup

---

### Lessons Learned
- Basic EC2 and SSH usage
- Server hardening fundamentals
- Apache configuration
- Firewall and access control
- HTTPS setup with a free SSL certificate
- Importance of logging and cleanup

---

### Next Steps
- Enable monitoring with AWS CloudWatch
- Set up automatic certificate renewal
- Build a simple portfolio on the secured site

---

# Asegurar un Sitio Web Personal en la Nube (Versión en Español)

## Proyecto realizado por David

### Objetivo
Aprender a lanzar, configurar y asegurar un servidor web en la nube utilizando AWS, Ubuntu y buenas prácticas de ciberseguridad. El enfoque fue adquirir experiencia real trabajando desde cero.

---

### Tecnologías utilizadas
- AWS EC2 (Free Tier)
- Ubuntu Server 22.04
- Servidor web Apache
- Firewall UFW
- Fail2Ban
- Let’s Encrypt + Certbot
- DuckDNS (DNS dinámico gratuito)
- Acceso remoto por SSH

---

### Pasos realizados

1. **Lanzamiento de instancia EC2**
   - Ubuntu 22.04 LTS
   - Instancia t2.micro (free tier)
   - IP pública asignada
   - Puertos abiertos: 22 (SSH), 80 (HTTP), 443 (HTTPS)

2. **Conexión por SSH desde Windows**
   - Usando la llave `.pem` en PowerShell

3. **Actualización del sistema**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

4. **Instalación del servidor Apache**
   ```bash
   sudo apt install apache2 -y
   ```

5. **Creación de usuario no root**
   ```bash
   sudo adduser david
   sudo usermod -aG sudo david
   ```

6. **Configurar acceso SSH con clave para el nuevo usuario**
   ```bash
   sudo cp -r /home/ubuntu/.ssh /home/david/
   sudo chown -R david:david /home/david/.ssh
   ```

7. **Bloquear acceso SSH al usuario por defecto**
   - Editar `/etc/ssh/sshd_config`:
     ```
     DenyUsers ubuntu
     ```

8. **Activar y configurar el firewall UFW**
   ```bash
   sudo ufw allow OpenSSH
   sudo ufw allow 'Apache Full'
   sudo ufw enable
   ```

9. **Instalar Fail2Ban para proteger de ataques por fuerza bruta**
   ```bash
   sudo apt install fail2ban -y
   ```

10. **Revisión de servicios activos innecesarios**
    ```bash
    sudo ss -tuln
    ps aux
    ```
    - Se desactivaron procesos no esenciales

11. **Configurar dominio gratuito en DuckDNS**
    - Crear subdominio y apuntar a la IP de EC2

12. **Instalar Certbot y habilitar HTTPS**
    ```bash
    sudo apt install certbot python3-certbot-apache -y
    sudo certbot --apache -d tudominio.duckdns.org
    ```

13. **Redirección forzada de HTTP a HTTPS**
    - Configurada por Certbot durante la instalación

---

### Lecciones aprendidas
- Manejo de EC2 y conexiones SSH
- Endurecimiento de servidores
- Configuración básica de Apache
- Control de acceso y firewall
- Instalación de certificados SSL gratuitos
- Limpieza de servicios innecesarios

---

### Próximos pasos
- Monitoreo con CloudWatch
- Renovación automática de certificados
- Crear una página de portafolio sobre el sitio seguro
