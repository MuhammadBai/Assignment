# Assignment

# Tutorial: Creating an SSH Key Pair and Deploying a DigitalOcean Droplet

This tutorial will guide you through creating SSH keys, setting up an Arch Linux Droplet on DigitalOcean, and connecting to it using SSH.

## Step 1: Create an SSH Key Pair on Your Local Machine

**SSH keys**  are a method of securely logging into a server without needing to enter a password. They use cryptographic keys: a **public key** stored on the server and a **private key** stored on your machine. Only a person with the private key can log into the server.

*To generate an SSH key pair on your local machine, open your terminal (or PowerShell on Windows) and run:*

```ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"

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

*Note:
so when we added our SSH key in our first server that we created on the digital ocean console, we added the SSH key to digital ocean and then we selected it, when we created our servers and that gets copied over into our droplet into the .SSH authorized key file. Our server there is a >SSH directory that gets created and authorized key giles that contains a public key, so we would like to have the key added to our server, but we will have to make sure we use different key everytime*


In our first step we will need to create a new SSH key:
**We can do so with the following command, but this time you should make sure its not identical to your existing keys.**

*To generate a key type:*
>`ssh-keygen -t ed25519 -f ~/.ssh/your-key -C "your email address"`

### Breaking Down the Command:
- ssh-keygen: This is the command used to generate SSH keys.
- -t ed25519: Specifies the type of key to create. In this case, it's the Ed25519 key, which is a modern and secure choice.
- -f ~/.ssh/do-key: Specifies the file name and location to save the generated key. It will save it as do-key in the ~/.ssh/ directory.
- -C "your email address": This is an optional comment field, typically used to identify the key, such as associating it with your email.

**Please make sure you replace your-key and your-email-address with your actual username and email address**

## Step 2: Retrieving your public key:

### Why are we retrieving our public key?
We are retrieving the public key because we will be using to our cloud-init config.

*you can display using the following command:*
>`cat ~/.ssh/your-key.pub`

**Replace your key-pub with your actual key name**

## Step 3: Add the public key to your cloud-init YAML file under the ssh-authorized-keys section:

>`ssh-authorized-keys:
> - ssh-ed25519 your-ssh-public-key  # Replace >with the key you retrieved`

## Step 4: open the yaml file into Visual studio code through the terminal with the following command
>`code config.yaml`

### Breakdown of the command:

- `code`: This command is used to open files or directories in *Visual Studio Code* (VS Code), a popular code editor. The `code` command launches VS Code from the terminal.

- `config.yaml`: This is the file you are instructing VS Code to open. In this case, it's a configuration file with the extension `.yaml`, which indicates it's written in YAML (YAML Ain't Markup Language) format, commonly used for configuration files.

*your YAML file can end with YML or YAML*

- **Putting it all together**: The command `code config.yaml` opens the **config.yaml** file in **VS Code**. If the file doesn't exist, VS Code will create it once you save any changes.

**Once our config file is created now we will have to paste our cloud-init configuration that we created...Go to Step 5**

## Step 5: Where to find or Create a Cloud-init File?

The **cloud-init** file is something you’ll either create yourself or use pre-configured templates, depending on your needs. It's used to automate setup tasks like creating users or installing packages on your server during its initial boot. Here’s how you can find or create one:

**1. Check the Official Cloud-Init Docs**

If you’re new to cloud-init, the best place to start is the official [cloud-init documentation](https://cloudinit.readthedocs.io/en/latest/reference/examples.html). There, you'll find plenty of examples showing how to create users, install software, or configure your server automatically when it's first launched.

**2. Using DigitalOcean Custom Images**

If you’re working on DigitalOcean, you’ll see an option to add **User Data** when creating a new Droplet (DigitalOcean’s term for a virtual machine). This is where you can paste your **cloud-config.yaml** file. To do this:

- When you create a Droplet, scroll down to **Advanced Options.**
- In the **User Data** field, paste your cloud-init YAML configuration. This is the file that will be run on your server the moment it boots up.

**3. Using Pre-Configured Templates**

You can find plenty of pre-configured cloud-init templates on GitHub or other repositories. These templates can be good starting points, but you’ll likely need to adjust them for your specific use case (like user creation, package installation, etc.).

**4. Writing Your Own Cloud-Init File**

You can also write your own file from scratch! Here’s a basic template to get you started, which sets up a user and installs some useful packages:


# Cloud-Config YAML Example

The following is an example of a cloud-init YAML configuration file which we recieved it from Nathan's notes:

```yaml
#cloud-config
users:
  - name: user-name  # Replace this with the username you want
    primary_group: user-group  # Choose the group for this user
    groups: wheel
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-ed25519 your-ssh-public-key  # Replace this with your actual SSH public key

packages:
  - ripgrep
  - rsync
  - neovim
  - fd
  - less
  - man-db
  - bash-completion
  - tmux

disable_root: true





