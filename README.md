# AWS EC2 Nginx Portfolio Deployment

## Project Overview

This project demonstrates the deployment of a personal portfolio website on an AWS EC2 instance using Nginx as the web server. The deployment process covers server setup, security configuration, Nginx installation, website hosting, and public accessibility through a web browser.

## Technologies Used

* AWS EC2
* Ubuntu Linux
* Nginx Web Server
* SSH
* HTML, CSS, JavaScript
* Linux Command Line

---

## Architecture

```text
User Browser
      │
      ▼
Public IP / Domain
      │
      ▼
AWS EC2 Instance (Ubuntu)
      │
      ▼
Nginx Web Server
      │
      ▼
Portfolio Website Files
```

---

## Prerequisites

Before starting, ensure you have:

* AWS Account
* EC2 Instance (Ubuntu)
* SSH Key Pair (.pem file)
* Portfolio Website Files
* Basic Linux Knowledge

---

## Step 1: Launch an EC2 Instance

1. Login to AWS Management Console.
2. Navigate to EC2 Dashboard.
3. Click **Launch Instance**.
4. Select:

   * Ubuntu Server (Latest LTS)
   * t2.micro (Free Tier Eligible)
5. Create or select an existing key pair.
6. Configure Security Group:

   * SSH (Port 22)
   * HTTP (Port 80)
   * HTTPS (Port 443)
7. Launch the instance.

---

## Step 2: Connect to EC2

```bash
ssh -i your-key.pem ubuntu@your-public-ip
```

Example:

```bash
ssh -i portfolio-key.pem ubuntu@13.234.xx.xx
```

---

## Step 3: Update the Server

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 4: Install Nginx

```bash
sudo apt install nginx -y
```

Check status:

```bash
sudo systemctl status nginx
```

Enable Nginx:

```bash
sudo systemctl enable nginx
```

---

## Step 5: Allow HTTP Traffic

```bash
sudo ufw allow 'Nginx Full'
```

Verify:

```bash
sudo ufw status
```

---

## Step 6: Upload Portfolio Files

Navigate to Nginx web root:

```bash
cd /var/www/html
```

Remove default files:

```bash
sudo rm index.nginx-debian.html
```

Copy portfolio files:

```bash
sudo cp -r ~/portfolio/* /var/www/html/
```

Set permissions:

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

---

## Step 7: Restart Nginx

```bash
sudo systemctl restart nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

## Step 8: Access Website

Open your browser and visit:

```text
http://your-public-ip
```

Example:

```text
http://13.234.xx.xx
```

Your portfolio website should now be live.

---

## Nginx Configuration (Optional)

Create a custom server block:

```bash
sudo nano /etc/nginx/sites-available/portfolio
```

Configuration:

```nginx
server {
    listen 80;
    server_name your-domain.com;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Enable configuration:

```bash
sudo ln -s /etc/nginx/sites-available/portfolio /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

## Project Outcomes

* Successfully deployed a static portfolio website.
* Configured AWS EC2 instance.
* Installed and managed Nginx web server.
* Learned Linux server administration basics.
* Hosted a website accessible over the internet.

---

## Troubleshooting

### Nginx Not Running

```bash
sudo systemctl restart nginx
sudo systemctl status nginx
```

### Website Not Accessible

* Check Security Group rules.
* Verify Port 80 is open.
* Confirm Nginx is active.

### Check Nginx Logs

```bash
sudo tail -f /var/log/nginx/error.log
```

---

## Future Enhancements

* Configure HTTPS using Let's Encrypt SSL.
* Connect a custom domain.
* Automate deployment using CI/CD.
* Deploy using Docker containers.
* Implement monitoring and logging.

---

## Author

**Omkar Dhamdhere**

Aspiring Cloud & DevOps Engineer

### Connect

* LinkedIn: Add your LinkedIn profile
* GitHub: Add your GitHub profile

---

## License

This project is open-source and available under the MIT License.
