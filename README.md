# Soularr on Unraid
Instructions for installing Soularr on Unraid. Please read through this fully before trying to use the Unraid template.

### Step 1

Make sure you go through the setup steps at https://soularr.net/ to make sure Lidarr and slskd are working. You will have to manually adjust your slskd.yml to add an API key for Soularr to use. 

#### Note for slskd:

If you installed slskd using the Unraid CA template, it will most likely be running as root. To make sure soularr will work, you need to adjust your slskd template.

First, go into your slskd template, and make sure "Advanced View" is on in the upper right hand corner. Then add "--user 99:100" without quotes in "Extra Parameters"

Second, you will need to update the ownership of any directories mounted into slskd. This will be appdata and downloads/incomplete if you mapped them somewhere other than the default.

In the Unraid terminal, run the below command. You will need to change it to match your appdata location.

    chown -R 99:100 /mnt/user/appdata/slskd/

If you left the download and incomplete directories as default, the above command should be enough. If your download and incomplete directories are mapped somewhere else, run the same command for those directories. 

After adding the extra parameters and adjusting folder ownership, restart slskd.
