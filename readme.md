# Open WebUI with ghostwheel

## Overview

This repository provides a fork of [Open WebUI](https://github.com/open-webui/open-webui) with some hacky changes to the Ollama backend, to allow for use with the ghostwheel inference server. Most of the base functionality of WebUI should work out of the box, but certain admin operations (i.e. pulling, pushing, editing, deleting models from the Ollama server) are disabled when using ghostwheel. You'll receive an error message in the panel, and a `405` from the WebUI backend, when attempting to use these features.

Other functionality works as expected—you can chat with the existing models, create new ones from the base models with specific knowledge or prompts, embed documents and use them for RAG question/answer, etc.

## Usage

You can set up and run WebUI from this fork, serving WebUI locally with ghostwheel as its Ollama backend. The instructions are very similar to (and derived from) [WebUI's own guide for local deployment](https://docs.openwebui.com/getting-started/#build-and-install-%EF%B8%8F). Note that we've made some changes to [the default environment configuration](https://github.com/enwask/ghostwheel-webui/blob/main/.env.example) to disable user login (since you'll likely only be running locally), as well as to enable ghostwheel and provide it your API key.

Run the following commands to install WebUI with ghostwheel locally (you will of course need an appropriate Python environment, as well as an `npm` installation):

```bash
# Clone the repository locally and enter it
git clone https://github.com/enwask/ghostwheel-webui.git
cd ghostwheel-webui

# Copy the .env file
# You must set your ghostwheel API key in the .env file, once created
cp -a .env.example .env

# Build the frontend with Node
npm install
npm run build

# Install requirements for the WebUI backend
cd backend
pip install -Ur requirements.txt

# Finally, run the start script
# This script serves both the backend & frontend for us
bash start.sh
```

Setup for running in Docker, or in another production environment, is left as an exercise for the reader.
