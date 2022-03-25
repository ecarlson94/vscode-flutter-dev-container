# Learn Flutter!<!-- omit in toc -->

A new Flutter project.

## Table of Contents<!-- omit in toc -->
- [Requirements](#requirements)
   - [MacOS/Windows](#macoswindows)
   - [Emulation](#emulation)
- [Getting Started](#getting-started)
   - [Web Hosting](#web-hosting)
   - [Android USB/Wireless Debugging](#android-usbwireless-debugging)
      - [Linux](#linux)
      - [MacOS/Windows](#macoswindows-1)
   - [Android Emulator (WIP)](#android-emulator-wip)
      - [Linux](#linux-1)
      - [MacOS/Windows](#macoswindows-2)
- [Resources](#resources)

## Requirements

- [VSCode](https://code.visualstudio.com/)
  - Extensions:
    - [Visual Studio Code Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [Docker](https://docs.docker.com/get-docker/)

### MacOS/Windows

- [adb (if using Wireless debugging or Android emulator)](https://developer.android.com/studio/releases/platform-tools#downloads)
  - Add `adb` executable to your PATH variable

### Emulation

- [Android Studio](https://developer.android.com/studio)
- [Android Virtual Device](https://developer.android.com/studio/run/managing-avds)

## Getting Started

1. Open folder in VSCode
1. Click `Reopen in container` from bottom right prompt

### Web Hosting

1. In a terminal inside the container, run the following command at the root of the repository
   ```bash
   flutter-web
   ```

The application should be accessible at `http://localhost:8090`

### Android USB/Wireless Debugging

Ensure developer mode is turned on and USB Debugging (Wireless Debugging for MacOS/Windows) is enabled on the mobile device.
1. Connect your android device
1. Set the connection mode to `PTP` or `File transfer / Android Auto` inside the mobile device.

   ![image](https://user-images.githubusercontent.com/6665964/141025055-1ee27ecb-b912-47c1-94d3-7cc09da6bc9a.png)

#### Linux

1. Uncomment the portions of [.devcontainer/devcontainer.json](./.devcontainer/devcontainer.json) related to `Linux OS Host` and `USB Debugging Support`
1. Open command pallete in VS Code and select `Remote-Containers: Rebuild Container`
1. Run the following command at the root of the repository
   ```bash
   flutter run
   ```

#### MacOS/Windows

Your android device and computer will need to be on the same network. Since USB passthrough cannot be accomplished on Mac and Windows, we will configure debugging over the network.

In a terminal the host machine:
1. Run the following command to see the list of connected devices
   ```bash
   adb devices
   ```
1. Run the following commands to connect to the device wirelessly
   ```bash
   adb tcpip 555
   adb connect <phone ip address>
   adb devices
   ```
1. Disconnect your android device and re-run `adb devices` to verify that the device is still connected wirelessly

Inside dev container
1. Open folder in VSCode
1. Click `Reopen in container` from bottom right prompt
1. Run the following command to see the list of connected devices
   ```bash
   adb devices
   ```
1. Run the following commands to connect to the device wirelessly
   ```bash
   adb connect <phone ip address>:5555
   adb devices
   ```
   1. If you get `device unauthorized`, run the following commands:
      ```bash
      adb kill-server
      adb connect <phone ip address>:5555
      adb devices
1. Run the following command at the root of the repository
   ```bash
   flutter run
   ```

### Android Emulator (WIP)

#### Linux

1. Uncomment the portions of [.devcontainer/devcontainer.json](./.devcontainer/devcontainer.json) related to `Linux OS Host` and `Android Emulator Support`
1. Connect your android device
1. Open command pallete in VS Code and select `Remote-Containers: Rebuild Container`
1. In a terminal inside the container, run the following command at the root of the repository
   ```bash
   flutter emulators --launch flutter_emulator
   ```
1. In a new terminal inside the container, run the following command at the root of the repository
   ```bash
   flutter run
   ```

#### MacOS/Windows

1. Download Android SDK Platform tools.zip and extract files
   - Windows: https://dl.google.com/android/repository/platform-tools-latest-windows.zip
   - MacOS: https://dl.google.com/android/repository/platform-tools-latest-darwin.zip
1. Start your local android emulator and run the following command on the host to make the emulator accessible via the network
   - For Windows: Open folder containing extracted Android SDK Platform tools files and run command prompt from that location to use adb commands
   ```bash
   adb tcpip 5555
   ```
1. In a terminal inside the docker container, run the following command to connect to the emulator
   ```bash
   adb connect host.docker.internal:5555
   ```
1. In a terminal inside the container, run the following command at the root of the repository
   ```bash
   flutter run
   ```

## Resources
- [matsp/docker-flutter](https://github.com/matsp/docker-flutter)
- [How to dockerize Flutter apps, Souvik Biswas](https://blog.codemagic.io/how-to-dockerize-flutter-apps/)

