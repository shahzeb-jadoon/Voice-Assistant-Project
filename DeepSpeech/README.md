# DeepSpeech

## Introduction:

[DeepSpeech](https://mycroft.ai/blog/deepspeech-update/) is an open source Speech-To-Text engine, using a model trained by machine learning techniques based on [Baidu's Deep Speech research paper](https://arxiv.org/pdf/1412.5567.pdf) and implemented with Google’s TensorFlow framework. [DeepSpeech's GitHub Repository](https://github.com/mozilla/DeepSpeech) and [DeepSpeech's Documentation](https://deepspeech.readthedocs.io/en/v0.6.1/?badge=latest) can help you further understand the details of its workings. Mozilla has also provided some information about their [Speech & Machine Learning](https://research.mozilla.org/machine-learning/) work. I also found this [YouTube video](https://www.youtube.com/watch?v=P9GLDezYVX4) helpful to understand what DeepSpeech is.

## How To Get DeepSpeech:

### Running DeepSpeech Using GPU:

Before we can attain DeepSpeech, we need to make sure we have certain requirements met so that DeepSpeech runs better. The first thing that is recommended is to have a Graphics Processing Units (GPU) especially if you want to train your own text-to-speech model using DeepSpeech. 

#### Checking for CUDA Compatibility:

This [NVIDIA website](https://developer.nvidia.com/cuda-gpus) can tell you if your GPU is compatible. It is recommended that your GPU has a compute compatibility rating of 3.0 or higher. The higher the rating, the better/quicker you can train your model. The rating is of [CUDA-enabled GPU's](https://developer.nvidia.com/cuda-toolkit). [CUDA (Compute Unified Device Architecture)](http://www.techdarting.com/2013/06/cuda.html) is a [parallel computing](http://www.techdarting.com/2013/07/what-is-parallel-programming-why-do-you.html) platform and first programming model that enabled high level programming for GPUs and thereby made them available for general purpose computing. 

#### Obtaining Latest GPU Driver:

Once you ahve checked whether your GPU is compatible, we need to make sure that you have the latest driver for your GPU. NVIDIA provides a [website](https://www.nvidia.com/Download/index.aspx?lang=en-us) to download system specific driver. I did a manual search by typing my Product Type, Product Series (make sure to scroll down in case you don't see the one you have), the Product, Operating System, Download Type (`Linux Long Lived` if you have the LTS version of Ubuntu), and Language. Click on Download when the driver is provided. I found this website [2 Ways to Install NVIDIA Driver on Ubuntu 18.04](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04) and this [post on Reddit](https://www.reddit.com/r/linux_gaming/comments/9129fq/installing_older_nvidia_drivers_from/) very helpful while installing this driver. You can use better resources if you find them (and please share them with me too so I can update my links here as well).

#### Downloading CUDA Toolkit:

The next step is to now download and install the [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit). Once you click on `Download Now` button, the website will take you the page where you will get the CUDA toolkit developed specifically for your computer. They will ask about your Operating System (Linux in my case), the Architecture of your system (x86_64 in most cases), the Distribution of Linux you are using (Ubuntu, if you followed what I did), the Version of Ubuntu you're using (18.04 or 16.04), and lastly the Installer Type you want to use (I personally found `runfile (local)` the easiest to implement). There they'll give you isntructions to download the file and install it using the terminal. I found this website [How To Install CUDA 10.1 on Ubuntu 19.04](https://www.pugetsystems.com/labs/hpc/How-To-Install-CUDA-10-1-on-Ubuntu-19-04-1405/) and this [Reddit post](https://www.reddit.com/r/CUDA/comments/elhnz4/worried_about_installing_cuda_on_thinkpad_with/) very helpful while installing this toolkit. You can use better resources if you find them (and please share them with me too so I can update my links here as well).

#### Creating & Activating Virtual Environment:

In order to run DeepSpeech, we need to create a Virtual Environment so that we can have earlier version of TensorFlow running within the virtaul environment while keeping the latest one that is used by the rest of the system. One thing that we need to confirm before moving forward is that we use [Python 3.5 or later version](https://deepspeech.readthedocs.io/en/v0.6.1/USING.html) to create the virtual environment. The virtual environment can be created using the following termianl command:

```bash
virtualenv -p python3 $HOME/tmp/deepspeech-venv/
```

We can then activate our virtual environment using the following command:

```bash
source $HOME/tmp/deepspeech-venv/bin/activate
```

#### Installing DeepSpeech-GPU:

Finally, we have all the requirements met to install DeepSpeech-GPU, which we will install with the following terminal command within the activated virtual environment.

```bash
pip3 install deepspeech-gpu
```

Just to make sure we have the latest version of DeepSpeech, run the following command:

```bash
pip3 install --upgrade deepspeech-gpu
```

### Running DeepSpeech Without GPU:

If you are fine with DeepSpeech taking a lot of time to create models and analyzing audio, or if your GPU is not CUDA-enabled, then you just need to create and activate the virtual environment as mentioned above. You still need to make sure you use Python 3.5 or higher to create the virtual environment. Then isntead of installing DeepSpeech-GPU, you will run these following commands to install DeepSpeech and update it to retrieve the latest version:

```bash
pip3 install deepspeech
pip3 install --upgrade deepspeech
```

## Running A Pre-Trained Model:

The DeepSpeech team provides a pre-trained Speech-to-Text model that we can retrieve using the following command:

```bash
wget https://github.com/mozilla/DeepSpeech/releases/download/v0.6.1/deepspeech-0.6.1-models.tar.gz
tar xvfz deepspeech-0.6.1-models.tar.gz
```

This will download and unzip the model files that are provided by DeepSpeech. Now if you have an audio file, you can get it transcribed using the [following command](https://deepspeech.readthedocs.io/en/v0.6.1/USING.html#getting-the-pre-trained-model):

```bash
deepspeech --model models/output_graph.pbmm --lm models/lm.binary --trie models/trie --audio my_audio_file.wav
```

The arguments `--lm` and `--trie` are optional, and represent a language model.

## Training Your Own Model:

If you have the time, have a CUDA-enabled GPU, and are feeling ambitious, you can try training your own model. This is where the virtual environment is useful as we will need to uninstall TensorFlow and get TensorFlow-GPU instead. DeepSpeech team have given [extensive instructions](https://deepspeech.readthedocs.io/en/v0.6.1/TRAINING.html) on how to train your own model. Since I used the mode provided by them, I did not create my own model, so I would just recommend following their instructions to train your own model. They also provide [Training Regimen and Hyperparameters for fine-tuning](https://github.com/mozilla/DeepSpeech/releases) your model. 
