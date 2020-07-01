# Mycroft-Precise

## Introduction:

This project has been possible due to the tools provided by MycroftAI. Tux is (for now) simply the voice assistant Mycroft - provided by MycroftAI. The reason that the voice assistant Mycroft now responds when we call out "Hey Tux!" is due to the [mycroft-precise tool](https://mycroft.ai/initiatives/#precise). It is a wake-word listener which means that it helps the voice assistant figure out when it is being called. I used this tool to create "Hey Tux!" as a wake-word. [MycroftAI's website](https://mycroft.ai/initiatives/#precise) has a detailed description as well as the [documentation](https://mycroft-ai.gitbook.io/docs/mycroft-technologies/precise) for it if you want to delve in deeper.  

## Obtaining mycroft-precise:

If you would like to give the voice assistant a different name (call it using a different name), the tool that you need to use is mycroft-precise which is provided by MycroftAI. Something that I got to learn later into the process (which I wish I would've known earlier) was that it is suggested (even recommended) that the wake-word you choose have at least *`three syllables`*. 

The version of mycroft-precise that is compatible with the Master branch of Mycroft (which is what is now being called Tux) is 0.2.0. They provide version 0.2.0 on [this website](https://github.com/MycroftAI/mycroft-precise/releases/tag/v0.2.0). All you have to do is download the file `precise-engine_0.2.0_x86_64.tar.gz` to a place where it is easily accessible (I moved it to my home directory) and unzip it using the following command:

```bash
tar -xvf precise-engine_0.2.0_x86_64.tar.gz
```

## Installing mycroft-precise:

In order to install mycroft-precise, run the following commands:

```bash
cd mycroft-precise-0.2.0
./setup.sh
```

After installation, mycroft-precise wasn't working for me. The following commands helped me solve my issues:

```bash
source .venv/bin/activate
pip install 'prettyparse<1.0'
pip install keras==2.1.5
```

The reason, as you might have already guessed, was due to mis-alignment of versions of the software that is being utilized. If after using the above-mentioned commands mycroft-precise is still not running for you, read the `requirements.txt` that is in the `mycroft-precise-0.2.0` directory. Make sure that all versions of the software named in this text file aligns with the versions of that software within the virtual environment (I would not recommend applying those versions for your whole machine as they might be outdated).

## Running mycroft-precise:

In or der to run mycroft-precise, we need to activate the virtual environment which will be done by:

```bash
source .venv/bin/activate
```

## How to Train Your Own Wake-Word:

Precise comes with a few executables used to train and test models. Here's a summary of all the executables:

1. `precise-collect` - Record (audio) wake-word samples for Precise
2. `precise-train` - Train a new model on a dataset (initial training)
3. `precise-train-incremental` - Reduce false activations (Train a model to inhibit activation by
                                 marking false activations and retraining)
4. `precise-test` - Statistics on dataset accuracy (Test a model against a dataset)
5. `precise-listen` - Real world test with your microphone (Run a model on microphone audio input)
6. `precise-convert` - Convert wake-word model from Keras to TensorFlow (from *.net* to *.pb*)

### 1. precise-collect:

The first step to the process of training your own wake-word is recording your own wake word. This can be done by the `precise-collect` command (within the virtual environment). I also recorded with my laptop's microphone because it matches the regular microphones that are used within smart devices these days. The following [example](https://github.com/MycroftAI/mycroft-precise/wiki/Training-your-own-wake-word#how-to-train-your-own-wake-word) is what MycroftAI's team has posted on their website:

```bash
$ precise-collect
Audio name (Ex. recording-##): hey-computer.##
ALSA lib pcm_dsnoop.c:638:(snd_pcm_dsnoop_open) unable to open slave
ALSA lib pcm_dmix.c:1099:(snd_pcm_dmix_open) unable to open slave
ALSA lib pcm_dmix.c:1099:(snd_pcm_dmix_open) unable to open slave
Press space to record (esc to exit)...
Recording...
Saved as hey-computer.00.wav
Press space to record (esc to exit)...
```

The name `hey-computer` is used for explaining purposes, and can be changed to anything you want to. For future reference as well, the name `hey-computer` can be swapped with whatever you want, even for the names of folders and the name of the model.

After the command is executed, you will be prompted to give a name to the recording. Afterwards, you'll press *space* to start and stop the recording. It is advised to have at least one (or two) seconds of silence before you say the wake-word within the recording. The recording is saved within the same folder (*mycroft-precise-0.2.0*). You should only say the wake-word once per recording. It is advised to record as many recordings as necessary to make the model better. Try to record those people as many times as possible for whom the voice assistant does not correctly understand that it is being called. I personally recorded in places which were not fully quiet (outdoors, library, and in a room) but I was mindful that I don't have a lot of background noise. I did this because in most scenarios that the voice assistant is being used, it'll have some sort of background noise. 

You can use a different tool to record audio as well, but by using precise-collect you will get the audio in the format that is utilized by the voice assistant (WAV files in little-endian, 16 bit, mono, 16000hz PCM format). You can read in more detail [here](https://github.com/MycroftAI/mycroft-precise/wiki/Training-your-own-wake-word#how-to-train-your-own-wake-word).

As suggested in the [mycroft-precise website](https://github.com/MycroftAI/mycroft-precise/wiki/Training-your-own-wake-word#how-to-train-your-own-wake-word), place most of these files under `hey-computer/wake-word/` and the rest under `hey-computer/test/wake-word` within the `mycroft-precise-0.2.0` directory:

```bash
hey-computer/
├── wake-word/
│   ├── hey-computer.00.wav
│   ├── hey-computer.01.wav
│   ├── hey-computer.02.wav
│   ├── hey-computer.03.wav
│   ├── hey-computer.04.wav
│   ├── hey-computer.05.wav
│   ├── hey-computer.06.wav
│   ├── hey-computer.07.wav
│   └── hey-computer.08.wav
├── not-wake-word/
└── test/
    ├── wake-word/
    │   ├── hey-computer.09.wav
    │   ├── hey-computer.10.wav
    │   ├── hey-computer.11.wav
    │   └── hey-computer.12.wav
    └── not-wake-word/
```

This tells Precise to train on the first 8 samples and evaluate the model's accuracy using the last 4.

### 2. precise-train:

The model is trained using the `precise-train` command as shown in this [example](https://github.com/MycroftAI/mycroft-precise/wiki/Training-your-own-wake-word#how-to-train-your-own-wake-word):

```bash
$ precise-train -e 60 hey-computer.net hey-computer/
...
Epoch 1/20
2018-02-23 11:32:05.235740: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
9/9 [==============================] - 0s 31ms/step - loss: 0.2620 - acc: 0.3333 - val_loss: 0.0836 - val_acc: 0.5000
...
Epoch 60/60
9/9 [==============================] - 0s 1ms/step - loss: 0.0025 - acc: 1.0000 - val_loss: 5.6518e-05 - val_acc: 1.0000
```

### 3. precise-listen:

After the creation of this initial model, we can do a demo using live microphone audio input by running the `precise-collect` command. It will listen to the microphone and keep outputting either `.` if it does not hear the wake word or `!` if it does hear it. This is the [sample run](https://github.com/MycroftAI/mycroft-precise/wiki/Training-your-own-wake-word#how-to-train-your-own-wake-word) from MycroftAI.

```bash
$ precise-listen hey-computer.net
Using TensorFlow backend.
2018-02-23 12:46:22.622717: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
ALSA lib pcm_dmix.c:1099:(snd_pcm_dmix_open) unable to open slave
ALSA lib pcm_route.c:867:(find_matching_chmap) Found no matching channel map
ALSA lib pcm_dmix.c:1099:(snd_pcm_dmix_open) unable to open slave
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
```

If you create your wake-word model just using these initially collected recordings of the wake-word, your voice assistant will wake up on everything since it does not recognize any not-wake-words (which would basically be everything else - words it shouldn't wake up on). In order to reduce false activations, you need to to either record words and sentences that resemble in sound to your wake-word, or you can get a random set of sounds and train your model on it. The downside of obtaining a large audio dataset is that your wake-word might be within one of the audio files and might get listed as a not-wake-word (but in my experience it is highly unlikely if you have a wake-word that is not used within normal conversation).

#### a. Recording Not-Wake-Words:

To record your own false activations, launch `precise-listen` in save mode:

```bash
precise-listen hey-computer.net -s hey-computer/not-wake-word
```

While this is activated, you can say words that sound similar to your wake-word (after a second or two interval). If the model activates, Precise will automatically store that recording in the `hey-computer/not-wake-word` folder. Make sure you *NEVER* say the wake-word while this command is running. After you have recorded similar sounding words/sentences 10-20 times for each one, you can retrain your model with the `precise-train` command again:

```bash
precise-train hey-computer.net hey-computer/ -e 600
```

You can stop training with *`Ctrl + C`* once the accuracy (*acc*) gets close to 1.0. Now, you can repeat the demo by running `precise-listen` again. Your model will have substantially improved as it now knows not to wake up on everything.

I would recommend adding some of the recently recorded files into the `hey-computer/test/not-wake-word` folder as then you can see the accuracy of your model with the not-wake-words.

#### b. Obtaining Not-Wake-Words:

At this stage, your model should still be activating on daily sounds/noises. This is where an audio dataset comes in handy. As instructed by the MycroftAI team, a good place to start looking for audio data is the [Public Domain Sounds Backup](http://pdsounds.tuxfamily.org/). You can download it with the following:

```bash
cd data/random
wget http://downloads.tuxfamily.org/pdsounds/pdsounds_march2009.7z
# Install p7zip
7z x pdsounds_march2009.7z
cd ../..
```

Other resources that I found useful can be found in this article [Over 1.5TB's of Labeled Audio Datasets](https://towardsdatascience.com/a-data-lakes-worth-of-audio-datasets-b45b88cd4ad) (the ones I used to train Tux were the [LibriSpeech](https://www.openslr.org/12/) and the [VoxCeleb](http://www.robots.ox.ac.uk/~vgg/data/voxceleb/) datasets). Resources listed by the MycroftAI team are the [precise-data](https://github.com/MycroftAI/precise-data/tree/models) and the [Precise-Community-Data](https://github.com/MycroftAI/precise-community-data)

If you can get some long audio files, they can be converted to the right format using the command line tool `ffmpeg`. MycroftAI provided the following script that you can use:

```bash
SOURCE_DIR=data/random/mp3
DEST_DIR=data/random

for i in $SOURCE_DIR/*.mp3; do echo "Converting $i..."; fn=${i##*/}; ffmpeg -i "$i" -acodec pcm_s16le -ar 16000 -ac 1 -f wav "$DEST_DIR/${fn%.*}.wav"; done
```

This will place all the converted files into `data/random` folder. 

### 4. precise-train-incremental:

Once we have the correct format data placed within `data/random`, we are now able to reduce the false activations using the `precise-train-incremental` command:

```bash
precise-train-incremental hey-computer.net hey-computer/
```

This will make precise go through all the `.wav` audio files placed within `data/random` and move the ones that cause a false activation into the `hey-computer/not-wake-word` directory, and then it retrains the model again. This step can take time depending on the length of the audio files, and also just how many audio files there are.

### 5. precise-test:

For this step, I'd suggest counting the number of files that have been added to the `hey-computer/not-wake-word` directory - lets say it's 1000. From the remaining audio files in the `data/random` randomly select enough files so that it makes almost 20% of the number of counted files within the `hey-computer/not-wake-word` directory - so in this case it'll be 200 audio files from `data/random`.

Having done this we can move on to testing our model. This is done using the `precise-test` command:

```bash
precise-test hey-computer.net hey-computer/
```

The file `hey-computer.net` is the [Keras] model that we created using the `precise-train` command and all `precise-test` is doing is running the model on the test data that we added in our `hey-computer/test` directory. It provides a statistical analysis of the testing of the model - gives its accuracy of prediction on the test set.

If you want to again check the model using live microphone audio output, you should use the `precise-listen` command again.

### 6. precise-convert:

So far we have used HDF5 model file trained with Keras `(.net)`, but the last step is to convert this file to be used by TensorFlow `(.pb)`. This will be done using the following command:

```bash
precise-convert hey-computer.net
```

This should create two files:

 - `hey-computer.pb` - TensorFlow neural network
 - `hey-computer.pb.params` - details specific to Precise for how the audio was processed for the network
 
 ## Finalizing:
 
 To finalize things, you should follow the instructions [on this page](https://github.com/shahzeb-jadoon/Voice-Assistant-Project) except for Step 2. For you, Step 2 will look something like this:
 
 Copy your `.pb` files (including the `.pb.params`) file into the `.mycroft/precise/` folder on your machine. Next, follow the following steps to implement your own name for the voice assistant:

```bash
cd ~/
cd mycroft-core
./bin/mycroft-config edit user
```

In the window that appears, copy the following code. Where it says `<insert wake-word>`, write your own wake-word within the double quotation marks, and within <filename> write the name you have given your TensorFlow model. Within `<user folder name>` you should write down your user account's folder name (it shoud be obvious that the names shoud be written without the `<>`):

```javascript
{
  "max_allowed_core_version": 20.2,
  "listener": {
    "wake_word": "<insert wake-word>"
  },
  "hotwords": {
    "<insert wake-word>": {
        "module": "precise",
        "local_model_file": "/home/<user folder name>/.mycroft/precise/<filename>.pb"
    }
  }
}
```

Press *`Ctrl + S`* to save and *`Ctrl + X`* to exit the window. Next type the following command:

```bash
./bin/mycroft-config reload
```

After this you can continue on to Step 3 as mentioned [here](https://github.com/shahzeb-jadoon/Voice-Assistant-Project).
