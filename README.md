# Tinyuka-Exam-Project1
Second Semester Exam Project process detailing


STEPS

1) Launched an EC2 instance on AWS
Operating system Ubuntu Server 24.04 LTS
Instance Type: t2.micro (free tier eligible)

**Security Group**:
- Allowed SSH (port 22)
- Allowed HTTP (port 80)
- Allowed HTTPS (port 443)
connected via SSH through SSH terminal "Termius" using my exixting key pair
**bash**:
ssh -i "london-key-01.pem" ubuntu@ec2-18-170-215-88.eu-west-2.compute.amazonaws.com

3) WEB SERVER SETUP
*firewall setup*
**UFW ALLOW**:
port 22
port 80
port 443

Apache Installation
**bash**:
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
Node Js Installation 
  
**bash**:
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
  
Created a basic app: app.js  in home directory
  
**bash**:
nano app.js
 
**script**:
const http = require('http');
const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/html' });
  res.end('<h1>Hello from Node.js backend!</h1>');
});

server.listen(8080, () => {
  console.log('Server running on http://localhost:8080');
});


3) Replaced Default Web Root:
   Added my html file to /var/www/html

**bash**:
sudo rm -r /var/www/html/index.html
sudo nano /var/www/html/index.html
*pasted my HTML code into nano and saved the file*
*repeated the same process for my CSS file.*

4) Point Domain to EC2 IP
On Namecheap:
My already existing Domain: cloudhorse.space

Go to Domain List > Manage > Advanced DNS

*Created an A Record:*
Host: @
Value: my ec2 instance Public ip 

TTL: set to Automatic

*Waited for DNS propagation (about 20 minutes approx).*

5) Installed SSL with Let’s Encrypt

**bash**
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache -d cloudhorse.space -d www.cloudhorse.space
*followed the Onscreen instruction process*

6)   Launched www.cloudhorse.space on a browser

Here is a screenshot of the rendered page in a browser 

![Screenshot ](https://github.com/user-attachments/assets/6b6024ec-0737-4012-93da-9269ee7d61ba)

  
    
    
