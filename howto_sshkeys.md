# ssh keys - No more passwords for remote servers and github

If you are here, you're probably wanting to set up an ssh key which allows your laptop to connect to a remote server, like one of our [high performance computing systems, aka supercomptuers](https://hpc.tamucc.edu/) or [GitHub](https://github.com). Follow these steps to get it setup

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
