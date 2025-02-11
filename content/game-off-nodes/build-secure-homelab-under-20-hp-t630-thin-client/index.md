---
date: '2025-02-10T22:40:35-06:00'
draft: true
title: "Building a Secure Homelab Under $20 Using an HP t630 Thin Client: A Beginner's Guide"
tags: ["homelab", "HP t630", "budget computing", "Nginx Proxy Manager", "Cloudflare", "Tailscale", "guide"]  
description: "Learn how to set up a secure and accessible homelab for under $20 using an HP t630 Thin Client. This comprehensive guide provides step-by-step instructions tailored for beginners, covering hardware acquisition, Linux installation, Docker and Nginx Proxy Manager setup, and secure remote access configuration with Cloudflare and Tailscale."  
seo_keywords: "homelab setup, HP t630 Thin Client, budget homelab, Nginx Proxy Manager tutorial, Cloudflare DNS setup, Tailscale VPN guide, beginner's homelab guide"  
---

Embarking on the journey of setting up a **homelab** is an excellent way to delve into the realms of self-hosting, server management, and networking. For beginners, the process might seem daunting, especially with concerns about cost and complexity. Fear not! This guide is crafted to walk you through creating a **secure, remotely accessible homelab for under $20** using an **HP t630 Thin Client**. By the end of this tutorial, you'll have a robust system that allows you to:

- **Securely Access Services:** Utilize subdomains to manage your services without memorizing IP addresses and ports.
- **Remote Connectivity:** Access your homelab from anywhere globally without exposing your network to potential threats.
- **Scalability:** Lay the foundation for future expansions, including adding more services or nodes to your homelab.

Let's dive in!

## Requirements

Before we begin, ensure you have the following:

- **HP t630 Thin Client**: A cost-effective, compact device ideal for homelab setups.
- **Registered Domain**: Essential for setting up subdomains and managing DNS records.
- **Cloudflare Account**: A free service to manage DNS and enhance security.
- **Tailscale Account**: Provides a secure VPN solution for remote access.
- **USB Flash Drive (8GB or larger)**: Needed for installing the operating system.

## Step 1: Acquiring an HP t630 Thin Client

The **HP t630 Thin Client** is a versatile device equipped with:

- **Processor**: AMD GX-420GI Quad-Core APU (2.0 - 2.2 GHz)
- **Memory**: 4GB DDR4 RAM (upgradable)
- **Storage**: 32GB M.2 SATA SSD
- **Graphics**: Integrated AMD Radeon R6E

To find one within our budget:

1. **Visit eBay**: Navigate to [eBay](https://www.ebay.com/) and use the search bar.
2. **Search Parameters**: Enter "HP t630 Thin Client".
3. **Apply Filters**:
   - **Price Range**: Set a maximum of $25 to allow room for negotiation.
   - **Listing Type**: Select "Best Offer" to propose your price.
   - **Condition**: Choose "Used" or "Refurbished" to find affordable options.
4. **Monitor Listings**: Check daily for new listings and be prepared to negotiate. Patience is key; within a week, you should secure a deal around $15.

**Tip**: Always review the seller's feedback and the item's condition description to ensure a satisfactory purchase.

## Step 2: Inspecting and Preparing the Device

Upon receiving your HP t630:

1. **Visual Inspection**:
   - **Exterior**: Look for any physical damage or wear.
   - **Ports**: Ensure all USB, DisplayPort, and network ports are intact.
2. **Internal Examination**:
   - **Accessing the Interior**: Remove the casing carefully.
   - **Components**: Verify the presence and condition of RAM, SSD, and other components.
   - **Cleaning**: Use compressed air to remove any dust accumulation.
3. **Documentation**:
   - **Photographs**: Take clear pictures of the internal layout. This will be helpful for future upgrades or troubleshooting without reopening the device.

**Note**: Handling internal components requires caution. Ground yourself to prevent static discharge, which can damage electronic parts.

## Step 3: Installing Ubuntu Minimal

A lightweight Linux distribution ensures optimal performance on the thin client. We'll use **Ubuntu Server Minimal** for this setup.

1. **Download Ubuntu Server**:
   - Visit the [Ubuntu Server download page](https://ubuntu.com/download/server).
   - Choose the latest LTS (Long-Term Support) version for stability.
2. **Create a Bootable USB**:
   - **Tools**: Use [Rufus](https://rufus.ie/) for Windows or [Etcher](https://www.balena.io/etcher/) for macOS/Linux.
   - **Process**:
     - Insert your USB flash drive.
     - Open the chosen tool and select the Ubuntu ISO file.
     - Ensure the correct USB drive is selected to prevent data loss.
     - Start the process and wait until completion.
3. **Boot from USB**:
   - **Connect Peripherals**: Attach a monitor, keyboard, and mouse to the HP t630.
   - **Insert USB Drive**: Plug the bootable USB into the device.
   - **Access Boot Menu**:
     - Power on the device and press the appropriate key (usually **F9** for HP devices) to access the boot menu.
     - Select the USB drive to boot from.
4. **Install Ubuntu**:
   - **Follow On-Screen Prompts**: The installation process will guide you through language selection, keyboard layout, and other settings.
   - **Network Configuration**:
     - **Static IP Address**: Assign a static IP to ensure consistent network access. For example:
       - IP Address: `192.168.1.100`
       - Subnet Mask: `255.255.255.0`
       - Gateway: `192.168.1.1`
       - DNS: `8.8.8.8` (Google's DNS)
   - **Minimal Installation**: Opt for the minimal installation to reduce resource usage.
   - **User Setup**: Create a username and strong password for administrative access.

**Tip**: Keep your system updated by running:

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 4: Installing Docker and Portainer

**Docker** is a platform that enables you to develop, ship, and run applications inside containers. Containers are lightweight, portable, and ensure that your applications run seamlessly across different environments. **Portainer** is a web-based management tool that simplifies working with Docker by providing a user-friendly interface.

### Installing Docker

1. **Update Package Lists**: Begin by updating your system's package lists to ensure you have the latest information on available packages.

   ```bash
   sudo apt update
   ```

2. **Install Prerequisite Packages**: These packages allow `apt` to use repositories over HTTPS.

   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
   ```

3. **Add Docker’s GPG Key**: This step ensures that the software you're installing is authentic and hasn't been tampered with.

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

4. **Add Docker Repository**: Add the Docker repository to `apt` sources to fetch Docker packages.

   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

5. **Update Package Lists Again**: Refresh your package lists to include the Docker repository.

   ```bash
   sudo apt update
   ```

6. **Install Docker**: Now, install Docker.

   ```bash
   sudo apt install docker-ce -y
   ```

7. **Verify Docker Installation**: Check if Docker is installed and running.

   ```bash
   sudo systemctl status docker
   ```

   You should see an output indicating that Docker is active and running.

8. **Manage Docker as a Non-Root User**: To avoid using `sudo` with every Docker command, add your user to the Docker group.

   ```bash
   sudo usermod -aG docker ${USER}
   ```

   After running this command, log out and log back in to apply the changes.

### Installing Portainer

Portainer provides a graphical interface to manage Docker containers, images, networks, and volumes, making it easier, especially for beginners.

1. **Create a Volume for Portainer Data**: Docker volumes are used to persist data. Creating a volume for Portainer ensures that its data remains intact across container restarts.

   ```bash
   docker volume create portainer_data
   ```

2. **Deploy Portainer Container**: Run the following command to download and start the Portainer container.

   ```bash
   docker run -d -p 8000:8000 -p 9443:9443 \
     --name=portainer \
     --restart=always \
     -v /var/run/docker.sock:/var/run/docker.sock \
     -v portainer_data:/data \
     portainer/portainer-ce:latest
   ```

   Here's a breakdown of the command:

   - `-d`: Runs the container in detached mode (in the background).
   - `-p 8000:8000 -p 9443:9443`: Maps ports 8000 and 9443 of the container to the same ports on the host. Port 9443 is used for accessing the Portainer web interface securely.
   - `--name=portainer`: Names the container "portainer".
   - `--restart=always`: Ensures that the Portainer container restarts automatically if it stops or if the system reboots.
   - `-v /var/run/docker.sock:/var/run/docker.sock`: Grants Portainer access to the Docker socket to manage Docker.
   - `-v portainer_data:/data`: Mounts the previously created volume to persist Portainer's data.

3. **Access the Portainer Web Interface**:

   - Open your web browser and navigate to `https://your-server-ip:9443`. Replace `your-server-ip` with the static IP address you assigned to your HP t630 Thin Client during the Ubuntu installation.
   - Since it's a self-signed certificate, you might encounter a security warning. It's safe to proceed.
   - On the first visit, you'll be prompted to create an admin user. Set a strong password to secure your Portainer instance.

By following these steps, you've successfully installed Docker and Portainer on your Ubuntu system. With Portainer's intuitive interface, managing Docker containers becomes more accessible, allowing you to deploy and oversee applications with ease.

In the next steps, we'll set up Nginx Proxy Manager to manage your subdomains and configure secure remote access using Cloudflare and Tailscale. 


## Step 5: Installing and Configuring Nginx Proxy Manager (NPM)

**Nginx Proxy Manager** is a powerful tool that simplifies the management of reverse proxies. It allows you to access your homelab services using subdomains (e.g., `service.yourdomain.com`) instead of remembering complex IP addresses and port numbers. This setup not only streamlines access but also provides a centralized point of entry, which is beneficial as your homelab grows.

### Prerequisites

Before proceeding, ensure that:

- **Docker** and **Docker Compose** are installed on your Ubuntu system.
- You have administrative access to your system.

### Installation Steps

1. **Create a Directory for NPM**:
   - Open a terminal window.
   - Create a new directory for NPM and navigate into it:
     ```bash
     mkdir ~/nginx-proxy-manager && cd ~/nginx-proxy-manager
     ```

2. **Create the Docker Compose File**:
   - Use a text editor to create a `docker-compose.yml` file:
     ```bash
     nano docker-compose.yml
     ```
   - Paste the following content into the file:
     ```yaml
     version: '3'
     services:
       app:
         image: 'jc21/nginx-proxy-manager:latest'
         container_name: npm
         restart: unless-stopped
         ports:
           - '80:80'    # HTTP
           - '443:443'  # HTTPS
           - '81:81'    # NPM Admin Panel
         volumes:
           - ./data:/data
           - ./letsencrypt:/etc/letsencrypt
     ```
     This configuration sets up NPM to handle HTTP, HTTPS, and provides access to its administrative interface on port 81.

3. **Start NPM Using Docker Compose**:
   - Run the following command to download and start the NPM container:
     ```bash
     docker-compose up -d
     ```
   - The `-d` flag runs the container in detached mode, allowing it to operate in the background.

4. **Access the NPM Web Interface**:
   - Open your web browser and navigate to `http://your-server-ip:81`.
   - Replace `your-server-ip` with the static IP address of your HP t630 Thin Client.
   - On the login page, use the default credentials:
     - **Email**: `admin@example.com`
     - **Password**: `changeme`
   - After logging in, you'll be prompted to change these credentials. It's crucial to set a strong, unique password to secure your NPM instance.

### Setting Up a Proxy Host

With NPM installed, you can now configure it to manage access to your homelab services.

1. **Add a New Proxy Host**:
   - In the NPM dashboard, navigate to the "Proxy Hosts" section.
   - Click on the "Add Proxy Host" button.

2. **Configure the Proxy Host**:
   - **Domain Names**: Enter the subdomain you wish to use (e.g., `service.yourdomain.com`).
   - **Scheme**: Choose `http` or `https` based on your service's configuration.
   - **Forward Hostname / IP**: Enter the internal IP address of the service within your network (e.g., `192.168.1.105`).
   - **Forward Port**: Enter the port number on which the service is running (e.g., `8080`).
   - **Websockets Support**: Enable this if your service requires websocket support.
   - **Block Common Exploits**: It's advisable to enable this for added security.
   - **SSL**: If you have an SSL certificate for your subdomain, you can configure it here. Alternatively, you can use NPM to obtain a free SSL certificate from Let's Encrypt.

3. **Save and Test**:
   - After configuring the proxy host, save the settings.
   - Test the subdomain in your web browser to ensure it correctly forwards to your internal service.

By following these steps, you've set up Nginx Proxy Manager to route external requests to your internal homelab services using friendly subdomain URLs. This configuration not only simplifies access but also enhances security by centralizing and managing entry points to your network.

In the next step, we'll configure **Cloudflare** to manage your domain's DNS settings, further securing and streamlining access to your homelab services. 

## Step 6: Configuring Cloudflare for Your Domain

**Cloudflare** offers robust DNS management and security features, making it an excellent choice for managing your domain's DNS settings.

### Adding Your Domain to Cloudflare

1. **Log in to Cloudflare**:
   - Navigate to the [Cloudflare dashboard](https://dash.cloudflare.com/) and log in with your credentials.

2. **Add a New Site**:
   - Click the **"Add a Site"** button.
   - Enter your domain name (e.g., `yourdomain.com`) and click **"Add Site"**.

3. **Choose a Plan**:
   - Select the **Free Plan**, which is sufficient for our setup.

4. **Review DNS Records**:
   - Cloudflare will scan for existing DNS records. Review and confirm them.

5. **Update Nameservers**:
   - Cloudflare will provide nameservers.
   - Log in to your domain registrar's dashboard and replace the existing nameservers with the ones provided by Cloudflare.
   - Propagation may take up to 24 hours, but it often updates sooner.

### Setting Up DNS Records for Your Homelab Services

1. **Access the DNS Management Page**:
   - In the Cloudflare dashboard, select your domain.
   - Navigate to the **"DNS"** tab.

2. **Add an A Record for Your Homelab**:
   - Click on **"Add record"**.
   - **Type**: Select **"A"**.
   - **Name**: Enter the desired subdomain (e.g., `service` for `service.yourdomain.com`).
   - **IPv4 Address**: Enter the static LAN IP address of your HP t630 Thin Client (e.g., `192.168.1.100`).
   - **Proxy Status**: Set to **"DNS Only"** (grey cloud) for now.
   - Click **"Save"**.

3. **Add Additional Records as Needed**:
   - Repeat the above steps for each service you want to expose via a subdomain.

## Step 7: Securing Your Subdomains with SSL Certificates

To ensure secure connections to your homelab services, we'll use **Nginx Proxy Manager (NPM)** to obtain SSL certificates via Let's Encrypt.

### Generating a Cloudflare API Token

1. **Log in to Cloudflare**:
   - Navigate to the [Cloudflare dashboard](https://dash.cloudflare.com/) and log in.

2. **Create an API Token**:
   - Click on your profile icon and select **"My Profile"**.
   - Navigate to the **"API Tokens"** section.
   - Click **"Create Token"**.
   - Use the **"Edit zone DNS"** template.
   - **Permissions**: Set to **Zone** > **DNS** > **Edit**.
   - **Zone Resources**: Set to **Include** > **All zones**.
   - Click **"Continue to summary"**, then **"Create Token"**.
   - Copy the generated token; you'll need it shortly.

### Obtaining a Wildcard SSL Certificate in NPM

1. **Access NPM**:
   - Open your web browser and navigate to `http://your-server-ip:81`.
   - Log in with your credentials.

2. **Add a New SSL Certificate**:
   - Navigate to the **"SSL Certificates"** section.
   - Click **"Add SSL Certificate"**.
   - **Domain Names**: Enter your domain and wildcard subdomain (e.g., `yourdomain.com, *.yourdomain.com`).
   - **Email Address**: Enter your email.
   - **Use a DNS Challenge**: Enable this option.
   - **DNS Provider**: Select **Cloudflare**.
   - **Credentials File Content**: Enter the following:
     ```
     dns_cloudflare_api_token = your_cloudflare_api_token
     ```
     Replace `your_cloudflare_api_token` with the token you generated earlier.
   - Agree to the Let's Encrypt Terms of Service.
   - Click **"Save"**.

   NPM will now attempt to obtain a wildcard SSL certificate for your domain. This process may take a few minutes.

3. **Assign SSL Certificates to Proxy Hosts**:
   - After obtaining the SSL certificate, assign it to your proxy hosts:
     - Navigate to the **"Proxy Hosts"** section.
     - Edit an existing proxy host or add a new one.
     - In the **"SSL"** tab:
       - **SSL Certificate**: Select the wildcard certificate you obtained.
       - **Force SSL**: Enable this option to ensure all traffic uses HTTPS.
       - **HTTP/2 Support**: Enable for improved performance.
       - **HSTS Enabled**: Enable for added security. 


## Step 8: Setting Up Tailscale for Secure Remote Access

**Tailscale** is a zero-configuration Virtual Private Network (VPN) service that connects your devices securely using the WireGuard protocol. It simplifies the process of creating a secure network between your devices, regardless of their location, and is particularly useful for accessing services behind NAT or CGNAT environments.

### Prerequisites

- **Tailscale Account**: If you haven't already, sign up for a free account at [Tailscale](https://tailscale.com/).

### Installation Steps

1. **Install Tailscale on Your Ubuntu System**:
   - Open a terminal on your HP t630 Thin Client.
   - Update your package list:
     ```bash
     sudo apt update
     ```
   - Install the Tailscale package:
     ```bash
     sudo apt install tailscale -y
     ```

2. **Authenticate and Connect Your Device**:
   - Start the Tailscale service:
     ```bash
     sudo tailscale up
     ```
   - This command will provide a URL. Open this URL in your web browser to authenticate and link your HP t630 Thin Client to your Tailscale account.

3. **Configure Tailscale as an Exit Node (Optional)**:
   - If you want to route your internet traffic through your homelab (acting as a VPN), you can set up your HP t630 as an exit node. This is useful for encrypting your internet connection when using public Wi-Fi or accessing geo-restricted content.
   - Enable IP forwarding:
     ```bash
     sudo sysctl -w net.ipv4.ip_forward=1
     ```
   - Advertise the exit node:
     ```bash
     sudo tailscale up --advertise-exit-node
     ```
   - In your Tailscale admin console, authorize your device to be used as an exit node.

4. **Accessing Your Homelab Services Remotely**:
   - With Tailscale running, your devices are part of a secure mesh network.
   - On any device where you're logged into Tailscale, you can access your homelab services using the Tailscale IP address assigned to your HP t630 Thin Client.
   - For example, if Nginx Proxy Manager is set up to manage your services, you can access it via `http://<tailscale-ip>:81`.

### Benefits of Using Tailscale

- **No Port Forwarding Required**: Access your services without modifying router settings.
- **Bypass CGNAT Limitations**: Ideal for ISPs that use CGNAT, which can complicate traditional remote access methods.
- **Secure Connections**: All traffic between devices is encrypted using the WireGuard protocol.
- **Simplified Network Management**: Easily manage device access and permissions through the Tailscale admin console.

By following these steps, you've successfully set up Tailscale to securely access your homelab from anywhere in the world. This configuration ensures that your services remain protected and accessible, regardless of network complexities or ISP restrictions.

Congratulations! You've now built a functional and secure homelab for under $20, accessible from anywhere without the need for complex network configurations. This setup not only provides a platform for learning and experimentation but also offers practical solutions for remote access and service management. 