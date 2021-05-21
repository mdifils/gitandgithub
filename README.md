# Git tutorial

## Configure Git and GitHub using SSH key

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

## Creating a new repository
There are two ways to create a new repository.

### From my local machine

I follow the following steps:
1. Create a new directory `mkdir my_repo`
2. `cd my_repo` and `git init` 
3. Create a README.md file `touch README.md`
4. `echo # Git tutorial > README.md`
5. Create a new repo on github with the same name without initializing README and gitignore files.
6. Finally, add changes to the stage area, commit and push them on github
```bash
$ git status
$ git add .
$ git commit -m "Initial commit"
$ git remote add origin git@github.com:username/my_repo.git
$ git push --set-upstream origin master
``` 
### From Github
