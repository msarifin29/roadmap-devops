## Deploy Next.js app using Vagrant

### Step 1: Set Up Vagrant
1. Create a new directory for your Vagrant project:
   ```bash
   mkdir nextjs-vagrant
   cd nextjs-vagrant
   ```
2. Initialize a new Vagrantfile:
   ```bash
   vagrant init
   ```
3. Edit the `Vagrantfile` to configure your VM
   ```bash
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/focal64" # Ubuntu 20.04 LTS
     config.vm.network "private_network", ip: "192.168.33.10" # Replace with your Vagrant private IP
     config.vm.provider "virtualbox" do |vb|
       vb.memory = "1024"
     end
   end
   ```
4. Start the Vagrant VM
   ```bash
   vagrant up
   ```
5. SSH into the VM
   ```bash
   vagrant ssh
   ```

### Step 2: Install Dependencies on the VM
1. Update the package list
   ```bash
   sudo apt update
   ```
2. Install Node.js (for running the Next.js app)
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   source ~/.profile
   nvm ls-remote
   nvm install 20.18.2
   node -v
   sudo npm install -g pm2
   ```
3. Install PM2 (process manager for Node.js apps)
   ```bash
   sudo npm install -g pm2
   ```
4. Install Nginx
   ```bash
   sudo apt install nginx -y
   ```

### Step 3: Next.js App
create simple next.js app inside nextjs-vagrant `directory`

### step 4 :  Update the Vagrantfile and  Reload VM
1. Update `Vagrantfile` to configure  `config.vm.synced_folder` line to point to the correct path
   ```bash
   nano Vagrantfile
   config.vm.synced_folder "./project-name", "/var/www/project-name"
   ```
   - `"./project-name"` is the relative path to the project directory from the location of the Vagrantfile.
 
   - `"/var/www/project-name"` is the absolute path on the VM where the folder will be synced.
2. Reload the Vagrant VM to apply the changes
   ```bash
   vagrant reload
   ```
3. Verify the Synced Folder
   ```bash
   vagrant ssh
   cd /var/www/project-name
   ls
   ```
   You should see your Next.js project files (e.g., `package.json`, n`ext.config.js`, etc.)

### Step 5 : Build and Deploy the Next.js App
1. Navigate to the synced project directory:
   ```bash
   cd /var/www/project-name
   ```
2. Install dependencies
   ```bash
   npm install
   ```
3. npm run build
   ```bash
   npm run build
   ```
4. Start the app using PM2
   ```bash
   pm2 start npm --name "project-name" -- start
   ```
5. Save the PM2 process list so it starts on reboot
   ```bash
   pm2 save
   pm2 startup
   ```

### Step 6 : Configure Nginx as a Reverse Proxy
1. Create a new Nginx configuration file for your app
   ```bash
   sudo nano /etc/nginx/sites-available/project-name
   ```
2. Add configuration
   ```
   server {
       listen 80;
       server_name 192.168.33.10; # Replace with your Vagrant private IP
   
       location / {
           proxy_pass http://localhost:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```
3. Enable the configuration by creating a symbolic link
   ```bash
   sudo ln -s /etc/nginx/sites-available/project-name /etc/nginx/sites-enabled/
   ```
4. Test the Nginx configuration
   ```bash
   sudo nginx -t
   ```
5. Restart Nginx
   ```bash
   sudo systemctl restart nginx
   ```

### Step 7: Access Your Next.js App
1. Open your browser and navigate to http://192.168.33.10 (or the private IP you configured in the Vagrantfile).

2. Your Next.js app should now be live and served via Nginx