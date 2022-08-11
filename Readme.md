# Package Creation

## To package Skittles Edge Server in terminal
sh ./PackageSkittlesEdgeServer.sh packageName version revision sourceFolder

### Example
sh ./PackageSkittlesEdgeServer.sh skittles-edge-server 0.0.1 1 /media/sf_Share

## WSL installation

## GPG 
gpg: all values passed to '--default-key' ignored
gpg: no default secret key: No secret key
gpg: signing failed: No secret key

If you see this error when running update-apt-repo.sh, you are running with sudo... ensure you execute as: *sh ./update-apt-repo.sh*

### Required packages
sudo apt install dpkg-dev
sudo apt install mono-utils
