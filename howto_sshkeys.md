# ssh keys - No more passwords for remote servers and GitHub

The following procedure will allow you to generate an SSH key, which will allow your RStudio instance on the ODU HPC or RStudio session on your local computer to talk to GitHub seamlessly. 

## Instructions for generating an SSH key on ODU HPC RStudio OnDemand

1. From your RStudio session on the ODU HPC, select Tools from the top menu, then Global Options, then the Git/SVN tab on the left.
   
2. Click the "Create SSH Key" button.  The dialog box should say "The SSH key will be created at: /home/<MIDAS>/.ssh/id_ed25519", where <MIDAS> will be your MIDAS ID.  The id_edXXXXX number will be different.

3. Leave Passphrase and Confirm blank and click "Create".  If you get a dialog box asking you to overwrite the existing key, you already have one and can likely cancel out of the process.  If not, click "Yes".

4. You'll get a dialog box with a funny looking randomart image in it.  This can be closed.  Click the "View public key" link and copy the key to the clipboard.  It will start with ssh and end with your midas ID and a bunch of numbers.

5.  Go to your GitHub account online and select the pixel art image in the upper right.  Select "SSH and GPG keys" from the menu to the left.

6.  Click the "New SSH Key" button.  Give a title (Wahab is good, so you know this links to the HPC), then past the key in the "Key" box.  Click the green "Add SSH Key" button.

7.  Now GitHub knows to trust access from your ODU HPC account and pushing/pulling from within RStudio should work.

## Instructions for generating a local SSH key

1.  You should be able to follow the above steps to generate a local key.  If that doesn't work and you have a Terminal or Terminal-like environment installed, you can use the alternate procedure below:

## Local SSH key alternate method

1. Determine if you've already created a key
    
    Run the following commands in your terminal
    ```bash
    cd ~
    ls .ssh
    ```
    
    If you see the following files (or something very similar), you have a key. Goto step 3.
    ```
    id_rsa  id_rsa.pub
    ```
    
    If you don't see a key pair `id_???` and `id_???.pub`, then goto step 2
 
 2. Create a key pair
    
    You only need 1 key pair, so if you *don't* have files named `id_???` and `id_???.pub` in your `~/.ssh` dir, then you need to generate them as follows:
    
    ```bash
    ssh-keygen -t rsa
    # you will be prompted for a pass phrase, etc
    # i recommend hitting enter at each prompt
    ```
    
    When the key pair is created, you should see something like this:
    
    ```
    Generating public/private rsa key pair.
    Enter file in which to save the key (/var/services/homes/Chris/.ssh/id_rsa): 
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /var/services/homes/Chris/.ssh/id_rsa.
    Your public key has been saved in /var/services/homes/Chris/.ssh/id_rsa.pub.
    The key fingerprint is:
    SHA256:rp5Z3rd6FenG7CZXjsERVhG5BODd4b3ReNcpr5/veq4 Chris@HOBIcloud
    The key's randomart image is:
    +---[RSA 2048]----+
    |           ....==|
    |          . . =+*|
    |           . +oBB|
    |              *o+|
    |        S    = = |
    |       .      X .|
    |        o    = = |
    |       * .  + * +|
    |     .= . o+.=EO=|
    +----[SHA256]-----+

    ```
    
    Run the following commands in your terminal
    ```bash
    cd ~
    ls .ssh
    ```
    
    If you see the following files (or something very similar), you have a key. Goto step 3.
    ```
    id_rsa  id_rsa.pub
    ```

3.  Placing your key on Github
    
    * For [GitHub](https://github.com) you can use the official instructions [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account) starting at step 2, or the following may be more straightforward:
      
    * from your home directory, enter the following command in Terminal:
    ```
      cat ~/.ssh/id_rsa.pub 
    ```
    * highlight and copy everything from ssh-rsa to the end of the line

    * next, Open and log into GitHub

    * in "account settings" go to "SSH and GPG Keys"

    * select "new SSH key" and paste your clipboard into the box

    * add the key
      
    * IMPORTANT: For the SSH key to work, when cloning a repo you must clone the SSH repo and not the HTTPS repo
      
4.  Placing your key on a remote server/computer
   
    * For any remote server/computer, copy your public to your `~/.ssh` dir on the remote computer as follows:
    
    ```bash
    # you must be on/in your laptop (or local machine) not the remote server when you run this command
    
    ssh-copy-id YourUserName@IP-address-of-remote
    
    # you will be prompted for your password on the remote computer
    ```
        
    * Example: for me (`dgauthie`) on the ODU Cluster (`wahab.hpc.odu.edu`)
        
    ```
    bash-3.2$ ssh-copy-id dgauthie@wahab.hpc.odu.edu
    /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/dgauthie/.ssh/id_rsa.pub"
    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
    /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
    (dgauthie@wahab.hpc.odu.edu) Password:
    
   Success. Logging you in...

    Number of key(s) added:        1

    Now try logging into the machine, with:   "ssh 'dgauthie@wahab.hpc.odu.edu'"
    and check to make sure that only the key(s) you wanted were added.

    ```
