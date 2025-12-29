# Day 14 — Create Key Pair (AWS)

## Task Description 

The Nautilus DevOps team is working on setting up secure SSH access for their virtual machines in Azure. One of the requirements is to add the SSH public key of the root user from the Azure client host (landing host) to the nautilus-vm Azure VM's authorized_keys file. This ensures secure and password-less SSH access to the VM.

Task Details:
1) VM Details:

The VM is named nautilus-vm and is running in the West US region. The default SSH user is azureuser — use this user to connect to the VM.
You need to add the root user's SSH public key from the Azure client host to the authorized_keys file of the VM's root user.
The SSH public key of the root user on the Azure client host is located at /root/.ssh/id_rsa.pub.
2) Public Key Addition:

Copy the public key located at /root/.ssh/id_rsa.pub on the Azure client host to the authorized_keys file of the root user on nautilus-vm.
Ensure that the proper permissions for the .ssh folder and authorized_keys file are set on the VM.
3) Verification:

After adding the public key, make sure that you are able to SSH into the nautilus-vm VM as the root user from the Azure client host without needing a password.
Important Notes:
Ensure that the VM is up and running before attempting to SSH.
You may need to adjust the firewall or security group rules for the VM to allow SSH access.

## Solution:

To complete the task of enabling passwordless root SSH access to nautilus-vm (West US region, public IP 20.57.197.169, default user azureuser) from the Azure client host's root account, the process addressed permission issues, key transfer failures, redirection errors, and SSH config restrictions through these precise steps.

# 1. VM Details
Confirmed VM identity: nautilus-vm in West US region with public IP 20.57.197.169 (extracted from SSH debug: "Connecting to 20.57.197.169 [20.57.197.169] port 22").

Verified baseline access: ssh azureuser@20.57.197.169 works from client host (evident from successful azureuser sessions during troubleshooting).

Identified client host key location: /root/.ssh/id_rsa.pub on separate Azure client host (not on VM), RSA SHA256:kci2J7726nccthefCRhHLiKRrjU0J9GtLnsI381YxGI (from SSH debug).

# 2. Public Key Addition
Key Transfer: sudo scp /root/.ssh/id_rsa.pub azureuser@20.57.197.169:/tmp/root_id_rsa.pub (from client host) - Copied client root public key to VM /tmp/ (fixed "No such file" errors from prior failed nested SSH attempts).

Directory Setup: sudo mkdir -p /root/.ssh && sudo touch /root/.ssh/authorized_keys && sudo chown -R root:root /root/.ssh && sudo chmod 700 /root/.ssh && sudo chmod 600 /root/.ssh/authorized_keys (on VM) - Created .ssh dir (700 perms), file (600 perms), root ownership to satisfy SSH strict mode.

Key Append: sudo tee -a /root/.ssh/authorized_keys < /tmp/root_id_rsa.pub && sudo rm /tmp/root_id_rsa.pub (on VM) - Appended key content as root (fixed sudo cat >> redirection permission denied), removed temp file.

Remove Forced Command: sudo nano /root/.ssh/authorized_keys (on VM) - Deleted command="sudo -u azureuser /bin/bash" pty user-rc prefix from line 1 (identified in debug: "Remote: /root/.ssh/authorized_keys:1: key options: command pty user-rc"), leaving clean ssh-rsa AAAAB3NzaC1yc2E... key.

SSH Config: sudo sed -i 's/^#*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && sudo sed -i 's/^#*PubkeyAuthentication.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config && sudo sshd -t && sudo systemctl restart sshd (on VM) - Enabled root login (handled commented/uncommented lines), verified syntax, restarted service.

# 3. Verification
Debug Test: ssh -v root@20.57.197.169 (from client host) - Confirmed: key offered ("Offering public key: /root/.ssh/id_rsa RSA SHA256:..."), accepted ("Server accepts key"), authentication succeeded ("Authentication succeeded (publickey)"), no more "Please login as azureuser" message, direct root shell granted (exit status resolved from 142 to success).

Key Match: Client /root/.ssh/id_rsa fingerprint matched VM authorized_keys (SHA256:kci2J7726nccthefCRhHLiKRrjU0J9GtLnsI381YxGI from debug).

Final Check: sudo cat /root/.ssh/authorized_keys (on VM) shows single clean public key line; sudo tail /var/log/auth.log shows no permission/rejection errors during tests.
