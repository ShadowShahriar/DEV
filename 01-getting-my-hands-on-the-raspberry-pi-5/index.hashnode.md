As someone who's been always passionate about computers and electronics. I was closely following the release of **Raspberry Pi 5**. Last year, I purchased my first **Raspberry Pi 5**, but it has been sitting unused on my shelf ever since.

While I was excited to write my first program on a Pi, I was also afraid of destroying it 😓 Luckily, I have become comfortable handling microcontrollers and SBCs, so I decided to give the Pi a try ✨

![Photo of a person holding a Raspberry Pi 5][GETTING-STARTED]

In this post, I will give a step-by-step walkthrough of working with a Raspberry Pi, from assembling the components to writing the first `Hello World!` program.

> **NOTE:** There is a lot of documentation and great resources about Raspberry Pi on the Internet. But I wanted to write my own for future reference.

---

## Prerequisite

I picked up my [Raspberry Pi 8GB complete set from **Roboticsbd**][RBD-SET], which had all the required accessories. But if you are purchasing the hardware separately, here is everything you need:

1. [Raspberry Pi 5 (**4GB/8GB/16GB variant**)][RBD-PI5]
2. [Active Cooler][RBD-AC]
3. [Official 27W 5A USB-C Power Supply][RBD-PWR]
4. [Micro HDMI to HDMI cable][RBD-HDMI]
5. [Raspberry Pi Case (**optional**)][RPI-CASE]
6. [Micro SD Card (or SSD)][RYANS-SDCARD]
7. [Wireless Mouse and Keyboard Combo][RYANS-MKC]

I followed [**this video from DIY Engineers**][RPI-AC-INSTALL] to install the active cooler on the Raspberry Pi.

## Choosing a Storage Device

Interestingly, Raspberry Pi now supports M.2 NVME SSDs. But I don't have an **M.2 HAT+**, so, I had to use a **micro SD card** instead.

![A person holding a micro SD card][STORAGE-01]

However, after running some [**benchmarks**](#benchmarks), I found the micro SD card's performance was terrible. I looked up on Google and found out we can use an external USB SSD to boot up the Pi. I followed [**this video from Bytes N Bits**][RPI-USB-BOOT] and made the necessary preparations.

![A person holding a pendrive-shaped SSD][STORAGE-02]

I had this pendrive-shaped [**SSD from Trancend**][RYANS-SSD], where I installed the **Pi OS**.

## Installing the Raspberry Pi OS

Unlike microcontrollers, Raspberry Pi is a single-board computer (**SBC**), which can run full-blown operating systems such as **Linux**. To install an operating system on our Pi, we can use the [**Raspberry Pi Imager**][RPI-SOFT].

1.  Install and open the **Raspberry Pi Imager** on your main computer.

2.  In the Pi Imager window, select your **Raspberry Pi Device**. Since I have a Raspberry Pi 5, I will choose that from the list.

    ![Choose the preferred Pi device from the list][IMAGER-01]

3.  Now select the **Operating System**. I am going to choose the **64-bit** version.

    ![Choose the preferred Pi OS from the list][IMAGER-02]

4.  Connect the micro SD card or SDD and select the **Storage Device**.

    ![Choose the storage device from the list][IMAGER-03]

5.  After you click **Next**, you will receive a prompt asking if you would like to apply OS customization settings. This step is optional, and you can click **No** to skip it. Since I _want_ to customize some of the settings, I will click **Edit Settings**.

    ![Image of the OS customization prompt][IMAGER-04]

6.  I will set the **hostname**, **username**, and **password** to [**access the Pi remotely**](#accessing-the-pi-remotely). I will also set the WiFi SSID and password so that whenever the Pi boots up, it will automatically connect to my home WiFi.

    ![Image of the OS customization window][IMAGER-05]

Having done that, we are finally ready to install the Pi OS on the micro SD card or SSD. The installation process may take some time, depending on the device's speed and WiFi connection.

Unplug the micro SD card or SSD once the installation is complete.

## Hardware Connections

I have created a YouTube video that you can follow along:

%[https://www.youtube.com/watch?v=uxGKJFrnxT0]

1.  If you're using a micro SD card, insert it into the Raspberry Pi's SD card slot. If you're using an external SSD like I am, connect the SSD to one of the **USB 3.0 ports** (the blue ones).

2.  Connect the USB dongle for the mouse and keyboard combo to one of the **USB 2.0 ports** (the black ones).

3.  Connect the micro HDMI cable to one of the Raspberry Pi's micro HDMI ports and the HDMI end to a monitor.

4.  Connect the power supply to the Raspberry Pi's USB Type-C port.

We will soon see the LED next to the power button, turn green, indicating that the Raspberry Pi is powered on.

## Running the Raspberry Pi for the First Time

The Raspberry Pi will restart multiple times when booted for the first time. This happens only when we turn on the Raspberry Pi for the first time because it prepares all the services and peripherals under the hood.

There should be a welcome screen. However, I did not see one since I customized the OS in the previous step.

Once the Raspberry Pi has successfully booted up, we will be greeted by the desktop.

![The Raspberry Pi desktop][DESKTOP-VIEW]

> **NOTE:** If you experience any issues during the boot session ( such as a blank screen), you should check the HDMI and micro HDMI connections. The micro HDMI ports on the Raspberry Pi are fragile enough and can be easily damaged if not handled carefully. Also, ensure that your Raspberry Pi is receiving enough power from the power supply.

## Installing Visual Studio Code on the Pi

I wanted to write my first line of code in JavaScript. Since I'm _already_ familiar with the Visual Studio Code interface, I thought it would be a good idea to use VSCode. The installation process is straightforward and only takes a few clicks.

![Installing Visual Studio Code][INSTALLING-VSCODE]

1. Open the applications menu by clicking the Raspberry Pi button on the left corner.
2. Head over to **Preferences**, click **Recommended Software**.
3. Under the **Programming** section, check **Visual Studio Code**.
4. Click **Apply** and wait for a few minutes.

This could have ended here. However, I soon encountered an obstacle when VSCode crashed within 5 seconds 😶

### Investigating the Problem

After some research, I discovered that others are facing the same issue. I found [**this forum post**](FORUM-REPLY) where the OP manually installed an older version (**v1.86.2**) of VSCode, which resolved the problem. Here's how we can do the same:

Open the terminal and type the following command:

```bash
wget https://update.code.visualstudio.com/1.86.2/linux-deb-arm64/stable
```

Copy the file name and run:

```bash
sudo dpkg -i code_1.86.2-1707853305_arm64.deb
```

This was actually a simple fix, but it took quite a while to figure it out 😓

> **NOTE:** Make sure to uninstall the previously installed version of Visual Studio Code, before running the above commands.

### Installing the Extensions

![Installing the extensions][INSTALLING-EXTENSIONS]

1. Open the applications menu by clicking the Raspberry Pi button on the left corner.
2. Head over to **Programming** and click **Visual Studio Code**.
3. Press **Ctrl + Shift + X** to open the **Extensions** sidebar.
4. Search for **ESLint** and install the one provided by **Microsoft**.

For this project, we only need to install one extension. However, we may install more extensions in a future project.

## Installing Additional Software

To run our JavaScript code, we need a runtime environment like [**Node.js**][NODEJS]. While we could install it manually, I chose to use [**Pi-Apps**][PI-APPS] to make things easier. You can think of **Pi-Apps** as a Google Play Store for Raspberry Pi. Here is the installation code from their [**official website**][PI-APPS-INSTALL]:

```bash
wget -qO- https://raw.githubusercontent.com/Botspot/pi-apps/master/install | bash
```

Having done that, open **Pi-Apps** by either typing `pi-apps` in the terminal or by clicking the desktop shortcut.

![Installing Node.js using Pi-Apps][INSTALLING-NODEJS]

1. Click **Tools**, then **Node.js**.
2. Click **Install** and wait for a few minutes.

Installing **Node.js** through **Pi-Apps** also installs Node Version Manager (**NVM**), which is beneficial for managing multiple versions of Node.js for various projects. I will cover NVM and its applications in a future post.

## Running the First Line of Code

Phew! After much preparation, we are finally ready to write our first line of code on a Raspberry Pi! 🙈

Go to the Visual Studio Code window and follow these steps:

1. From the menubar, go to **File** > **Open Folder...**. Create a new folder named `test` in the home directory.
2. Create a new file named `index.js` in the Explorer.
3. From the menubar, click **Terminal** > **New Terminal**.

Verify the installation of **Node.js** by running the following command:

```bash
node -v
```

Write the following JavaScript code into `index.js`:

```javascript
function main() {
	console.log('Hello World')
}

main()
```

Then run the following:

```bash
node .
```

If everything is okay, we should see **Hello World** printed in our terminal. Congrats! We just wrote our first JavaScript on a **Raspberry Pi** 🎉

![First line of code in Raspberry Pi][HELLO-WORLD]

## Benchmarks

I used the built-in **Raspberry Pi Diagonistics** tool to perform a speed test in both micro SD card and SSD. Here are the results:

| Comparsion             | Micro SD Card | External USB SSD   |
| :--------------------- | :------------ | :----------------- |
| Sequential write speed | 26.828 MB/sec | **335.517 MB/sec** |
| Random write speed     | 1249 IOPS     | **33098 IOPS**     |
| Random read speed      | 3356 IOPS     | **36963 IOPS**     |

As we can see, the speed of an external SSD dramatically surpasses that of a micro SD card. Now, some of you might think the test isn't fair as I am comparing a **64GB** micro SD card with a **256GB** SSD.

However, the theoretical maximum speed of a USB 3.0 device is **625 MB/s**, which exceeds the maximum speed of a micro SD card, typically around **104 MB/s**. Also, micro SD cards aren't designed for continuous data rewrites. So, they tend to get corrupt in a Raspberry Pi sooner than an external SSD.

Taking everything into account, opting for an external SSD seems like a good decision.

## Accessing the Pi Remotely

There are times when we might want to run the Raspberry Pi without a monitor. We can do this over our local WiFi by using remote access software like [**RealVNC Viewer**][REALVNC]. Here's how to set it up:

1. Enable VNC on the **Raspberry Pi** by opening the applications menu, **Preferences** > **Raspberry Pi Configuration**. Head over to **Interfaces** and toggle **VNC** on.

    ![Enable VNC on the Raspberry Pi][ENABLE-VNC]

2. Download and install the [**RealVNC Viewer**][REALVNC] on your main computer.

3. Run the **RealVNC Viewer** executable.

4. Go to **File** > **New Connection...**.

5. Update the text field **VNC Server** to the hostname of your Raspberry Pi.

    ![Type VNC server hostname to connect][VNC-01]

6. Type the **username** and **password** in the dialog box.

    ![Type the username and password of the Raspberry Pi][VNC-02]

If everything goes right, we should see the desktop of our Raspberry Pi on our main computer 🎉

![Desktop view of Raspberry Pi through RealVNC][VNC-03]

## What's Next?

Setting up a Raspberry Pi 5 for the first time to run JavaScript code on it has been a great experience. I have done my best to cover all the basics so that any beginner can follow along. This is also the first post in the **"Raspberry Pi Programming"** series here on Dev Community 🚀

We both learned a lot in this journey. Feel free to ask any questions about the post or chat in the comments. See you soon! 🙈✨

<center><a href="https://codepen.io/ShadowShahriar"><b>CodePen</b></a> | <a href="https://www.threads.net/@shadowshahriar"><b>Threads</b></a> | <a href="https://wokwi.com/makers/shadowshahriar"><b>Wokwi</b></a> | <a href="https://hashnode.com/@ShadowShahriar"><b>Hashnode</b></a></center>

<!--- images --->

[GETTING-STARTED]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/getting-started-01.jpg
[STORAGE-01]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/storage-02.jpg
[STORAGE-02]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/storage-01.jpg
[IMAGER-01]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/imager-01.png
[IMAGER-02]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/imager-02.png
[IMAGER-03]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/imager-03.png
[IMAGER-04]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/imager-04.png
[IMAGER-05]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/imager-05.png
[DESKTOP-VIEW]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/desktop.jpg
[INSTALLING-VSCODE]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/installing-vscode.png
[INSTALLING-EXTENSIONS]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/installing-extensions.png
[INSTALLING-NODEJS]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/installing-nodejs.png
[HELLO-WORLD]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/first-line-of-code.png
[ENABLE-VNC]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/enable-vnc.png
[VNC-01]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/realvnc-01.png
[VNC-02]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/realvnc-02.png
[VNC-03]: https://shadowshahriar.github.io/DEV/01-getting-my-hands-on-the-raspberry-pi-5/images/realvnc-03.png

<!--- links --->

[RBD-SET]: https://store.roboticsbd.com/raspberry-pi/2440-raspberry-pi-5-8gb-complete-set-robotics-bangladesh.html
[RBD-PI5]: https://store.roboticsbd.com/raspberry-pi/2439-raspberry-pi-5-8gb-robotics-bangladesh.html
[RBD-AC]: https://store.roboticsbd.com/raspberry-pi/1081-raspberry-pi-5-active-cooler-robotics-bangladesh.html
[RBD-PWR]: https://store.roboticsbd.com/raspberry-pi/1082-official-27w-usb-c-pd-power-supply-for-raspberry-pi-5-white-robotics-bangladesh.html
[RBD-HDMI]: https://store.roboticsbd.com/raspberry-pi/1145-micro-hdmi-male-to-hdmi-male-cable-for-pi-4-or-5-robotics-bangladesh.html
[RPI-CASE]: https://www.raspberrypi.com/products/raspberry-pi-5-case/
[RYANS-SDCARD]: https://www.ryans.com/transcend-300s-64gb-microsdxc-sdhc-uhs-i-u1-memory-card
[RYANS-MKC]: https://www.ryans.com/aula-ac308-black-wireless-keyboard-and-mouse-combo
[RYANS-SSD]: https://www.ryans.com/transcend-esd310c-256gb-usb-type-a-and-type-c-otg-black-portable-ssd
[RPI-SOFT]: https://www.raspberrypi.com/software/
[RPI-USB-BOOT]: https://www.youtube.com/watch?v=xsSgJo7SRaA
[RPI-AC-INSTALL]: https://www.youtube.com/watch?v=go6safw8uQU&t=10s
[FORUM-REPLY]: https://forums.raspberrypi.com/viewtopic.php?t=385208#p2301851
[PI-APPS-INSTALL]: https://pi-apps.io/install/
[PI-APPS]: https://pi-apps.io/
[NODEJS]: https://nodejs.org/en
[REALVNC]: https://www.realvnc.com/en/connect/download/viewer/
