# Verifying Installation

At the end of the installation, the installer displays the IP and ports
of ATSD. You can use them to access the ATSD web interface.

Depending on your device and hard drive, it can take another 15-20
minutes for ATSD to start after the message below has been displayed
(this is the case on Raspberry Pi 2).

![](images/atsd_install_shell.png "atsd_install_shell")

To find the IP address of the target machine manually, enter `ifconfig`
or `ip addr` command.

Open your browser and navigate to port `8088` on the target device. When
accessing the ATSD web interface for the first time, you will need to
setup an administrator account.

## Verifying Portals

Click on Portals tab in the ATSD web interface. A pre-defined ‘ATSD’
portal consisting of 12 widgets should be visible. This portal displays
various system usage metrics for ATSD and the machine where it’s
installed.

![](images/fresh_atsd_portal21.png "ATSD Host")