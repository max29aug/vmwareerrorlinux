**#After downloading the zip file please extract those files and then cd to that file location, afterwards use the commands as follows:

make

sudo make install

sudo reboot


#After rebooting the computer launch the vmware and you need to get the installation and activation completed for vmware
#Even after that if you are gettig the error please use the commands below:

sudo vmware-modconfig --console --install-all

sudo openssl req -new -x509 -newkey rsa:2048 -keyout VMWARE.priv -outform DER -out VMWARE.der -nodes -days 36500 -subj "/CN=VMWARE/"

sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMWARE.priv ./VMWARE.der $(modinfo -n vmmon)

sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMWARE.priv ./VMWARE.der $(modinfo -n vmnet)

tail $(modinfo -n vmmon) | grep "Module signature appended"

sudo reboot

sudo mokutil --import VMWARE.der


#Once you computer reboots, you need to click on Continue to boot as it would either ask to enroll mok or continue to boot, I would sugesst that you click on continue to boot. Then you need to check if mok is enrolled or not through terminal once you are logged in.

sudo mokutil --import VMWARE.der**
