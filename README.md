# Data402_SSH

The steps to get SSH working on your own computer!

SSH is in general more secure than HTTPS so long as you are careful, so it is very beneficial to start cloning repositories (and if you own a repo have push/pull access) via SSH.

## Navigate to SSH
In your home directory, there should be a hidden folder called ".ssh", so first you want to navigate to this. While in your home directory:

```
cd .ssh
```

## Create a key
```
ssh-keygen -t rsa -b 4096 -C "<email here>"
```

You will be prompted to type a name for the file.

You will then be prompted to enter a passphrase. Copy the passphrase to a safe space or remember it very well if you do want to have a passphrase, but you can also choose to omit a passphrase entirely by just pressing enter.

## Copy the public key
```
sudo nano name_of_key.pub
```
Copy the key you see.

## Make a "Deploy key"

## Add the ssh key to your list of valid keys

