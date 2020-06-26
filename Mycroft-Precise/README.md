# Mycroft-Precise

## Introduction:

This project has been possible due to the tools provided by MycroftAI. Tux is (for now) simply the voice assistant Mycroft - provided by MycroftAI. The reason that the voice assistant Mycroft now responds when we call out "Hey Tux!" is due to the [mycroft-precise tool](https://mycroft.ai/initiatives/#precise). It is a wake-word listener which means that it helps the voice assistant figure out when it is being called. I used this tool to create "Hey Tux!" as a wake-word. [MycroftAI's website](https://mycroft.ai/initiatives/#precise) has a detailed description as well as the [documentation](https://mycroft-ai.gitbook.io/docs/mycroft-technologies/precise) for it if you want to delve in deeper.  

## Obtaining mycroft-precise:

If you would like to give the voice assistant a different name (call it using a different name), the tool that you need to use is mycroft-precise which is provided by MycroftAI. The version of mycroft-precise that is compatible with the Master branch of Mycroft (which is what is now being called Tux) is 0.2.0. They provide version 0.2.0 on [this website](https://github.com/MycroftAI/mycroft-precise/releases/tag/v0.2.0). All you have to do is download the file *precise-engine_0.2.0_x86_64.tar.gz* to a place where it is easily accessible (I moved it to my home directory) and unzip it using the following command:

```bash
tar -xvf precise-engine_0.2.0_x86_64.tar.gz
```

## Installing mycroft-precise:

In order to install mycroft-precise, run the following commands:

```bash
cd mycroft-precise-0.2.0
./setup.sh
```

Right after installation, mycroft-precise wasn't working for me. The following commands helped me solve my issues:

```bash
source .venv/bin/activate
pip install 'prettyparse<1.0'
pip install keras==2.1.5
```

The reason, as you might have already guessed, was due to mis-alignment of versions of the software that is being utilized. If after using the above-mentioned commands mycroft-precise is still not running for you, read the *requirements.txt* that is in the *mycroft-precise-0.2.0* directory. Make sure that all versions of the software named in this text file aligns with the versions of that software within the virtual environment (I would not recommend applying those versions for your whole machine as they might be outdated).

## Running mycroft-precise:

In order to run mycroft-precise we need to activate the virtual environment which will be done by:

```bash
source .venv/bin/activate
```

