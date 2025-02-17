## Aim
This guide explains how to install large language models on the high-performance computing (HPC) cluster available to Kew researchers.

## Pre-requisites
- An account on the [crop diversity HPC cluster](https://cropdiversity.ac.uk/), with [key authentication](https://help.cropdiversity.ac.uk/ssh.html) set up.
    - Request an account [here](https://help.cropdiversity.ac.uk/user-accounts.html) if you don't have one already.
- Basic familiarity with Linux command-line operations, such as:
    - Navigating directories (`cd`, `ls`)
    - Cloning Git repositories (`git clone`)
    - Modifying file permissions (`chmod`)
    - Running background processes (`nohup`, `&`)
    
    If needed, take the DataCamp course [Introduction to the Shell](https://www.datacamp.com/courses/introduction-to-shell) – Kew provides [free access to DataCamp courses](https://kewnet.kew.org/team_news/free-datacamp-licenses/).

## Setup
You will need to execute commands in three different environments:
1. Your **local machine** (assumed to be Windows)
2. The **head node** of the HPC cluster (`gruffalo.cropdiversity.ac.uk`)
3. A **compute node** on the HPC cluster (assigned upon request)

Ensure you have separate terminal sessions open for each environment as needed.

## Installation Steps
The instructions below specify where each command should be executed.

### 1. *(Local Machine)* Connect to the HPC Head Node
Open **Command Prompt** (or your preferred terminal) and connect to the head node:
```bash
ssh [YOUR_USER_NAME]@gruffalo.cropdiversity.ac.uk
```
Replace `[YOUR_USER_NAME]` with your actual username.

### 2. *(Head Node)* Request a Compute Node with a GPU
Run the following command to request an interactive shell on a GPU node:
```bash
srsh --partition gpu --gpus=1
```
You will be assigned a compute node (e.g., `gpu-node-01`). Take note of this name, as you will need it later.

### 3. *(Compute Node)* Install Ollama and Verify Model Serving

#### Install Ollama (without `sudo`)
Because the standard Ollama installation requires `sudo` privileges, use the script below to install it in a user directory:
```bash
#! /bin/sh

# Create a working directory
mkdir -p ollama-install && cd ollama-install

# Download the latest Ollama binary
curl -L https://ollama.com/download/ollama-linux-amd64.tgz -o ollama-linux-amd64.tgz

# Extract the binary into a local directory
mkdir -p ollama && tar -C ollama -xvf ollama-linux-amd64.tgz

# Navigate back to home directory
cd

mkdir -p bin

# Create a symbolic link for easier execution
ln -s ~/ollama-install/ollama/bin/ollama ~/bin/ollama
```

After installation, verify that Ollama is correctly installed by checking its version:
```bash
./ollama --version
```

#### Test Ollama with a Minimal Model
Run a small model (`tinyllama`) to confirm the installation:
```bash
ollama serve &
ollama run tinyllama
```
You should see debug messages indicating that the model is being retrieved and executed. The prompt will wait for user input, confirming that Ollama is running correctly. Now kill the process as we will now prepare ollama for network access:
```bash
pkill ollama
```

### 4. *(Compute Node)* Prepare Ollama for Network Access and Serve a Model

#### Set Environment Variables
Ollama must be accessible over a network. Set the `OLLAMA_HOST` environment variable:
```bash
export OLLAMA_HOST=0.0.0.0:18199
```
**Note:** The port **must** be above 1024. This setting will reset on logout unless added to `~/.bashrc`.

#### Run Ollama as a Background Process
Start the Ollama server:
```bash
ollama serve &
```
To check if the server is running:
```bash
ps aux | grep ollama
```
To stop the process later:
```bash
pkill ollama
```

#### Download and Serve a Substantial Model
Choose a model from the [Ollama library](https://ollama.com/library) and install it:
```bash
ollama run llama3
```

### 5. *(Local Machine)* Set Up Port Forwarding
To access the model from your local machine, set up SSH port forwarding:
```bash
ssh -L18199:GPU_NODE_NAME.hpc.hutton.ac.uk:18199 YOUR_HPC_USER_NAME@gruffalo.cropdiversity.ac.uk
```
Replace `GPU_NODE_NAME` with your assigned compute node (e.g., `gpu-node-01`) and `YOUR_HPC_USER_NAME` with your username.

Keep this SSH session open while using Ollama.

### 6. *(Local Machine)* Access the Ollama Test Page
In a web browser, open:
```
http://127.0.0.1:18199
```
If the page loads, your setup is complete.

## Using the LLM
You can now develop scripts in windows which communicate with the Ollama server on the HPC using the [Python Ollama library](https://pypi.org/project/ollama/).

### Install the Python Library
```bash
pip install ollama
```

### Example Python Script

```python
import ollama

# Connect to the Ollama server accessed via localhost:18199 (SSH tunnelled to the HPC)
ollama_client = ollama.Client(host='http://127.0.0.1:18199')

# Send a prompt to the model
response = ollama_client.chat("llama3", "Hello, how are you?")

print(response)
```

This script should return a text response from the model, verifying that the setup is complete.

---

### **Final Notes**
- Ensure your SSH tunnel remains open while accessing Ollama remotely.
- To persist environment variables (`OLLAMA_HOST`), add them to `~/.bashrc` or `~/.bash_profile`.
- For troubleshooting, check Ollama logs (`ollama --debug`).

This guide should now provide a clear, step-by-step setup process for running large language models on the Kew HPC cluster. 🚀

