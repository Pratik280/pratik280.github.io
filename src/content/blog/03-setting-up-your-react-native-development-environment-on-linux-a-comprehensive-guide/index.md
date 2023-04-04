---
author: Pratik Chandlekar
pubDatetime: 2023-03-25T17:05:16Z
title: "Linux Devs Rejoice: A Comprehensive Guide to Setting Up Your React Native Development Environment"
postSlug: "linux-devs-rejoice-a-comprehensive-guide-to-setting-up-your-react-native-development-environment"
featured: false
draft: false
tags:
  - "linux-desktop"
ogImage: ""
description: A comprehensive guide on how to set up a developer environment for React Native in Linux. From installing Node.js, Java-OpenJDK, VSCodium, to configuring Android Studio, this guide covers everything you need to get started with React Native development in Linux.
---

## Table of contents

## Introduction

React native is open source framework created by facebook, which is used to develop mobile apps using javascript and react. In this article, we will learn how to start with react-native development on linux by installing all the necessary tools. At the end of the article you will have a bare bones "Hello world" react-native application running in your system.

I will primarily be using Arch Linux for this guide, but whenever necessary, I will also provide instructions for other popular Linux distributions such as Fedora and Ubuntu.

We will require these 4 tools for setting up developer environment for react-native.

1. Node JS
1. Java OpenJDK
1. Android Studio
1. Visual Studio Code

## Installing and Setting up NodeJS

To manage Node.js versions, we'll be using Node Version Manager (NVM), which is compatible with any Linux distribution. NVM offers the flexibility to install and switch between multiple Node.js versions on our system, enabling us to work with different projects that require specific versions of Node.js. You can learn more about nvm [here](https://github.com/nvm-sh/nvm).

**Steps for installing and setting up NodeJs using nvm:**

Open [this link](https://github.com/nvm-sh/nvm#installing-and-updating) to download nvm. Where you will get the script to download and install nvm OR Just copy paste the below command in your terminal.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

After downloading NVM, refresh your Bash session with the following command:

```bash
bash
```

Run the following command to verify the nvm installation:

```bash
nvm --verion
```

We're now ready to install Node.js using NVM, and we'll be installing the Long-Term Support (LTS) version. To do so, execute the following command:

```bash
nvm install --lts
```

Again refresh your Bash session with the following command:

```bash
bash
```

Verify your node js download using the following command:

```bash
node -v
```

## Installing and Setting up Java OpenJDK

### To install java openJDK use the following command:

- for arch and arch based linux distros.

  ```bash
  sudo pacman -S jdk11-openjdk
  ```

  For more info check [Arch wiki](https://wiki.archlinux.org/title/java).

- for ubuntu and ubuntu based linux distros.

  ```bash
  sudo apt install openjdk-11-jdk
  ```

  For more info check [help.ubuntu.com/community/Java](https://help.ubuntu.com/community/Java).

- for fedora and fedora based linux distros.

  ```bash
  sudo dnf install java-11-openjdk.x86_64
  ```

  For more info check [docs.fedoraproject.org](https://docs.fedoraproject.org/en-US/quick-docs/installing-java/).

### Adding JAVA_HOME environment variable in bashrc.

To add the JAVA_HOME environment variable, edit the .bashrc file located in the home directory (which is a hidden file). Simply copy and paste the following content to add the JAVA_HOME variable in .bashrc.

- for arch and arch based linux distros.

  ```bash
  export JAVA_HOME=/usr/lib/jvm/java-11-openjdk/
  ```

- for ubuntu and ubuntu based linux distros.

  ```bash
  export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
  ```

- for fedora and fedora based linux distros.

  ```bash
  export JAVA_HOME=/usr/lib/jvm/jre-11-openjdk
  ```

## Installing and Setting up Visual Studio Code

I would recommend using VSCodium, which is functionally identical to VSCode but is a free and open-source alternative.

- For Arch and Arch based linux distros

  To install [VSCodium](https://vscodium.com/) we'll use the following command to download it from the AUR (Arch User Repository) on Arch Linux:

  ```
  yay -S vscodium-bin
  ```

- For Ubuntu and Ubuntu based linux distros use the following commands:

  ```bash
  wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \
      | gpg --dearmor \
      | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
  ```

  ```bash
  echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \
      | sudo tee /etc/apt/sources.list.d/vscodium.list
  ```

  ```bash
  sudo apt update && sudo apt install codium
  ```

- For Fedora and Fedora based linux distros use the following commands:

  ```bash
  sudo rpmkeys --import https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/-/raw/master/pub.gpg
  ```

  ```bash
  printf "[gitlab.com_paulcarroty_vscodium_repo]\nname=download.vscodium.com\nbaseurl=https://download.vscodium.com/rpms/\nenabled=1\ngpgcheck=1\nrepo_gpgcheck=1\ngpgkey=https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/-/raw/master/pub.gpg\nmetadata_expire=1h" | sudo tee -a /etc/yum.repos.d/vscodium.repo
  ```

  ```bash
  sudo dnf install codium
  ```

## Installing and Setting up Android Studio

### Install android-studio.

1. Installing android-studio (on any linux distro)

- Download the Android Studio tar file from the [android studio official site](https://developer.android.com/studio), and then extract it using your preferred method.
- Once extracted, go inside its bin folder and run the studio.sh.

  ```bash
  ./studio.sh
  ```

2. Installing android on arch and arch based distros.

   For Arch Linux and its derivatives, an AUR package is also available which can be downloaded using the following command:

   ```bash
   yay -S android-studio
   ```

### Adding the necessary paths in bashrc for proper working of andoid-studio

To ensure the proper functioning of Android Studio, we need to add the necessary paths to the .bashrc file.
Copy and paste the following content into your .bashrc file.

```bash
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/tools
```

### Adding android device for testing our react native application

For setting up Android device. There are two ways

1. Using physical device by connecting to computer using usb cable.

   To test your React Native application on a physical device, connect your Android device to your PC using a USB cable. Ensure that USB debugging is enabled in your Android device's developer options, and select file transfer mode for the USB connection.

1. Creating a virtual device in Android Studio.
   For a more detailed guide on creating virtual devices in Android Studio, you can refer to the [official guide](https://developer.android.com/studio/run/managing-avds.html).
   - Open Android Studio click on “More Action” then click “Virtual Device Manager”
     ![Opening Virtual Device Manager in Android Studio](/assets/03-setting-up-your-react-native-development-environment-on-linux-a-comprehensive-guide/virtual-device-manager.png)
   - Select a device which has Google play icon in Playstore column. From official documentation “A device definition labeled with the Google Play logo in the **Play Store** column includes both the Google Play Store app and access to Google Play services, including a **Google Play** tab in the **Extended controls** dialog that provides a convenient button for updating Google Play services on the device.”
     ![Selecting Android Virtual Device in Android Studio](/assets/03-setting-up-your-react-native-development-environment-on-linux-a-comprehensive-guide/avd.png)
   - Click on the play icon to launch avd.
     ![Android Virtual Machine in Android Studio](/assets/03-setting-up-your-react-native-development-environment-on-linux-a-comprehensive-guide/avd-launched.png)
   - If the emulator doesn't launch or terminates instantly, you can launch it from the terminal to see the logs and diagnose any issues.
     In my case, the emulator failed to launch due to a missing _libpulse_ library, which I resolved by downloading it.
   - Navigate to your Android folder, which for me is located at ~/Android/Sdk, to start the emulator from the terminal
     ```bash
     cd ~/Android/Sdk/emulator
     ```
   - Run this command to list the avds
     ```bash
     ./emulator -list-avds
     ```
   - Then run this command to start the avd
     ```bash
      ./emulator @<AVD_NAME>
      ./emulator @Pixel_4_API_33
     ```

## Starting with react-native.

To ensure everything is working, we will create a simple HelloWorld project in React Native.

Create a react-native project by executing the following command:

```bash
npx react-native init <ProjectName>
```

```bash
npx react-native init Hello
cd Hello
```

Open the "Hello" folder in VSCodium/VSCode.

Open two separate terminals in the same folder and run these two commands.

```bash
npx react-native start
```

```bash
npm run android
```

You will see the application running in your android device.

> I recommend installing the "ES7+ React/Redux/React-Native snippets" extension by the publisher "dsznajder" in VSCodium/VSCode. This extension provides snippets that enable you to generate React Native components quickly and easily.

In VSCodium/VSCode, open the App.tsx file and delete its contents to start fresh. Type 'rnfes', and VSCode will automatically suggest the snippet from the extension we installed earlier. This snippet will create a simple component for us.

App.tsx

```javascript
import { StyleSheet, Text, View } from "react-native";
import React from "react";

const App = () => {
  return (
    <View>
      <Text>Hello</Text>
    </View>
  );
};

export default App;

const styles = StyleSheet.create({});
```

Once you save the file, the application will display a simple 'Hello' message.

![Hello Application ready using React Native](/assets/03-setting-up-your-react-native-development-environment-on-linux-a-comprehensive-guide/hello-app.png)

## Conclusion

Congratulations, you have successfully set up your development environment for React Native on Linux! By installing and configuring Node.js, Java OpenJDK, VSCodium, and Android Studio, you are now equipped with the necessary tools to develop high-quality mobile applications using React Native. With these tools in place, you can start exploring the vast potential of React Native and begin building amazing apps that will run seamlessly on Android platform. I hope this guide has been helpful, and I wish you all the best in your React Native development journey.

:)
