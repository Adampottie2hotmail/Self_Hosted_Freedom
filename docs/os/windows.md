---
title: Windows 10 / 11
description: A detailed guide for how to use Windows 10 or 11 as a server OS
icon: material/microsoft-windows
hide:
  - path
---


# **Setting Up Windows 10/11 as a Server: A Step-by-Step Guide**

## **1. Install Windows 10/11**
If you haven’t installed Windows yet, follow these steps:
- **Download the ISO:** Get Windows 10/11 from Microsoft's official website.
- **Create a Bootable USB:** Use **Rufus** or **Windows Media Creation Tool**.
- **Install Windows:** Boot from the USB, select your language, and install the OS.

**Post-Installation Setup:**
- Set up an **Administrator Account**.
- Disable unnecessary telemetry (`Settings > Privacy`).
- Install essential drivers (Chipset, LAN, Graphics, etc.).
- Enable **Remote Desktop** (`Settings > System > Remote Desktop`).

---

## **2. Configure Networking**
A server requires a **static IP address** to function reliably.

### **Set Static IP:**
1. **Go to:** `Control Panel > Network and Sharing Center > Change adapter settings`
2. Right-click your active network > **Properties**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** > **Properties**.
4. Choose **"Use the following IP address"**, enter:
   - **IP Address:** (e.g., `192.168.1.100`)
   - **Subnet Mask:** (e.g., `255.255.255.0`)
   - **Default Gateway:** (Your router's IP, e.g., `192.168.1.1`)
   - **Preferred DNS:** (Google: `8.8.8.8`, Cloudflare: `1.1.1.1`)

---

## **3. Install Server Features**
Windows 10/11 doesn’t come with **Windows Server** features, but you can enable similar functionality.

### **Enable File and Printer Sharing**
1. Open **Control Panel > Network and Sharing Center**.
2. Click **Change advanced sharing settings**.
3. Turn on:
   - **Network discovery**
   - **File and printer sharing**
   - **Password-protected sharing** (optional)

### **Enable SMB for File Sharing**
1. Open **Control Panel > Programs > Turn Windows features on or off**.
2. Enable **SMB 1.0/CIFS File Sharing Support**.
3. Click **OK** and restart.

### **Set Up a Shared Folder**
1. Right-click a folder > **Properties** > **Sharing** tab.
2. Click **Advanced Sharing > Share this folder**.
3. Set **permissions** (`Everyone` for open access or restrict users).
4. Use `\\yourserverIP\sharename` to access it.

---

## **4. Install and Configure a Web Server (IIS)**
Windows has a built-in web server called **IIS (Internet Information Services)**.

### **Enable IIS:**
1. Open **Control Panel > Programs > Turn Windows features on or off**.
2. Scroll down, check **Internet Information Services (IIS)**.
3. Expand **IIS > World Wide Web Services** and enable:
   - **Common HTTP Features**
   - **Application Development Features** (CGI, ASP.NET)
   - **Security** (Basic Authentication, Windows Authentication)
4. Click **OK** and restart.

### **Configure IIS:**
1. Open **IIS Manager** (`Windows + R`, type `inetmgr`, press Enter).
2. Expand **Sites**, right-click **Default Web Site**, select **Bindings**.
3. Click **Add**, set:
   - **Type:** HTTP
   - **IP Address:** (Choose your static IP)
   - **Port:** 80 (or 8080 if 80 is taken)
4. Place your website files in `C:\inetpub\wwwroot\`.

To access the website:
- From local network: `http://192.168.1.100`
- From the internet (requires port forwarding): `http://yourpublicIP`

---

## **5. Set Up Remote Access**
### **Enable Remote Desktop**
1. Go to `Settings > System > Remote Desktop`.
2. Enable **Remote Desktop** and **Allow connections**.
3. Open **Windows Firewall** and allow **Remote Desktop**.

### **Setup SSH Server (Optional)**
For remote command-line access:
1. Install **OpenSSH Server** (`Settings > Optional Features > Add Feature`).
2. Start the SSH service:
   ```powershell
   net start sshd
   ```
3. Connect via `ssh yourusername@yourserverIP`.

---

## **6. Install FTP Server (File Transfers)**
1. Open **Control Panel > Programs > Turn Windows features on or off**.
2. Enable **Internet Information Services > FTP Server**.
3. Open **IIS Manager > Add FTP Site**.
4. Set **Binding & SSL**:
   - **IP:** Static IP
   - **Port:** 21
   - **SSL:** No SSL (or use a certificate for security)
5. Set **Authentication & Authorization**:
   - **Authentication:** Basic
   - **Authorization:** Allow **specific users or Everyone**
   - **Permissions:** Read & Write
6. Access FTP via `ftp://192.168.1.100`.

---

## **7. Install Docker Desktop (Containerized Applications)**
Docker allows you to run applications in isolated containers.

### **Install Docker Desktop:**
1. Download from [Docker’s official site](https://www.docker.com/products/docker-desktop/).
2. Install and restart Windows.
3. Enable **WSL 2 Backend** (`Settings > Resources > WSL Integration`).
4. Open PowerShell and test:
   ```powershell
   docker --version
   ```

### **Run a Test Container:**
1. Pull an Nginx web server:
   ```powershell
   docker run -d -p 80:80 --name webserver nginx
   ```
2. Access via `http://localhost`.
3. Use `docker ps` to check running containers.

---

## **8. Secure Your Server**
### **Firewall Configuration**
- Open **Windows Defender Firewall**.
- Create **Inbound Rules** for only required services.
- Block unused ports.

### **Install SSL for Websites**
- Get a **free SSL certificate** from Let’s Encrypt.
- Use **Certbot** to automate renewal.

### **Set Up Automatic Backups**
- Use **Windows Backup** (`Control Panel > Backup & Restore`).
- Use **robocopy** or **PowerShell scripts** for scheduled backups.

---

## **9. Optimize Performance**
### **Disable Unnecessary Services**
Run `services.msc` and disable:
- **SysMain** (Superfetch) if using an SSD.
- **Windows Search** if not needed.
- **Xbox Services** (for gaming-related background services).

### **Optimize Power Settings**
- Set to **High Performance** (`Control Panel > Power Options`).
- Disable **Sleep/Hibernate** to keep services running.

---

## **Conclusion**
By following these steps, you’ve turned Windows 10/11 into a **fully functional server** capable of handling **file sharing, web hosting, remote access, and containerized applications**. 🚀
