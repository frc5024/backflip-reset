# Darth Raider recovery instructions

This guide will cover how to reset **Darth Raider** to a known working state without requiring any complicated development tools.

For programmers and mentors, the last known working version of the [InfiniteRecharge](https://github.com/frc5024/InfiniteRecharge) codebase was commit: `d96fb57bc22d2a0b6e5259946c21bc18feeee1f8`. This was used in a real game.

## Software prerequisites

The following software is required to complete this guide:

- Java
  - Click [here](https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.13%2B8/OpenJDK11U-jdk_x86-32_windows_hotspot_11.0.13_8.msi) to install JDK11 if using **Windows**
  - Linux users should install Java via [sdkman](https://sdkman.io/)
- An SSH client
  - Install [PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.76-installer.msi) if using windows
  - Linux users should know how to use OpenSSH instead

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

Once this is done, power down the radio and the robot, plug everything back together on the robot itself, and then power the robot back up.

## Rebuilding the vision pipeline

I can't remember the configuration process for the Limelight, but I do remember that the `vpr` file that defines how to detect the upper goal on the field can be found [here](https://raw.githubusercontent.com/frc5024/InfiniteRecharge/master/src/main/limelight/2020default.vpr).

I don't think there is any reason to reset the Limelight, since it has not been touched at all. If reprogramming is needed, check out the documentation at [limelightvision.io](https://docs.limelightvision.io/en/latest/getting_started.html).

I'm sure someone can figure out how to save and restore the state of the Limelight if absolutely necessary.

## Re-flashing the RoboRIO

At this point, you will want to connect your computer to the RoboRIO itself via a USB cable. For this process, we are going to manually perform the steps required to load new code onto a robot without using the development tools.

First, open PuTTY, and set the following settings:

| Setting         | Value                                                              |
|-----------------|--------------------------------------------------------------------|
| Host Name       | `172.22.11.2` (or `10.50.24.2` if you *need* to connect over wifi) |
| Port            | 22                                                                 |
| Connection type | SSH                                                                |

Then press `Open`.

This will connect you straight into the RoboRIO terminal. Your username is `admin`, and simply press <kbd>Enter</kbd> when asked for a password. **Be extremely careful here** spelling mistakes and mis-clicks may seriously corrupt the robot, which will require a full firmware reset and development tools to fix.

Run the following command (spaces and slashes are important):

```sh
cd /home/lvuser
```

Next, we need to kill the robot manually (this is a bit like a software E-stop):

```sh
/usr/local/frc/bin/frcKillRobot.sh -t
```

Now, leave the PuTTY window open, and open the windows file explorer. In the file location / address bar, enter the following:

```text
ftp://172.22.11.2
```

You are now accessing the robot's internal filesystem. Once again, be careful. Navigate to `home` then `lvuser`.

Somewhere in this area you should see a `.jar` file (or a few). Delete them, then paste [this file]() into the folder.