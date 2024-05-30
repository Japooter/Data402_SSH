# Data402_SSH

The steps to get SSH working on your own computer!

SSH is in general more secure than HTTPS so long as you are careful, so it is very beneficial to start cloning repositories (and if you own a repo have push/pull access) via SSH.

## A quick background on SSH
SSH stands for "Secure SHell", a "shell" in computing terms is a way to communicate with your operating system usually with low-level software. SSH specifically allows for this to be done with a remote service (i.e. not your personal computer). The idea is it is analogous to a lock and key. SSH creates two keys, one public and one private. Let's assume that the "public key" is a key hole. Everyone can see the key hole and it is the way into the house (which in this metaphor represents the server we get access to). To get access, we need a key to fit the key hole, this being the "private key". Only the homeowner (the computer client) should have access to the key (ignoring for the sake of this metaphor factors such as letting agencies or others) and if anyone malicious got their hands on the key, the house would be insecure. This is the idea with SSH and so long as caution is taken it is the better way between it and HTTPS to keep your data on git/github secure.

## Navigate to .ssh
In your home directory, there should be a hidden folder called ".ssh", so first you want to navigate to this. While in your home directory:

```
cd .ssh
```
If you want you can now check to see if there is anything within the folder, but if this is your first time creating a key (as part of the next step) you will not likely see anything - if you cannot see a file ending in the extension ".pub", you have likely not created a key before on this computer.

## Create a key
Create a key using the command `ssh-keygen`. The full command is listed below, with an example of certain flags that are typically included. When typing the command, note that the flag "-t" is the type of encryption that is going to be used. For this example, we are using rsa, but if you would prefer another type, research online other types you can use. "-b" is the flag for bits used, essentially how long the encryption will be. Ideally, you want a size that isn't too small and isn't too large for the sake of a balance between security and convenience. For this example, 4096 bits are used, a generally accepted good value. Finally, "-C" can be used to write a comment. It is generally accepted that an email address is used for this comment, for example "james@toast.ws", surrounded by quotes like this. Now, input the command in full.

```
ssh-keygen -t rsa -b 4096 -C "<email here>"
```

You will be prompted to type a name for the file. Call this whatever you want so long as it is memorable to you. The name of the file itself isn't the key, but it will generate both the public and private key under this name (the private key being called just "name_you_chose", and the public key being called "name_you_chose.pub".

You will then be prompted to enter a passphrase. Copy the passphrase to a safe space or remember it very well if you do want to have a passphrase, but you can also choose to omit a passphrase entirely by just pressing enter. Type the passphrase in a total of two times and then you have successfully created the keys. You will be given a key fingerprint and randomart. The randomart is a way of identifying the key, but for the github process it is not necessary. If you check the files found within the directory now, you should see your created keys.

## Copy the public key
Open the public key's file by typing the following into the command line:
```
sudo nano name_of_key.pub
```
Copy the key you see within the file and close the file safely. Do not copy any whitespace that is before or after the key (the key should begin with "ssh-" and end with the comment you wrote in earlier). Alternatively, you can type the command:
```
cat name_of_key.pub
```
This will paste the public key and you can just copy it this way. If both of these are not desirable for you in one way or another, you can instead navigate to the directory with your file explorer (or equivalent) and open the public key file in a text editor. *DO NOT* edit anything within the key, but copy and paste the key as usual, avoiding any whitespace after the key.

## Make a "Deploy key"
On your github account, access the repository you wish to have access to in a local repository and enter the settings page. Under "Security", find "Deploy keys" as an option. Click this and in the menu that opens click the button "Add deploy key".

Give the key an appropriate title and then paste the public key *in its entirety* in the key section. By default, all keys have read access to the git repo, meaning they can pull to the local directory. If you wish to provide write access, so that the local repo can push to the github repository, be sure to check the box "Allow write access".

If you entered the key correctly (remember, no whitespace after the comment) then this will add a key that is now permitted.

## Add the ssh key to your list of valid keys
We are done on the github side, but we still need to ensure that we can clone the repo. In the command line, **navigate out of the .ssh folder** and navigate to any appropriate folder. Ensure that you do this first step, as you do not want to do any of this within the .ssh folder.

Once you have done so, the following command can be typed in:
```
ssh-add ~/.ssh/name_of_key
```
Once you have typed this, you may get a warning that github is not a trusted source. This is fine, accept anything it wants you to and continue until you see `Identity added:` and then your key's file path. To double check this has worked, type:
```
ssh -T git@github.com
```
This should be responded to with a message along the lines of:
```
Hi YourUserName! You've successfully authenticated, but GitHub does not provide shell access.
```
This is expected, you can now finish with cloning the repository and you will see that it works!

Go to an appropriate location and then type:
```
git clone SSH_LINK_FROM_GITHUB_HERE
```
where the link can be found from the "Code" button on your repository page.

Note: If you have a Windows computer, you may have to do a command before `ssh-add`, so ensure that you check what this is before you continue.
