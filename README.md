# Soularr on Unraid
Instructions for installing Soularr on Unraid. Please read through this fully before trying to use the Unraid template. All commands should be entered in your Unraid system's terminal. (The ">_" symbol in the upper right hand corner of the Unraid WebUI.)

### Step 1

Make sure you go through the setup steps at https://soularr.net/ to make sure Lidarr and slskd are working. You will have to manually adjust your slskd.yml to add an API key for Soularr to use. You can see sample [here](https://github.com/JPDVM2014/soularr/blob/main/sample_smskd.yml).

#### Note for slskd:

If you installed slskd using the Unraid CA template, it will most likely be running as root. To make sure soularr will work, you need to adjust your slskd template.

First, go into your slskd template, and make sure "Advanced View" is on in the upper right hand corner. Then add "--user 99:100" without quotes in "Extra Parameters"

Second, you will need to update the ownership of any directories mounted into slskd. This will be appdata and downloads/incomplete if you mapped them somewhere other than the default.

In the Unraid terminal, run the below command. You will need to change it to match your appdata location.

    chown -R 99:100 /mnt/user/appdata/slskd/

If you left the download and incomplete directories as default, the above command should be enough. If your download and incomplete directories are mapped somewhere else, run the same command for those directories. 

After adding the extra parameters and adjusting folder ownership, restart slskd.

### Step 2

Now you will need to create your Soularr appdata directory and create your Soularr config file. Enter the below command in your Unraid terminal.

Adjust to match your appdata directory structure.

    mkdir /mnt/user/appdata/soularr/ && wget -P /mnt/user/appdata/soularr/ "https://raw.githubusercontent.com/mrusse/soularr/refs/heads/main/config.ini" && chown -R 99:100 /mnt/user/appdata/soularr/

Once the config is downloaded, you need to edit the values.

    nano /mnt/user/appdata/soularr/config.ini

The main things to change are your Lidarr and slskd API keys and make sure the host_url for both entries are correct. 

You will also need to adjust the download_dir for Lidarr and slskd. Lidarr should be the slskd downloar directory the way it looks from within Lidarr, not the Unraid share directory. For example, my slskd Unraid share is "mnt/user/data/music", but in Lidarr that directory is mounted at "/data/music". So, in the Soularr config, I set Lidarr's download_dir to /data/music.

If you are going to use the Unraid template as-is, you can set slskd's download_dir to /downloads. Then ctrl + o then enter to save. Ctrl + x to exit nano.

### Step 3

Now you should be able to install Soularr using the template. It should connect to Lidarr and Slskd and start searching/downloading any missing music.
