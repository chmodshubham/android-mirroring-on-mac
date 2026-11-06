# Wireless Android Screen Mirroring on macOS

This guide explains how to mirror and control your Android device from a Mac over Wi-Fi using scrcpy.

### Prerequisites

- An Android device

- A Mac computer

- Both devices must be connected to the exact same Wi-Fi network

### Step 1: Prepare the Android Device

1. Open your phone Settings.

2. Navigate to About Phone > Software Information.

3. Tap Build Number 7 times to unlock Developer Options.

4. Go back to the main Settings menu and open Developer Options.

5. Disable Auto Blocker. You must disable this to allow USB Debugging.

> [!NOTE]
> Auto Blocker automatically resets and turns back on after 30 minutes, so ensure it is disabled right before you connect.

6. Toggle on USB Debugging.

### Step 2: Prepare the Mac

If you do not already have Homebrew installed on your Mac, install it first via your Terminal. Then, install the required Android debugging tools and the mirroring application.

1. Open the Terminal application.

2. Install the Android platform tools by running:

```bash
brew install --cask android-platform-tools
```

3. Install the screen mirroring tool by running:

```bash
brew install scrcpy
```

### Step 3: Initial Setup and Connection

You will need a USB cable for the initial configuration.

1. Plug your Android phone into your Mac using a USB cable. If prompted on the phone, allow the computer access.

2. In the Mac Terminal, enable the wireless listening port by running:

```bash
adb tcpip 5555
```

3. Find your phone's local IP address by going to Settings > Wi-Fi on your phone and tapping your current network.

4. Connect to the phone wirelessly by running:

```bash
adb connect YOUR_PHONE_IP:5555
```

5. Unplug the USB cable.

6. Launch the screen mirror by running:

```bash
scrcpy
```

### Reconnecting Later

Once the initial setup is complete, you will rarely need the USB cable.

**When you DO NOT need the USB cable:**
You do not need the physical cable in the following situations:

- You close the Terminal.

- You restart your Mac.

- You close the scrcpy window.

- You change to a new Wi-Fi network.

Simply ensure both devices are on the same Wi-Fi network, check your phone for its current IP address, and run:
`adb connect YOUR_PHONE_IP:5555`. Then run `scrcpy` to launch the mirror.

**When you DO need the USB cable:**
You only need to plug the phone back into the Mac if the background debugging service drops. This happens when:

- You restart your phone.

- Your phone runs out of battery.

- The Android operating system forcefully closes background services to save battery.

If any of these occur, you must plug the USB cable in, verify that Auto Blocker is still disabled, and run `adb tcpip 5555` again to reinitialize the wireless port before connecting over Wi-Fi.
