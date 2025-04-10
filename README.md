# Demos for the neuro-san library
This repository contains a collection of demos for the neuro-san library.
They should help developers get started with the library and understand how to create their own agent networks.

---

## Installation

Clone the repo:
```bash
git clone https://github.com/leaf-ai/neuro-san-demos
```

Go to dir:
```bash
cd neuro-san-demos
```
Ensure you have a supported version of python (3.12 at this time)
```bash
python --version
```

Create a dedicated Python virtual environment:
```bash
python -m venv venv
```
Source it:
```bash
source venv/bin/activate && export PYTHONPATH=`pwd`
```

Install the requirements:
```bash
pip install -r requirements.txt
```

**IMPORTANT**: By default the server relies on OpenAI's `gpt-4o` model. 
Set the OpenAI API key, and add it to your shell configuration so it's available in future sessions:  
**NOTE**: Replace `XXX` with your actual OpenAI API key.  
**NOTE**: This is OS dependent. This command is for macOS and Linux.
```bash
export OPENAI_API_KEY="XXX" && echo 'export OPENAI_API_KEY="XXX"' >> ~/.zshrc
```
Other models are supported too but will require proper setup.

---

## Run

There are multiple ways in which we can now use the neuro-san server with a client

### Option 1: Command Line Interface

- Export the following environment variables:
```bash
# Point the server to the manifest file containing the agent network configurations
export AGENT_MANIFEST_FILE="./registries/manifest.hocon"
# Point the server to the directory containing the agent Python tools
export AGENT_TOOL_PATH="./coded_tools"
```

- Start the server:
```bash
python -m neuro_san.service.agent_main_loop --port 30011
```

- Start the client:
From another terminal window, navigate to the repo's folder and activate the virtual environment:
```bash
source venv/bin/activate && export PYTHONPATH=`pwd`
```

Then start the client:
```bash
python -m neuro_san.client.agent_cli --connection service --agent hello_world
```

- Query the client
When prompted, ask a question to the `hello_world` agent network. For example:
```
I am travelling to a new planet and wish to send greetings to the orb.
```
And it should return something like:

    Hello, world.

... but you are dealing with LLMs. Your results will vary!

Type `quit` to exit the client.

---

### Option 2: Using a basic Web Client interface

- Start the server and the client in one single command:
```bash
python -m run
```

The client and server logs will show on the screen,
and will also be saved to `logs/server.log` and `logs/client.log` respectively.
As a default, on a web browser you can now navigate to http://127.0.0.1:5003/ to start using the application.

- To see the various config options for this app, on terminal
```bash
python -m run -h
```
or
```bash
python -m run --help
```

- (Optional) How to run in demo-mode

This is really meant to experience some of the default multi-agent networks that are available in the neuro-san library.
To use it, start the server and the client in one single command:
```bash
python -m run --demo-mode
```

---

### Option 3: Using `nsflow` as a developer-oriented web client
If you want to use neuro-san with a FastAPI-based developer-oriented client, follow these steps:

- Install nsflow. Make sure to replace `x.x.x` with the actual version you want to install.
```bash
pip install wheels_private/nsflow-x.x.x-py3-none-any.whl
```

- Start the Backend & Frontend, from project root
```bash
python -m nsflow.run
```

By default:
- Frontend will be available at: `http://127.0.0.1:4173`
- OpenAPI specs will be available at: `http://127.0.0.1:4173/docs`

To see the various config options for this app, on terminal
```bash
python -m nsflow.run -h
```
or
```bash
python -m nsflow.run --help
```

---

## User guide

Ready to dive in? Check out the [user guide](docs/user_guide.md) for a detailed overview of the neuro-san library
and its features.

---

## Tutorial
For a detailed tutorial, refer to [docs/tutorial.md](docs/tutorial.md)

---

## Examples

For examples of agent networks, check out [docs/examples.md](docs/examples.md).
