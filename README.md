# Assignment

# Tutorial: Creating an SSH Key Pair and Deploying a DigitalOcean Droplet

This tutorial will guide you through creating SSH keys, setting up an Arch Linux Droplet on DigitalOcean, and connecting to it using SSH.

## Step 1: Create an SSH Key Pair on Your Local Machine

**SSH keys**  are a method of securely logging into a server without needing to enter a password. They use cryptographic keys: a public key stored on the server and a private key stored on your machine. Only a person with the private key can log into the server.

*To generate an SSH key pair on your local machine, open your terminal (or PowerShell on Windows) and run:*


>`ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"`

`~`: Refers to your home directory.This is where the key will be stored by default unless you specify a different location.
Replace `"your email address"` with your actual email. This email will be embedded in the public key as a comment, which is useful for identifying the key.

Breakdown of the Command:
`ssh-keygen`: This is the command used to generate SSH keys.<br>
`-t ed25519`: Specifies the type of key to generate. Ed25519 is a modern, faster, and more secure option than RSA and is recommended for most cases.<br>
`-f ~/.ssh/do-key`: Specifies the filename and location where the key files will be saved.<br>
`~/.ssh/`: The default folder where SSH keys are stored.<br>
`do-key`: The name of the key file.<br>
`-C "your email address"`: Adds a comment to the key, often used for identifying the key with your email.

If you're on Windows, PowerShell might not recognize the `~`. In this case, use the full path:

`ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"`


`-t`: Specifies the type of key (ed25519 is recommended).

`-f`: Specifies the filename and location.

`-C`: Adds a comment (optional but useful for identification).

After running the command, two files will be generated in your .ssh folder:

`do-key` (your private key): This must be kept safe and secure on your local machine.
`do-key.pub` (your public key): This will be shared with DigitalOcean to authenticate your connection.

## Why SSH Keys Are Important:
Using SSH keys is much more secure than traditional password-based authentication, as they prevent brute-force attacks. With SSH keys, the server only accepts logins from machines that possess the corresponding private key.

## Step 2: Accessing the Manual Pages
To learn more about the `ssh-keygen` command and its various options, you can access the manual pages directly from your terminal. On your Arch Linux VM, run:
`man ssh-keygen`

This will open a detailed manual explaining all the parameters and functions available with the `ssh-keygen` tool.

## Step 3: Verify Connection to Your Droplet
Once your Arch Linux Droplet is set up, you can test the connection by trying to SSH into your server. Use the following command:
`ssh your-user-name@your-droplets-ip-address`

`your-user-name`: Replace this with the username on your server (default is usually root or `arch` for Arch Linux).
`your-droplets-ip-address`: Replace this with the IP address of your DigitalOcean Droplet.

This command will initiate an SSH connection. If everything is configured properly, you’ll be connected to your Droplet.

To exit the remote connection, use:
`exit`

## Step 4: Copy Your Public Key

To connect to your Droplet via SSH, you need to provide DigitalOcean with your public key. There are two ways to copy the public key to your clipboard:

### Method 1: Using Terminal Commands
Windows (PowerShell):
`Get-Content C:\Users\your-user-name\.ssh\do-key.pub | Set-Clipboard`

MacOS:
`pbcopy < ~/.ssh/do-key.pub`

Linux:
`wl-copy < ~/.ssh/do-key.pub`

These commands will copy the contents of your public key file (do-key.pub) to your clipboard so you can paste it into DigitalOcean.

### Method 2: Using a Text Editor
Alternatively, you can manually copy the public key by opening it in a text editor. If you’re using VS Code, run the following command to open the public key file:
`code ~/.ssh/do-key.pub`

Once opened, select and copy the entire key.

## Step 5: Add Your SSH Key to DigitalOcean
1. Log into your DigitalOcean account.
2. Go to Settings from the left-hand menu.
3. Click the Security tab.
4. Select Add SSH Key.
5. Paste the content of your public key into the provided field.
6. Give your key a recognizable name (e.g.,`laptop-ssh-key`).

Adding your SSH key here will allow you to authenticate securely when creating new Droplets.

## Step 6: Create a New Droplet on DigitalOcean
Now, let's create your new server (Droplet) on DigitalOcean.

1. From the DigitalOcean dashboard, click Create on the top-right corner and select Droplets.
2. Choose Arch Linux from the Custom Images tab.
3. Select the Region where you want your Droplet to be hosted (e.g., San Francisco).
4. Choose Datacenter SF03 as the specific data center.
5. Under Droplet Size, select Basic and pick the $7 (AMD) or $8 (Intel) option, depending on your preference.
6. Under Authentication, choose the SSH key you added earlier.
7. Optionally, change the hostname to something short and memorable, like `bcit`.

After completing these steps, you will receive an IP address for your new Droplet. Keep this IP address handy, as you will need it to connect to your Droplet via SSH.

## Step 7: Connect to Your Droplet via SSH
Once your Droplet is created, use the following command to connect via SSH:
`ssh -i ~/.ssh/do-key arch@your-droplets-ip-address`

`-i ~/.ssh/do-key`: Specifies the identity file (your private key) that should be used for authentication.
`arch`: The default username for Arch Linux Droplets.
Replace `your-droplets-ip-address` with the actual IP of your server.

To exit the SSH session, simply type:
`exit`

### Important Note:
By following this guide, you have successfully created an SSH key pair, added it to your DigitalOcean account, and deployed a new Arch Linux Droplet. You can now securely connect to your server using SSH without needing a password. This setup ensures that your server is secure and only accessible from your machine.

Remember to keep your private key safe, and never share it with anyone!














