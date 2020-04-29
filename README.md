# Voice Assistant - Tux

## Background

I am an Undergraduate student of senior standing at [Wartburg College](https://www.wartburg.edu/) pursuing a degree in Computer Science and Actuarial Science. For my senior project, I wanted to research and puruse machine learning, and get to learn what various techniques are implemented to make a voice assistant work. After being introduced by Dr. John Zelle, and along with some research, I found [MycroftAI](https://mycroft.ai/)'s team that provided the [tools](https://github.com/MycroftAI) that I could use to create my own voice assistant. 

This is completely a research-based project since I had litlle knowledge of machine learning, and no knowledge of the tools provided by MycroftAI. Thus, as I learn along, this page will provide further information regarding the things I have achieved thus far. Everything provided by MycroftAI is open-sourced, and they encourage people to use their code. 

I will utilize version control for this project because I might need to make some adjustments to the code provided by the MycroftAI's team in their repository(repo), and it will also serve as a way for me to document my work. Thus I am planning on using Git and also GitHub since I want to show the progress I've made.

### 1. Git

The first thing I did was install git on my machine. 

```markdown
sudo apt update
sudo apt install git
```

Then I cloned the MycroftAI's [mycroft-precise repository](https://github.com/MycroftAI/mycroft-precise) and initiated my local git repo within that folder.

```markdown
git clone https://github.com/MycroftAI/mycroft-precise
git init
git add .
git commit -m "<comment>"
```

I have created a [Git cheat-sheet](https://docs.google.com/document/d/1N3ToWxiGmmR6QWdNF1TplYEpfsYLyMqc2AeIdb_Q4dg/edit?usp=sharing) so that I have quick access to all the commands that I will need. This has been made possible due to the people that have been linked to within the cheat-sheet. Although it has helped me quite a lot, I would recommend that you understand what the commands do before you start typing them up just to be on the safe side.

### 2. GitHub

The second step to my project was to create a GitHub account. This is because I want to show the progress to anyone who would like to see. As I begin to learn more and more about this platform, I am adding my information on a [Google doc](https://docs.google.com/document/d/1N3ToWxiGmmR6QWdNF1TplYEpfsYLyMqc2AeIdb_Q4dg/edit?usp=sharing) that helps me easily revisit all of the things I've learned about GitHub.

After creating my project folder on GitHub, I pushed my local repo onto the online one, but before doing that I created a readme markdown file for my project with the following commands.

```markdown
echo "# CS-460-Project" >> README.md
git add .
git commit -m "<comment>"

git remote add origin <URL>
git push -u origin master
```

This created my markdown readme file and also linked my local repo to [my online GitHub acccount](https://github.com/shahzeb-jadoon/CS-460-Project).

### 3. mycroft-precise

mycroft-precise is a tool based on TensorFlow that is provided by MycroftAI. Its basic functionality include tools that I can use to record wake-words and not-wake-words for my voice assistant. I can then use these recordings to train and create a model for my voice assistant that would make it recognize sound patterns when it is being called and wake up accordingly. This tool also lets me see the accuracy of my model, and at the end converts the model into a TensorFlow file. I created another [document](https://docs.google.com/document/d/17hs_4hXubngRJfpbfTIIGhwK1Zd5zbFIQTUSP3wU8Us/edit?usp=sharing) to list all the code and functionality of mycorft-precise.


### 4. DeepSpeech

Also built on TensorFlow, DeepSpeech is a speech-to-text engine built by Mozilla. Mycroft and Mozilla are working in collaboration to make this engine better every day. I have a [document](https://docs.google.com/document/d/1fbVyQC9dOY7ez9vVJb386isMwrKn9MkPNhKklMvT9gs/edit?usp=sharing) that lists the resources one might find useful to learn and use DeepSpeech. 


## Support or Contact

If you have any questions, comments, or concerns, you can email me at shahzeb.jadoon.sj@gmail.com

