## Configure web servers using Nginx

### Required Installation
  - [VirtualBox](https://www.virtualbox.org/)
  - [Vagrant](https://www.vagrantup.com/)

## 1.  Set Up Vagrant
   - #### Create a Vagrant Project
   ```bash
   mkdir vagrant-project
   cd vagrant-project
   vagrant init bento/ubuntu-22.04
   ```

   - #### Update the Vagrantfile:
   Open the Vagrantfile and add the following configuration:
   
   ```bash
     # Forward port 80 on the VM to port 8080 on the host
     config.vm.network "forwarded_port", guest: 80, host: 8080
     
     # Assign a private network IP (optional)
     config.vm.network "private_network", ip: "192.168.33.10"
     
     # Sync a folder from the host to the VM
     config.vm.synced_folder "./www", "/var/www/html"
   ```
   - #### Create the Shared Folder
   Create a folder named www in your project directory
   ```bash
   mkdir www
   ```
   - #### Start Vagrant VM
     ```bash
     vagrant up
     ```
     notes: "if you get error , replace `ip` `private_network` in `Vagrantfile` with Ranges in your error message."
   
   - #### SSH into the VM
     ```bash
     vagrant ssh
     ```

## 2. Install Nginx
   - #### Update and Install Nginx
     ```bash
     sudo apt update
     sudo apt install nginx -y
     ```
   
   -  #### Start and Enable Nginx
      ```bash
      sudo systemctl start nginx
      sudo systemctl enable nginx
      ```
      
      - #### Verify Nginx is Running
      ```bash
      sudo systemctl status nginx
      ```

## 3. Serve a Basic HTML File
   - #### Create a Test HTML File
     On your host machine, create a file named index.html in the www folder:
     ```bash
     cd www
     nano index.html
     <h1>Hello, World!</h1>
     ```
   
   - #### Verify the File in the VM
     Inside the VM, check the shared folder:
     ```bash
     ls /var/www/html
     ```
   
   - #### Access the File in Your Browser:
     Open your browser and navigate to:
     ```bash
     http://localhost:8080/index.html
     ```

## 4. Enable HTTPS (optional)
   - #### Update the Vagrantfile
     Open the Vagrantfile and add the following configuration:
     ```bash
       # Forward port 443 (HTTPS) to the host
       config.vm.network "forwarded_port", guest: 443, host: 8443
     ```
     and restart VM
     ```bash
     vagrant reload
     ```
   
   - #### Generate a Self-Signed SSL Certificate
     SSH into the VM
     ```bash
     vagrant ssh
     ```
     
     Inside the VM, run the following commands:
     ```bash
     sudo mkdir -p /etc/nginx/ssl
     ```
     ```bash
     sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
       -keyout /etc/nginx/ssl/selfsigned.key \
       -out /etc/nginx/ssl/selfsigned.crt \
       -subj "/C=US/ST=State/L=City/O=Organization/OU=Unit/CN=localhost"
     ```
       - This creates a private key (`selfsigned.key`) and a self-signed certificate (`selfsigned.crt`).
       - The `-subj` flag provides dummy values for the certificate fields.
   
   - #### Configure Nginx to Use the Certificate:
     Open the default Nginx configuration file:
     ```bash
     server {
         listen 80;
         server_name _;
         return 301 https://$host$request_uri; # Redirect HTTP to HTTPS
     }
     
     server {
         listen 443 ssl;
         server_name _;
     
         ssl_certificate /etc/nginx/ssl/selfsigned.crt;
         ssl_certificate_key /etc/nginx/ssl/selfsigned.key;
     
         root /var/www/html;
         index index.html;
     
         location / {
             try_files $uri $uri/ =404;
         }
     }
     ```

   - #### Test the Nginx Configuration
     ```bash
     sudo nginx -t
     ```
     
   - #### Restart Nginx
     ```bash
     sudo systemctl restart nginx
     ```

## 5. Access HTTPS in Your Browser

   - #### Open Your Browser:
     Navigate to:
     ```bash
     http://localhost:8080/index.html
     ```
   - #### Bypass the Browser Warning
     - Since the certificate is self-signed, your browser will show a warning.
     - In Chrome/Firefox, click *Advanced* → *Proceed to localhost (unsafe)*.

## 6. Clean Up
   When you're done, you can destroy the VM:
   ```bash
   vagrant destroy
   ```