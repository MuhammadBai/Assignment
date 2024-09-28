# Assignment

# Tutorial: Creating an SSH Key Pair and Deploying a DigitalOcean Droplet

This tutorial will guide you through creating SSH keys, setting up an Arch Linux Droplet on DigitalOcean, and connecting to it using SSH.

## Step 1: Create an SSH Key Pair on Your Local Machine

To create a new SSH key pair, run the following command in your terminal:


ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"

`~`: Refers to your home directory.
Replace `"your email address"` with your actual email.

If you're on Windows, PowerShell might not recognize the `~`. In this case, use the full path:

`ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"`


`-t`: Specifies the type of key (ed25519 is recommended).
`-f`: Specifies the filename and location.
`-C`: Adds a comment (optional but useful for identification).

This command will generate two files:
`do-key` (private key)
`do-key.pub` (public key)

##Step 2: Accessing the Manual Pages
To learn more about `ssh-keygen`, you can access the manual pages on your Arch Linux VM by running:
`man ssh-keygen`

This provides detailed information about the `ssh-keygen` tool.

##Step 3: Verify Connection to Your Droplet
Once you have set up your Arch Linux Droplet, check if you can connect remotely using SSH:
`ssh your-user-name@your-droplets-ip-address`

Replace `your-user-name` and `your-droplets-ip-address` with your actual username and IP.

To exit the remote connection, use:
`exit`

##Step 4: Copy Your Public Key

After generating the SSH keys, you need to copy your public key. There are two ways to do this:

###Method 1: Using Terminal Commands
Windows (PowerShell):
`Get-Content C:\Users\your-user-name\.ssh\do-key.pub | Set-Clipboard`

MacOS:
`pbcopy < ~/.ssh/do-key.pub`

Linux:
`wl-copy < ~/.ssh/do-key.pub`

###Method 2: Using a Text Editor
You can also open the `.pub` file in a text editor (like VS Code) and copy it manually. Navigate to your `.ssh` directory and use:
`code ~/.ssh/do-key.pub`

##Step 5: Add Your SSH Key to DigitalOcean
1. Log into your DigitalOcean account.
2. Go to Settings from the left-hand menu.
3. Click the Security tab.
4. Select Add SSH Key.
5. Paste the content of your public key into the provided field.
6. Give your key a recognizable name (e.g.,`laptop-ssh-key`).

##Step 6: Create a New Droplet on DigitalOcean
1. Click Create on the top-right corner of the DigitalOcean dashboard and choose Droplets.
2. Select Arch Linux from the Custom Images tab.
3. Choose the Region (e.g., San Francisco).
4. Select Datacenter SF03.
5. Choose Basic for the Droplet size, and select the $7 (AMD) or $8 (Intel) option.
6. Under Authentication, select the SSH key you previously added.
7. Optionally, change the hostname to something short, like bcit.

If everything is set up correctly, you’ll be provided with an IP address for your Droplet.

##Step 7: Connect to Your Droplet via SSH
Now, connect to your Arch Linux Droplet by running the following command:
`ssh -i ~/.ssh/do-key arch@your-droplets-ip-address`

`-i`: Specifies the identity file (your private key).
`arch`: The default username for the Arch Linux image.

To exit the SSH session, simply type:
`exit`















