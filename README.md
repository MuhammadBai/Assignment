# Assignment
Tutorial to create a new SSH Key pair on your local machine

Step 1) 
First you will need to create .ssh directory in your home directory
so the following command to create it:
  *ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"*

the above command have ~(tilde) which is your home directory.
replace "your email address" with your email address.

Go to 2nd step if the above step doesnt work.
Step 2) 
In Windows PowerShell tilde expansion doesnt always work, so you can enter the full and replace your your-user-name with your Windows user name in the following command:
 *ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"*

-t = type (this is the type of encryption used for the key)
-f = filename (specify filename and location)
-C = comment (attaches a comment to a key)

The above command will create two plain text files in the .ssh directory, and you will be able to see the public and private key created:

"do-key" This is your private key.
"do-key.pub" This is your public key. The public key is the one that you copy to your server. 

Once you have an Arch Linux VM(virtual machine) set up you will be able to see the manual pages by typing the following command:
*man ssh-keygen*

Function of ssh-keygen:
ssh-keygen generates, manages and converts authentication keys for ssh(1). ssh-keygen can create keys for use by SSH protocol version 2.

To check whether you can remotely connect to your arch server type the following commands:
Your-user-name you set when creating the account with ssh
*ssh your-user-name*

once you successfully logged into your remote linux server, go to Step 3:

Step 3)
Exit from your remote server by typing exit command 
i.e *exit*

The above step will take you to your home directory:
then from your home directory >> go to .ssh directory by typing the following command:
cd .ssh
 once you are in the .ssh >> type ls to see if the public and private keys are created in your computer it will show you the Name with time

Once it is created you will see the keys with the name you set them. 

Two ways you can copy your public key:
1) you can copy the conents directly from the terminal.
--The commands below are exampes of how you can copy the contents of file to your clipboard from the terminal.

In PowerShell:
*Get-Content C:\Users\your-user-name\.ssh\do-key.pub | Set-Clipboard*
 
For MacOS users:
*pbcopy < ~/.ssh/do-key.pub*

For Linux Users:
*wl-copy < ~/.ssh/do-key.pub*

2) Since the key is in a plain text file you can open it in VSCode and copy it like any other text

To open it in the VSCode, you need to be in your home directory which is not Linux, so after listing the keys you created in .ssh file you list them by typing ls to see the name of your keys i.e public and private keys. 
Type 
*code your-key.pub*
By typing the above command you can copy your public key.

either way 

Step 4)
 Adding the copied public key to the digital ocean account  
 steps to follow:
 1. Go to Settings in menu in the left menu.
 2. Click the Security tab.
 3. Next Click the "Add SSH key" button.
 4. Paste the contents of your public key into 
    the SSH Key box.
 5. Give your key a name. For example for laptop 
    it can be lap-2121, and for desktop desk-2121. 

 Step 5) 
 To create a new droplet:
 Click Create on the top right corner, and select Droplets from the dropdown list. 

 Step 6)
 To choose the appropriate settings for your droplet follow the steps below:
 1. Choose Region = San Francisco
 2. Select Datacenter = SF03
 3. Click "Custom images" to select Arch Linux you uploaded.
 4. Leave the size on "Basic"
 5. Select the $7 option under Premium AMD or $8 option under Premium intel. 
 6. Choose SSH key as an Authentication method that you added to your account previously. 
 7. Change Hostname to something shorter like bcit, you will see this name in your prompt when you are connected to your server.
 leave the rest of the settings as default.

 if everything worked you should see something like the following:
 hostname with is your-hostname
 209.54.23.23.45 is the IP address it will show you with your hostname. 

 Step 7)
 In this step you will be connecting to your droplet via ssh through your command prompt
 
 You can use the following command to connect it the server you created in digitalocean account.

 ssh -i .ssh/do-key arch@your-droplets-ip-address
-i = identify_file, identify file, the path to the private key file.
arch = your username, The image that we used contains a regular user named "arch"

To exit your SSH connect just type exit and press enter.



 



To Add your public key to your DigitalOcean account < you should be able to access it to copy the public key and paste it in your DigitalOcean acount



