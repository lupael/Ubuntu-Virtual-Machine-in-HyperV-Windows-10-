# Creating an Ubuntu Virtual Machine in HyperV (Windows 10)

Last updated using Ubuntu 18.04.2 (amd64)

## 0. Pre-requisites

To check if your machine supports Hyper-V, fire up the Command Prompt (`cmd.exe`) and enter `systeminfo.exe`

At the end of the output, you will see an entry named `Hyper-V Requirements`.

If all you see are `No`, you need to enable hardware virtualization in BIOS. Otherwise, proceed

## 1. Enable Hyper-V

Open `Windows Features` (you can search for it in search box), check Hyper-V. 

Click `OK` and wait for reboot

## 2. Get Ubuntu Image

You can find and download your favorite ubuntu release [here](http://releases.ubuntu.com/)

## 3. Create Virtual Machine

Open `Hyper-V Manager` (you can search for it in search box).

In `Action` menu, select `New -> Virtual Machine...`

![hyperv1](https://user-images.githubusercontent.com/25496380/60899770-94e06100-a25a-11e9-8169-d9f9a8bec22d.PNG)

Then, follow the wizard to create a virtual machine:

![hyperv2](https://user-images.githubusercontent.com/25496380/60900552-e50bf300-a25b-11e9-9ac4-69b55bdfbc0d.PNG)

Very discriptive name

![hyperv3](https://user-images.githubusercontent.com/25496380/60900555-e50bf300-a25b-11e9-8bd9-5e6a9dda618f.PNG)

Use generation 1

![hyperv4](https://user-images.githubusercontent.com/25496380/60900557-e50bf300-a25b-11e9-9d78-6d04bf87bb04.PNG)

2GB should be sufficient. Customize based on need and available system resources

![hyperv5](https://user-images.githubusercontent.com/25496380/60900558-e50bf300-a25b-11e9-94ae-1028308e9fb1.PNG)

We will [configure network connection later](#5-but-i-cant-apt-get)

![hyperv6](https://user-images.githubusercontent.com/25496380/60900559-e50bf300-a25b-11e9-8e2c-b0f88983b64b.PNG)

16GB should be sufficient for a guest OS. Customize based on need and available system resources

![hyperv7](https://user-images.githubusercontent.com/25496380/60900560-e5a48980-a25b-11e9-96b9-054fb410fa67.PNG)

We will use the Ubuntu image you downloaded earlier to install OS

![hyperv8](https://user-images.githubusercontent.com/25496380/60900562-e5a48980-a25b-11e9-9a7b-fe52c805fdf0.PNG)

Looks right

![hyperv9](https://user-images.githubusercontent.com/25496380/60900551-e50bf300-a25b-11e9-9ac6-f95b9921e9a9.PNG)

Voilà!

![hyperv10](https://user-images.githubusercontent.com/25496380/60900939-9448ca00-a25c-11e9-8235-334c8127f4cf.PNG)


## 4. First Boot

Double click on your newly created virtual machine.

Click `start` in the new window to fire it up, and you shall be welcomed by Ubuntu:

![hyperv11](https://user-images.githubusercontent.com/25496380/60953206-3cf23a80-a2ec-11e9-8d66-8ec06f17a076.PNG)

Select install and follow the guide

![ubuntu1](https://user-images.githubusercontent.com/25496380/60952898-ade52280-a2eb-11e9-9766-f19c9fca011e.PNG)

Whatever keyboard you use...

![ubuntu2](https://user-images.githubusercontent.com/25496380/60952899-ade52280-a2eb-11e9-958b-019efc4824f4.PNG)

Basic or *FULL DELUXE VERSION* ?

![ubuntu3](https://user-images.githubusercontent.com/25496380/60952900-ade52280-a2eb-11e9-8f36-14226412a90d.PNG)

And yes we are going to erase disk for re-formatting. We are in a new virtual realm so there is nothing to wipe really. 

![ubuntu4](https://user-images.githubusercontent.com/25496380/60952902-ade52280-a2eb-11e9-9a98-199b75a1346a.PNG)

Continue

![ubuntu5](https://user-images.githubusercontent.com/25496380/60952903-ade52280-a2eb-11e9-99fb-84b3670ca77a.PNG)

Where am I?

![ubuntu6](https://user-images.githubusercontent.com/25496380/60952904-ade52280-a2eb-11e9-9a74-1ed318ed9cc7.PNG)

Who am I?

![ubuntu7](https://user-images.githubusercontent.com/25496380/60952905-ae7db900-a2eb-11e9-93ed-102039d88935.PNG)

Almost there, just restart

![ubuntu8](https://user-images.githubusercontent.com/25496380/60952906-ae7db900-a2eb-11e9-84e7-66656f03ba1c.PNG)

**NOTE: If virtual machine is stuck on prompt to remove disk and reboot, just `Turn Off...` the virtual machine in Hyper-V manager and start it again**

*YAY!* **✧◝(⁰▿⁰)◜✧**

![ubuntu9](https://user-images.githubusercontent.com/25496380/60952907-ae7db900-a2eb-11e9-8b08-ca54591760e7.PNG)

## 5. But I can't `apt-get`

Remember that we didn't configure network connection right? We will do that now

First, shut down the virtual machine and go to `Hyper-V Manager` and in `Action` menu select `Virtual Switch Manager...`

Create a new **Internal** virtual switch. This allows us to connect to the virtual machine from hosting machine, using stuff like `ssh`

![switch1](https://user-images.githubusercontent.com/25496380/60961195-1ee00680-a2fb-11e9-88c8-15a55c2a03e7.PNG)

![switch2](https://user-images.githubusercontent.com/25496380/60961196-1ee00680-a2fb-11e9-92fa-fdbc9b460803.PNG)

***But, but, I want connect to the Internet!***

To connect our virtual machine to the internet, open `Network and Sharing Center` in `Control Panel`

Select an active internet connection and click `Properties`:

In the `Sharing` tab, `Allow other network users to connect through this computer's network connection` and select `vEthernet (Internal)` in `Home networking connection`

![switch3](https://user-images.githubusercontent.com/25496380/60961197-1ee00680-a2fb-11e9-90e0-30bc10cb791e.PNG)

In `Hyper-V Manager`, select your virtual machine and in `Action` menu, select `Settings...`

In `Network Adaptor`, select the internal network switch you created earlier.

![switch4](https://user-images.githubusercontent.com/25496380/60965998-c7e02e80-a306-11e9-8f12-e8c6077e239d.PNG)

This should get you online. Enjoy!

## 6. Further Notes

### If you are on a company intranet, you may need to configure proxy. 
- Go to `Settings -> Network -> Network Proxy`
- For system wide proxy on Ubuntu 18 ([Original Post Here](https://askubuntu.com/questions/1049440/how-do-i-set-system-wide-proxy-in-ubuntu-18-04))
  - Edit `/etc/environment` to include:
    ```
    http_proxy=http://username:password@host:port/
    ftp_proxy=ftp://username:password@host:port/
    https_proxy=https://username:password@host:port/ 
    ```
  - Edit `/etc/apt/apt.conf.d/80proxy` to include:
    ```
    Acquire::http::proxy "http://username:password@host:port/";
    Acquire::ftp::proxy "ftp://username:password@host:port/";
    Acquire::https::proxy "https://username:password@host:port/";
    ```
