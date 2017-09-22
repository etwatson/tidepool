# **Tidepool** best practices
Here, you will find comments and suggestions specific to the tidepool server. 

## Remote login
You can log in to tidepool remotely using a Secure Shell (SSH) with the command: ```user@tidepool.usc.edu```

## Installing programs on tidepool
There are many ways to install new programs in linux. The best way is to use a repository such as Ubuntu Software Center, apt-get, aptitude, deb, conda, pip, etc... These will compile and install the software in the correct location. 

### Ubuntu Software Center
The easiest and most convenient way to find and install software in Ubuntu is by using Ubuntu Software Center. In Ubuntu Unity, you can search for Ubuntu Software Center in Dash and click on it to open it. You can think of Ubuntu Software Center as Google’s Play Store or Apple’s App Store. It showcases all the software available for your Ubuntu system. You can either search for an application by its name or just browse through various categories of software.

### Debian files
.deb files are similar to the .exe files in Windows. This is an easy way to provide software installation. Many software vendors provide their software in .deb format. Google Chrome is such an example.

You can download .deb file from its official website, usually SourceForge. Once you have downloaded the .deb file, just double click on it to run it. It will open in Ubuntu Software Center and you can install it in the same way as we saw in the previous section.

Tip: A few things to keep in mind while dealing with .deb files:
* Make sure that you are downloading the .deb file from the official source. Only rely on the official website or GitHub pages.
* Make sure that you are downloading the .deb file for correct system type (64 bit).

### Aptitude / apt-get

You might have noticed a number of websites giving you a command like ```sudo apt-get install``` to install software in Ubuntu.

This is actually the command line equivalent of what we saw in the first section. Basically, instead of using the graphical interface of Ubuntu Software Center, you are using the command line interface. Nothing else changes.

Using the apt-get command to install software is extremely easy. All you need to do is to use a command like:

```sudo apt-get install package_name```

Here sudo gives ‘admin’ or ‘root’ (in Linux term) privileges. You can replace package_name with the desired software name. 

apt-get commands have auto-completion so if you type a few letters and hit tab, it will provide all the programs matching with those letters.

PPA stands for Personal Package Archive. This is another way that developers use to provide their software to Ubuntu users.

In section 1, you came across a term called ‘repository’. Repository basically contains a collection of software. Ubuntu’s official repository has the softwares that are approved by Ubuntu. Canonical partner repository contains the softwares from partnered vendors.

In the same way, PPA enables a developer to create its own APT repository. When an end user (i.e you) adds this repository to the system (sources.list is modified with this entry), software provided by the developer in his/her repository becomes available for the user.

Now you may ask what’s the need of PPA when we already have the official Ubuntu repository?

The answer is that not all software automatically get added to Ubuntu’s official repository. Only the trusted software make it to that list. Imagine that you developed a cool Linux application and you want to provide regular updates to your users but it will take months before it could be added to Ubuntu’s repository (if it could). PPA comes handy in those cases.

Apart from that, Ubuntu’s official repository often doesn’t include the latest version of a software. This is done to secure the stability of the Ubuntu system. A brand new software version might have a regression that could impact the system. This is why it takes some time before a new version makes it to the official repository, sometimes it takes months.

But what if you do not want to wait till the latest version comes to the Ubuntu’s official repository? This is where PPA saves your day. By using PPA, you get the newer version.

Typically PPA are used in three commands. First to add the PPA repository to the sources list. Second to update the cache of software list so that your system could be aware of the new available software. And third to install the software from the PPA.

I’ll show you an example by using Numix theme PPA:

```sudo add-apt-repository ppa:numix/ppa```

```sudo apt-get update```

```sudo apt-get install numix-gtk-theme numix-icon-theme-circle```

In the above example, we added a PPA provided Numix project. And after updating the software information, we add two programs available in Numix PPA.

### Compiling programs from source code

Installing a software using the source code is not something I would recommend to you. You’ll have to fight your way through dependencies and what not. You’ll often have to keep the source code files else you won’t be able to uninstall it later.

However, most of the programs used in computational biology are architecture-dependent, and require local compilation. 

I’ll be short in this section and just list out the steps to install a software from source code


* Download the source code of the program you want to install. Many times, you will need to clone a repository using GitHub. 
* Extract the downloaded file, or clone using GitHub: ```git clone https://github.com/etwatson/tidepool.git```
* __All source code should be extracted or cloned to ```/usr/local/repo```__ 
* Go to extracted directory and look for a README or INSTALL file. A well-developed software may include such a file to provide installation and/or removal instructions.
* Look for a file called configure. If it’s present, run the file using the command: ```./configure``` This will check if your system has all the required softwares (called ‘dependencies’ in software term) to install the program. Note that not all software include configure file which is, in my opinion, bad development practice.
* If configure notifies you of missing dependencies, install them.
* Once you have everything, use the command ```make``` to compile the program.
* Once the program is compiled, run the command ```sudo make install``` to install the software.
* If necessary, add the folder including binaries to your path: ```echo "export PATH=$PATH:/folder/bin" >> ~/.bashrc```
* If updating your path is necessary, please share that information with other users. 


## Data storage on tidepool
All data should be stored on the data drive located in ```/media/data``` in an effort to keep the boot drive clean. Data may be temporarily stored in your ```/home/(user)``` directory, but be mindful of the available storage on this drive, as it may prevent tidepool from booting if it fills up. 

You can find out how much storage is available on each drive using the command ``` df -H```
