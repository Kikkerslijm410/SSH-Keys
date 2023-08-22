# SSH-Keys
Documentation about using SSH keys for Bitbucket on Linux
SSH Keys

NOTES BEFOREHAND:
-THis is for Linux
-Do everything in the terminal (Linux Terminal: Ctrl + Alt + T)

STEP 1: 
-Downloading SSH Agent 
sudo apt update && sudo apt install openssh-client

-Check if SSH Agent is downloaded
ssh -V

STEP 2
-Starting SSH Agent
eval `ssh-agent -s`

-Check if SSH Agent is running:
ps -auxc | grep ssh-agent

-Output (similar to):
myusername      3291  0.0  0.0   6028   464 ?        Ss   07:29   0:00 ssh-agent
myusername      3291  0.0  0.0   6028   464 ?        Ss   07:29   0:00 ssh-agent

STEP 3
-Creating SSH Key
cd ~ 
ssh-keygen -t ed25519 -b 4096 -C "{username@emaildomain.com}" -f {ssh-key-name}

NOTE: This wil make 2 files in the home directory: {ssh-key-name} (private key) and {ssh-key-name}.pub (public key)

STEP 4
-Adding SSH Key to SSH Agent
ssh-add {ssh-key-name}

-Check if SSH Key is added to SSH Agent
ssh-add -l

-Output (similar to):
4096 SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx {ssh-key-name} (ED25519)

STEP 5
-Connecting SSH Key to Bitbucket
Host bitbucket.org
  AddKeysToAgent yes
  IdentityFile ~/.ssh/{ssh-key-name}

STEP 6
Add your public SSH Key to Bitbucket (Settings > SSH Keys > Add Key)
You can now clone your repository with SSH

AFTER INSTALLLING AND ADDING
Go through STEP 2 and STEP 4 again to check if SSH Agent is running and if SSH Key is added to SSH Agent
the other steps shouldn't be necessary anymore
After this you can clone your repository with SSH



