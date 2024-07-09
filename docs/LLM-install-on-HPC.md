## Aim
This guide explains how to install large language models on the high performance compute cluster available to Kew researchers.

## Pre-requisites
- Account on the [crop diversity HPC cluster](https://cropdiversity.ac.uk/), with [key authentication](https://help.cropdiversity.ac.uk/ssh.html) set up.
    - Request an account [here](https://help.cropdiversity.ac.uk/user-accounts.html) if you don't have one already.
- Familiarity with Linux command line to navigate between directories, clone git repositories etc
    - Use the datacamp course [Introduction to the shell](https://www.datacamp.com/courses/introduction-to-shell) if necessary - Kew has [free access to datacamp courses](https://kewnet.kew.org/team_news/free-datacamp-licenses/)

## Setup

You will need to be able to execute commands in three different places, ie:
1. Your *local machine* (assume Windows)
2. The *head node* of the HPC cluster (gruffalo.cropdiversity.ac.uk)
3. A *compute node* on the HPC cluster (assigned on request)

## Installation steps

The instructions below note which machine you should run each on:

1. *(Local machine)* Open a command windows and log into the HPC head node `gruffalo.cropdiversity.ac.uk`
1. *(head node)* Request an interactive shell on a node with a GPU: `srsh --partition gpu --gpus=1` Note the name of the compute node that you are assigned - you will need it later
1. *(compute node)* Install Ollama. The standard ollama setup instructions use `sudo` - as you are unable to elevate permissions on the HPC you instead need to download a release directly. Check the ollama github repository page for the latest release details, these use version 0.1.47
    1. Download the ollama release: `wget https://github.com/ollama/ollama/releases/download/v0.1.47/ollama-linux-amd64`
    2. Make it executable: `chmod 755 ollama-linux-amd64`
    3. Create a softlink: `ln -s ollama-linux-amd64 ollama` 
    4. Install a minimal model (for speed of download): `./ollama run tinyllama`
    5. Set the environment OLLAMA_HOST environment variable: `export OLLAMA_HOST=0.0.0.0:11435`
    6. Run the ollama server as a background process: `./ollama serve &`
1. *(local machine)* Set up port forwarding. In a command line shell in your local environment, execute:   
    `ssh -L11434:GPU_MACHINE_NAME.cropdiversity.ac.uk:11435 YOUR_HPC_USER_NAME@gruffalo.cropdiversity.ac.uk`

   Substitute GPU_MACHINE_NAME and YOUR_HPC_USER_NAME appropriately.
1. *(local machine)* Open the Ollama test page in your local browser at https://127.0.0.1:11434

## Using the LLM

You can communicate with the ollama server using a [python ollama library](https://pypi.org/project/ollama/). Install it on your *local machine* using `pip install ollama` and then create a test script as per the examples in the documentation.
