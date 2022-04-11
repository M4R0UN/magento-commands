# Script for creating a shortcut to the Desktop folder on Windows (Using Ubuntu extention)

**Go to the bin folder** `cd /bin`

**Create a file desktop** `sudo touch desktop`

**Edit desktop file** `sudo nano desktop`

###### Paste this: (edit yourusername)

> #!/bin/bash
> 
> ln -s /mnt/c/Users/yourusername/OneDrive/Desktop ~/Desktop

**Close and save the file**

**Now you can access desktop by just entering** `cd ~/Desktop`
