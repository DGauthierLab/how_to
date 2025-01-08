# Working with Git inside Rstudio

## Step 1: Configure Git inside Rstudio
### Note: This is the same procedure outlined [here:](howto_sshkeys.md)
1. Under Tools inside Rstudio, open `Global Options`
  
2. Select `Git/SVN` on the left menu

3. Browse to find your Git executable
  - For Windows, most likely, it is at C:/Program Files/Git/bin/git.exe and will need to be set.
  - For Macs, most likely, it is at /usr/local/bin/git and will NOT need to be set.
  - *IMPORTANT*: do not select any files that look like executables outside the bin folder.  They will mess up everything.

4. Select the `Create SSH key` button.  Leave `Passphrase` and `Confirm` blank.  Select `Create`

5. Close the popup window.  Select `View Public Key` and press Ctrl+C to copy to clipboard.
   
6. Go to your Github account and select your profile.  Select `Settings` and then `SSH and GPG` keys from the left menu.
  
7. Press the green `New SSH Key` button and paste in your SSH Public Key copied from Rstudio.  Title it whatever you want.

## Step 2: Clone repository from Github
### This is what you want if you've already set up an SSH key

1. In Rstudio, select `File/Create New Project`

2. Select `Version Control` from the popup window

3. Select `Git` from the next popup window

4. Go to your Github account and the repository you want to work with.  There should be a green `Code` button.  Select it and select the `SSH` submenu under `Clone`

5. Copy the text in the gray box immediately below `SSH`

6. Head back to Rstudio and paste this text into the `Repository URL` line

7. Name your project directory whatever you like

8. On the next line, select where you want your repository stored locally on your computer
      *PRO TIP* It is not recommended to store your repo on a shared server, like Drive or OneDrive

9. Click `Create Project`  You should now have a Git tab in your Environment pane and the cloned repo should be under the Files tab
