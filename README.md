# Final Fantasy Call Automation with Tasker & Termux

This guide will walk you through setting up an automation system on your Android phone using **Tasker** and **Termux**. The goal is to:
- Set a **Final Fantasy VI Battle Theme** ringtone for your incoming calls.
- Play the **Final Fantasy VI Victory Fanfare** after you end a call.

## Requirements

- **Tasker**: A powerful automation app for Android.
- **Termux**: A terminal emulator for Android that allows running scripts and commands.
- **Media files**: 
  - "Final_Fantasy_VI_Battle_Theme_-_Metal_Cover_-_editied.mp3" (for ringtone)
  - "Final_Fantasy_VI_-_Victory_Fanfare_Metal.mp3" (for victory fanfare)

## Step 1: Install Termux and Tasker

1. **Install Termux**: Download and install Termux from F-Droid or the Play Store.
2. **Install Tasker**: Download and install Tasker from the Play Store.

## Step 2: Set up Termux Script

### 2.1 Install required packages

Open Termux and install the necessary packages to control media playback:

```bash
pkg install termux-api
```

### 2.2 Create Termux Script

Create a new script that will play the **Victory Fanfare** after a call ends.

1. Open Termux and create the script file `play_victory.sh`:

```bash
nano ~/play_victory.sh
```

2. Paste the following script content:

```bash
#!/bin/bash

# Path to your victory fanfare file
victory_fanfare="/storage/emulated/0/Music/Final_Fantasy_VI_-_Victory_Fanfare_Metal.mp3"

# Check if the file exists
if [ -f "$victory_fanfare" ]; then
    # Use termux media player to play the audio
    termux-media-player play "$victory_fanfare"
else
    echo "Victory fanfare file not found!"
fi
```

3. Make the script executable:

```bash
chmod +x ~/play_victory.sh
```

**Note**: Ensure the path to the `Victory_Fanfare_Metal.mp3` is correct and matches your file location.

## Step 3: Set up Tasker Automation

### 3.1 Create Trigger in Tasker

1. Open **Tasker** and create a new profile.
2. Choose **Event → Phone → Call End** to trigger the task after the call ends.

### 3.2 Create Task to Run Termux Script

1. Inside the profile, add a new **Task** and name it (e.g., `PlayVictoryFanfare`).
2. Add an **Action → Code → Run Shell**.
3. Set the command to:

```bash
bash ~/play_victory.sh
```

4. Ensure **Use Root** is not selected since we're running a non-root setup.

### 3.3 Set Incoming Ringtone (Optional)

You can also automate setting your ringtone to **Battle Theme** by adding this action to the same task:

1. Add an **Action → Audio → Ringtone**.
2. Select the path to your **Battle Theme** MP3 file.

## Final Notes

- **No root required**: This setup works without root access.
- **Permissions**: Make sure that Termux has permission to access your phone's storage and Tasker can run the script.
- **File paths**: Ensure the paths to your MP3 files are correct.

Enjoy your automated Final Fantasy experience! 🎮✨
