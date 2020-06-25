# Voice Assistant - Tux

## Getting Started with Tux

### Step 1: Retrieving Mycroft Tools (only runs on Linux)

```bash
cd ~/
git clone https://github.com/MycroftAI/mycroft-core.git/tree/master
cd mycroft-core
bash dev_setup.sh
```

  * Y (run on stable ‘master’ branch)
  * Y (automatically update)
  * N (not needed if you have an internet connection at all times)
  * Y (make Mycroft’s job easier)
  * Y (automatically check code when submitting)

### Step 2: Implementing Tux:

The first thing that needs to be done is to copy Hey-Tux.tgz file in `.mycroft/precise/` folder. Before moving on to the next step, unzip the `Hey-Tux.tgz` in the same folder (`.mycroft/precise/`) using the following command:

```bash
tar -xvzf Hey-Tux.tgz
```

Next, follow the following steps to implement Tux:

```bash
cd ~/
cd mycroft-core
./bin/mycroft-config edit user
```

In the window that appears, copy the following code (you can choose to put `Hey-Tux-Old.pb` in place of `Hey-Tux-New.pb` if you want to try the older Precise wake-word model for Tux).

```javascript
{
  "max_allowed_core_version": 20.2,
  "listener": {
    "wake_word": "hey tux"
  },
  "hotwords": {
    "hey tux": {
        "module": "precise",
        "local_model_file": "/home/shahzeb/.mycroft/precise/Hey-Tux-New.pb"
    }
  }
}
```

Press *`Ctrl + S`* to save and *`Ctrl + X`* to exit the window. Next type the following command:

```bash
./bin/mycroft-config reload
```

### Step 3: Starting Tux:

If you would like to see what Tux is hearing, and also see what Tux is saying, type the following command. This will bring an interface to interact with Tux.

```bash
./start-mycroft.sh debug
```

Press *`Ctrl + C`* to exit the interface (this will also close all Tux services). If you want Tux to work in the background without an interface, type the following command:

```bash
./start-mycroft.sh all
```

To end all background services of Tux, simply type:

```bash
./stop-mycroft.sh
```

### Support or Contact

If you have any questions, comments, or concerns, you can email me at shahzeb.jadoon.sj@gmail.com


