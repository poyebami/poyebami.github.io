<h1>Package Management Introduction </h1>


<h3>Package Managers</h3>
There are hundreds of Linux distributions. One way to categorize a linux distribution is by the package management it uses.
RHEL (Red Hat Enterprise Linux), Fedora, and CentOS are RPM based distribution. Ubuntu, Debian, Arch Linux, Linux Mint make use of
the Debian package managers such as DPKG. 

RHEL and CentOS are very similar. CentOS forked from RHEL. However, CentOS is a community-driven enterprise operating system. RHEL is only 
available through a paid subscription. With the subscription, you get support for mission-critical systems and quicker access to the latest 
features. 

A `package` is a compressed archive that contains all the files that are required by a particuilar software to run. Let say we are using an Ubuntu
system and installing GIMP (GNU Image Manipulation Program). TO install GIMP, we need to make sure of GIMP.DEB package. The GIMP.DEB package contains
all the software binaries and files needed for the image editor to run, along with the metadata, which provides information about the software itself.

There are hundreds of different linux distributions with their own sets of tools and libraries, software, and possibly different linux kernels. As a result of 
this, a linux program may not run the same way from one system to another. To fix the problem., packages include a manifest of dependencies, or list of programs
and versions that must be satisfied for the package software to run correcly on a given computer. If the dependencies is not met, the installation will fail. 
Dependent packages may also have dependencies of their own. This makes package installation and management very tedious. Package manager makes it easier.

A `package manager` is software in a linux system that provides a consistent and automated process of installing, upgrading, configuring, and removing
packages from the operating system. Some the the functions of a package manager are 
* ensuring the integrity and authenticity of the package by verifying their digital certificates and checksums. This is to ensure that the package is downloaded
from a trusted source and safe to install.
* simplifying the entire package management process. Most package managers have querying options, making it easier to look up packages and then downloading,
installing, or updating existing software from a software repoistory.
* grouping packages by function ro reduce user confusion.
* managing dependenciesto ensure a package is installed with all packages it requires, avoiding the 'dependency hell'.

Some of the common package managers are DPKG, used for Debian-based distributions. APT, a newer front-end for the DPKG system found in Debian-based distribution, such as 
Ubuntu, Linux Mint, and elementary OS. APT-GET is the traditional front-end fro the DPKG system also found in Debian-based distributions. RPM is the base package manager found
in Red Hat-based distributions, such as Red Hat Enterprise Linux, CentOS, and Fedora. YUM, a front-end for the RPM system found in Red Hat-based distributions. DNF, a more feature-rich
front-end for the RPM system.

<h3>RPM and YUM </h3>
RPM (Red Hat Package Manager): the file extension for packages managed by RPM is .rpm. RMP has five basic modes of operations: installing, uninstalling, upgrade, query, and verifying.
Each of these modes can be run using the rpm command followed by specific command options.
 * Installation
    ```console
     $ # install a package
     $ rpm -ivh "package_name".rpm
     $ rpm -ivh telnet.rpm
    ```
    "i" stands for install
    "v" stands for verbose. prints out a detailed output of the command
    "h" stands for hash marks. shows progress with #######
 
 * Uninstalling 
    ```console
     $ # uninstalling a package
     $ rpm -e "package_name".rpm
     $ rpm -e telnet.rpm
    ```
    "e" stands for erase

 * Upgrade
    ```console
     $ # upgrading an existing package to a newer version
     $ rpm -Uvh "package_name".rpm
     $ rpm -Uvh telnet.rpm
    ```
    "u" stands for upgrade
    The RPM database stores information about all RPM packages installed in your system. /var/lib/rpm.
    It is used to query what pacakages are installed, what version each package is, and any changes to any files in the package since installations, etc.
 
 * Query
    ```console
     $ # to query database and get details about an installed package
     $ rpm -q "package_name".rpm
     $ rpm -q telnet.rpm
    ```
    "q" stands for query

 * Verifying
    ```console
     $ # verify a package
     $ rpm -v "package_name".rpm
     $ rpm -v telnet.rpm
    ```
    verifying a package comapres information about files installed from a package with the same information from the original package. It useful to make sure that the package has been installed from a trusted and secure source.
    RPM does not resolve package dependencies on its own. There is a higher level package manager called YUM.

YUM (Yellowdog Updater Modified) is a free and open-source package manager that works on RPM-based Linux systems. Works with software repositories, which are essentially a collection of packages
and provides package and dependency management on RPM-based distros. The repository information is stored in the /etc/yum.repos.d, and the repository files have a .repo extension. It still depends 
on RPM to manage and install packages on the linux system. YUM handles pacakge dependencies very well and is able to install any dependent packages to get the vase package installed on the linux system.

YUM Depends on software repositories, containing hundreds and thousands of RPM packages files. These repositories can be local or on a remote location that can be accessed through transfer protocols such as FTP, HTTP, or HTTPS.
The information about the repository is saved in a configuration file under /etc/yum.repos.d. Usually the OS comes bundled with its own software repoitories. For example, for a Red Hat OS with an active suvscription, you would normally find a 
file called redhat.repo in the directory. /etc/yum.repos.d/redhat.repo It points to the official Red Hat managed software repository for the specific version of the OS that is running. You can also add a new repo
in this diectory in case you don't want to make sure of the official repo. /etc/yum.repos.d/nginx.repo This happens if the official repo doesn't have the latest version of the software you want to install and sometimes it may not have it at all.

 * Installing package
    ```console
     $ yum install httpd
    ```
    YUM will first run a transaction check. If the package is not installed in the system. YUM checks the configured repositories under the repos.d directory for the availability of the requested package. It also
    chcecks if any of the dependent packages are already installed or it is needs to be upgraded.
    After this step, a transaction summary is displayed on the screen for the user to review. If we wish to proceed with the install, enter the Y bottom. To skip the confirmation use -y flag. 
    ```console
     $ yum -y install telnet
    ```
    After confirmation, YUM will download and install the necessary RPMs to the system. 

  * Common YUM Commands
    ```console
     $ # display all the repos added to the system
     $ yum repolist

     $ # check which package should be installed for a specific command to work
     $ yum provides ""argument"
     $ yum provides scp

     $ # removes a package
     $ yum remove httpd

     $ # update a single package
     $ yum update telnet

     $ # update all packages installed
     $ yum update

     $ # list all available commands
     $ yum help
    ```
