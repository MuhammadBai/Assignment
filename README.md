# Assignment

# Tutorial: Creating an SSH Key Pair and Deploying a DigitalOcean Droplet

This tutorial will guide you through creating SSH keys, setting up an Arch Linux Droplet on DigitalOcean, and connecting to it using SSH.

## Step 1: Create an SSH Key Pair on Your Local Machine

**SSH keys**  are a method of securely logging into a server without needing to enter a password. They use cryptographic keys: a **public key** stored on the server and a **private key** stored on your machine. Only a person with the private key can log into the server.

*To generate an SSH key pair on your local machine, open your terminal (or PowerShell on Windows) and run:*

>`ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"`

Breakdown of the Command:<br>
- `ssh-keygen`: This is the command used to generate SSH keys.<br>
- `-t ed25519`: Specifies the type of key to generate. Ed25519 is a modern, faster, and more secure option than RSA and is recommended for most cases.<br>
- `-f ~/.ssh/do-key`: Specifies the filename and location where the key files will be saved.<br>
- `~/.ssh/`: The default folder where SSH keys are stored.<br>
- `do-key`: The name of the key file.<br>
- `-C "your email address"`: Adds a comment to the key, often used for identifying the key with your email.
- `~`: Refers to your home directory.This is where the key will be stored by default unless you specify a different location.<br>
- Replace `"your email address"` with your actual email. This email will be embedded in the public key as a comment, which is useful for identifying the key.

>If you're on Windows, replace the path `~/.ssh/` >with the full path to your SSH directory, such >as `C:\Users\your-user-name\.ssh\do-key`.

>`ssh-keygen -t ed25519 -f >C:\Users\your-user-name\.ssh\do-key -C >"youremail@email.com"`


- `-t`: Specifies the type of key (ed25519 is recommended).<br>
- `-f`: Specifies the filename and location.<br>
- `-C`: Adds a comment (optional but useful for identification).

### Output:
After running the command, two files will be generated in your .ssh folder:

- `do-key` (your private key): This must be kept safe and secure on your local machine.<br>
- `do-key.pub` (your public key): This will be shared with DigitalOcean to authenticate your connection.

## Why SSH Keys Are Important:
Using SSH keys is much more secure than traditional password-based authentication, as they prevent brute-force attacks. With SSH keys, the server only accepts logins from machines that possess the corresponding private key.

## Step 2: Understanding SSH and `ssh-keygen` 
To learn more about the `ssh-keygen` command and its various options, you can access the manual pages directly from your terminal.<br> On your Arch Linux VM, run:<br>
>`man ssh-keygen`

This will open a detailed manual explaining all the parameters and functions available with the `ssh-keygen` tool.

## Step 3: Verifying your connection to the Droplet
Once your Arch Linux Droplet is set up, you can test the connection by trying to SSH into your server. <br>Use the following command:
>`ssh your-user-name@your-droplets-ip-address`

- `your-user-name`: Replace this with the username on your server (default is usually root or `arch` for Arch Linux).<br>
- `your-droplets-ip-address`:The IP address assigned to your DigitalOcean Droplet.replace this with the IP address of your DigitalOcean Droplet.

This command will initiate an SSH connection. If everything is configured properly, you’ll be connected to your Droplet.

To log out from the remote connection, use:
>`exit`

## Step 4: Copy Your Public Key

To connect to your Droplet via SSH, you need to provide DigitalOcean with your public key. There are two ways to copy the public key to your clipboard:

### Method 1: Using Terminal Commands
- Windows (PowerShell):
>`Get-Content C:\Users\your-user-name\.ssh\do-key.>pub | Set-Clipboard`

- MacOS:
>`pbcopy < ~/.ssh/do-key.pub`

- Linux:
>`wl-copy < ~/.ssh/do-key.pub`

These commands will copy the contents of your public key file (do-key.pub) to your clipboard so you can paste it into DigitalOcean.

### Method 2: Using a Text Editor
Alternatively, you can manually copy the public key by opening it in a text editor. If you’re using VS Code, run the following command to open the public key file:
>`code ~/.ssh/do-key.pub`<br>
Copy the entire contents of the `.pub` file. This is your public key.

## Step 5: Adding Your SSH Key to DigitalOcean
1. Log into your DigitalOcean account.
2. Go to **Settings** from the left-hand menu.
3. Click the **Security** tab.
4. Select **Add SSH Key**.
5. Paste the content of your public key into the provided field.
6. Give your key a recognizable name (e.g.,`laptop-ssh-key`).

Adding your SSH key here will allow you to authenticate securely when creating new Droplets.

## Step 6: Creating a New Droplet on DigitalOcean
Now, let's create your new server (Droplet) on DigitalOcean.<br>

*Before we get started..*<br>
A **Droplet** is a virtual private server (VPS) on DigitalOcean. Here’s how to create one running Arch Linux:

From the DigitalOcean dashboard, 

1. click **Create** on the top-right corner and select **Droplets**.
2. Under **Custom Images**, select **Arch Linux**.
3. Select the Region where you want your Droplet to be hosted (e.g., **San Francisco**).
4. Select **Datacenter SF03** as the specific data center.
5. Under **Droplet Size**, select **Basic** and pick the $7 (AMD) or $8 (Intel) option, depending on your preference.
6. Under **Authentication**, choose the SSH key you added earlier.
7. Optionally, change the hostname to something short and memorable, like `bcit`.

After completing these steps, DigitalOcean will generate an IP address for your new Droplet. Save this IP, as it will be needed for future SSH connections.

## Step 7: Connect to Your Droplet via SSH
Once your Droplet is created, use the following command to connect via SSH:
>`ssh -i ~/.ssh/do-key >arch@your-droplets-ip-address`

- `-i ~/.ssh/do-key`: Specifies the identity file (your private key) that should be used for authentication.
- `arch`: The default username for Arch Linux Droplets.
- Replace `your-droplets-ip-address` with the actual IP of your server.

To exit the SSH session, simply type:
>`exit`

### Additional Notes for Beginners
- What is SSH?<br>
SSH (Secure Shell) is a way to connect to another computer over the internet in a secure way. It lets you control and manage that computer remotely, which is really useful for tasks like managing servers. Instead of using passwords, SSH often uses special cryptographic keys to make sure only authorized users can access the system.

- What is a Droplet?<br>
A Droplet is like your own personal computer, but it's hosted in the cloud. DigitalOcean provides these virtual machines that you can use to run websites, apps, or any other services. You can think of it as a server that you can easily set up and control through their platform.

- What is Arch Linux?<br>
Arch Linux is a type of operating system that's known for being lightweight and super customizable. It's perfect for people who want more control over how their system works. Arch is popular with advanced users because it’s simple at its core but allows for a lot of flexibility when setting things up.

### Conclusion
By following this guide, you’ve successfully:

- Created an SSH key pair to securely log into remote servers.
- Added the public key to DigitalOcean for authentication.
- Created and connected to an Arch Linux Droplet via SSH.<br>

This setup improves security by using SSH keys instead of passwords. Keep your private key safe and do not share it. If you need to perform administrative tasks on your server, you can now do so remotely from your local machine.

Remember to keep your private key safe, and never share it with anyone!

## Use a Cloud-init Configuration File to Automate Setup Tasks

### What is Cloud-Init?

Cloud-init is used to automate the initial configuration of cloud instances (like servers or virtual machines) when they are first launched. it is widely used in cloud environments (e.g.,AWS, Azure, DigitalOcean). It is especially useful for cloud environments where you might need to spin up multiple servers quickly.

When you create a server, cloud-init runs a special script (a configuration file) that can do things like:

- Automatically create users
- Install software packages
- Set up SSH keys for secure access
- perform other tasks you would typically do manually

### Why Configure Tasks with Cloud-init?

When we use cloud-int it saves a lot of time by automatinf these repetitive tasks. Instead of logging in to each new server and manually setting things up, you can write a cloud-init configuration file and which is usually is YAML(YML) format, and it will handle things for you.

For example, if you want to create a new user, install essential software, or add your SSH key, you can just define that in the configuration file, and cloud-init will take care of the rest when the server starts. This is especially useful when working with many servers or if you want to ensure consistency in your setups.

*Suppose you have 10 servers to setup, and we are making a SSH connection to all those server which will be a tedious task. time consuming tasks such as conencting to them, installing the software repetitively. it is fine to do it for one or two servers, but it will take our a lot of time doing the same configuration for each server. To make this easier, we will rather make a config file that uses cloud-init which is easier to reproduce you just copy cloud-init confuguration and paste it into you cloud config file*

*cloud-init comes with every linux distribution this file is usually written in YAML which is easier to read than JSON file*

## Step 1: Creating a new SSH key for cloud-init server:











