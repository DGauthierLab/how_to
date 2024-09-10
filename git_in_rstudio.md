# Working with Git inside Rstudio

### Step 1: Configure Git inside Rstudio
- Under Tools inside Rstudio, open "Global Options"
- Select `Git/SVN` on the left menu
- Browse to find your Git executable
  - For Windows, most likely, it is at C:/Program Files/Git/bin/git.exe and will need to be set.
  - For Macs, most likely, it is at /usr/local/bin/git and will NOT need to be set.
  - *IMPORTANT*: do not select any files that look like executables outside the bin folder.  They will mess up everything.
- Select the `Create SSH key` button.  Leave `Passphrase` and `Confirm` blank.  Select `Create`
- Close the popup window.  Select `View Public Key` and press Ctrl+C to copy to clipboard.
- Go to your Github account and select your profile.  Select `Settings` and then `SSH and GPG` keys from the left menu.
- Press the green `New SSH Key` button and paste in your SSH Public Key copied from Rstudio.  Title it whatever you want.

### Step 2: Clone repository from Github
- In Rstudio, select `File/Create New Project`
- Select `Version Control` from the popup window
- Select `Git` from the next popup window
- Go to your Github account and the repository you want to work with.  There should be a green `Code` button.  Select it and select the `SSH` submenu under Clone
- Copy the text in the gray box immediately below `SSH`
- Head back to Rstudio and paste this text into the `Repository URL` line
- Name your project directory whatever you like
- On the next line, select where you want your repository stored locally on your computer
      *PRO TIP* It is not recommended to store your repo on a shared server, like Drive or OneDrive
- Click `Create Project`  You should now have a Git tab in your Environment pane and the cloned repo should be under the Files tab
