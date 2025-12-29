# Day 13: SSH into an Azure Virtual Machine

## Task Description 

The Nautilus DevOps team is working on setting up secure SSH access for their virtual machines in Azure. One of the requirements is to add the SSH public key of the root user from the Azure client host (landing host) to the nautilus-vm Azure VM's authorized_keys file. This ensures secure and password-less SSH access to the VM.

Task Details:

# 1) VM Details:
The VM is named nautilus-vm and is running in the West US region. The default SSH user is azureuser — use this user to connect to the VM.
You need to add the root user's SSH public key from the Azure client host to the authorized_keys file of the VM's root user.
The SSH public key of the root user on the Azure client host is located at /root/.ssh/id_rsa.pub.

# 2) Public Key Addition:
Copy the public key located at /root/.ssh/id_rsa.pub on the Azure client host to the authorized_keys file of the root user on nautilus-vm.
Ensure that the proper permissions for the .ssh folder and authorized_keys file are set on the VM.

# 3) Verification:
After adding the public key, make sure that you are able to SSH into the nautilus-vm VM as the root user from the Azure client host without needing a password.
Important Notes:
Ensure that the VM is up and running before attempting to SSH.
You may need to adjust the firewall or security group rules for the VM to allow SSH access.

# Solution :

To complete the task of enabling passwordless root SSH access to nautilus-vm from the Azure client host, the process involved confirming VM details, copying the client host's root public key to the VM, and verifying connectivity after fixing authentication restrictions.

# 1. VM Details
Identified nautilus-vm in West US region with default SSH user azureuser and public IP 20.57.197.169 (visible in debug output and prior commands).

Confirmed SSH access works as azureuser from client host, establishing baseline connectivity before root modifications.

# 2. Public Key Addition
sudo scp /root/.ssh/id_rsa.pub azureuser@20.57.197.169:/tmp/root_id_rsa.pub (from client host): Transferred root public key to VM's /tmp.

sudo mkdir -p /root/.ssh && sudo touch /root/.ssh/authorized_keys && sudo chown root:root /root/.ssh /root/.ssh/authorized_keys && sudo chmod 700 /root/.ssh && sudo chmod 600 /root/.ssh/authorized_keys (on VM): Created .ssh directory and file with strict permissions.

sudo tee -a /root/.ssh/authorized_keys < /tmp/root_id_rsa.pub && sudo rm /tmp/root_id_rsa.pub (on VM): Appended key content as root and cleaned up temp file.

sudo nano /root/.ssh/authorized_keys (on VM): Edited to remove forced command="sudo -u azureuser /bin/bash" prefix that blocked direct root access.

sudo sed -i 's/^#*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && sudo systemctl restart sshd (on VM): Enabled root login and restarted SSH service.

# 3. Verification
ssh -v root@20.57.197.169 (from client host): Confirmed key offer (Offering public key), acceptance (Server accepts key), and successful authentication, resolving the "Please login as azureuser" restriction.
