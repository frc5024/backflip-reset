# Darth Raider recovery instructions

This guide will cover how to reset **Darth Raider** to a known working state without requiring any complicated development tools.

## Software prerequisites

The following software is required to complete this guide:

- Java
  - Click [here](https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.13%2B8/OpenJDK11U-jdk_x86-32_windows_hotspot_11.0.13_8.msi) to install JDK11 if using **Windows**
  - Linux users should install Java via [sdkman](https://sdkman.io/)


## Re-flashing the router to "home field mode"

*This section should only need to be performed once*

To re-flash the router on **Darth Raider**, you will need to download the [radio configuration utility](https://github.com/frc5024/backflip-reset/raw/master/firmware/radio/FRC_Radio_Configuration_20_0_0.exe) (Windows only software). 

Use an ethernet cable to connect your computer to the ethernet port *closest* to the router's power port. After this is done, plug the router in to power. A robot is a valid power source, just don't plug the robot's main ethernet cable itself into the router while doing this process. Finally, run the configuration utility.

After running the utility, you can follow WPI's guide on flashing your router starting at the *"Allow the program to make changes"* section:

[WPI Router Programming Guide](https://docs.wpilib.org/en/2020/docs/getting-started/getting-started-frc-control-system/radio-programming.html#allow-the-program-to-make-changes-if-prompted)

**Make sure to set the following settings:**

| Setting     | Value               |
|-------------|---------------------|
| Team Number | 5024                |
| Robot Name  | Darth Raider        |
| WPI Key     | `raiderrobotics`    |
| Firewall    | Disabled            |
| BW Limit    | Disabled            |
| Radio       | OpenMesh            |
| Mode        | 2.4GHz Access Point |

You will need to *Load Firmware* and *Configure*. So make sure to follow the entirety of WPI's guide.

