#1. Automatic IP update for Raspberry Pi 
The purpose of this project is to perform automatically update this repository with the IP address of a Raspberry Pi so that you can easily `ssh` and program the Pi remotely.
Enterprise networks rarely allow you to setup a static IP for your Pi and hence the need for this alternative approach.

#2. Setup Instructions

## Fork the repo
Make sure that `origin` points to your fork or you will need do to a minor modification in `ip-update.sh`

## Create ssh keys
```
cd ~                 # Your home directory
ssh-keygen -t rsa    # Press enter for all values
```

Make sure to press `Enter` for all questions.

## Associate the SSH key with the remote repository
Go on github. `Settings -> Deploy keys -> Add Deploy Keys`. Copy the contents of `~/.ssh/id_rsa.pub` in the key field.

## Set the remote URL to a form that supports SSH

On the Raspberry PI make sure you have the SSH form of the link for the remote repository. It should look like

```
git+ssh://git@github.com/username/reponame.git
```
as opposed to
```
https://github.com/username/reponame.git
```

## Setup the cronjob on the Raspberry Pi
Make sure to modify `$DIR` in the `ip-update.sh` script to match the full path of your directory.
Also modify the path for the script inside `ip-cron.txt`
Then setup the cronjob

```
crontab ip-cron.txt
```
The cronjob will be active even after reboot. The IP address will be in the file named `ip.txt`. The first IP is for `eth0` and the second for `wlan0`.


