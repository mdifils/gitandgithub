# Git and GitHub using SSH key

In this project, I'll explain how configure to connect my local machine with github account by SSH key. 
First of all, I need to check for an existing ssh key by typing the following command:
```bash
$ ls -al ~/.ssh

## result in case of any existing ssh key
id_rsa  id_rsa.pub  known_hosts
```
To generate a new ssh key, I type the following command:
```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Enter a file in which to save the key (/c/Users/_user_name_/.ssh/id_rsa): [Leave blank and press Enter]
Enter passphrase (empty for no passphrase): [Leave blank and press Enter]
Enter same passphrase again: [Leave blank and press Enter]
```
A private/public RSA key pair is then generated. In order for my local machine to communicate with github I need to the public key into my github account.
Also, if I don't want to reenter your passphrase every time you use your SSH key, I can add my private key to the SSH agent, which manages my SSH keys and remembers my passphrase.

```bash
# start the ssh-agent in the background
$ eval `ssh-agent -s`

# Add your SSH private key to the ssh-agent
$ ssh-add ~/.ssh/id_rsa
```

After adding my private to the ssh-agent, I can now add my public key to github by first copying its content: 
```bash
$ clip < ~/.ssh/id_rsa.pub
```
Then I can paste it by following the steps describe in this [tutorial](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).
