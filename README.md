---
title: Webapp Factory WizardCoder CTransformers
emoji: 🏭🧙🤖
colorFrom: brown
colorTo: red
sdk: docker
pinned: false
app_port: 7860
---

A minimalist Docker project to generate apps on demand.

Ready to be used in a Hugging Face Space.


# Examples

## Local prompt examples

```
http://localhost:7860/?prompt=a%20pong%20game%20clone%20in%20HTML,%20made%20using%20the%20canvas
```
```
http://localhost:7860/?prompt=a simple html canvas game where we need to feed tadpoles controlled by an AI. The tadpoles move randomly, but when the user click inside the canvas to add some kind of food, the tadpoles will compete to eat it. Tadpole who didn't eat will die, and those who ate will reproduce.
```

## Installation

### Prerequisites

**A powerful machine is required! You need at least 24 Gb of memory!**

- Install NVM: https://github.com/nvm-sh/nvm
- Install Docker https://www.docker.com

### Python

This project relies on Python dependencies called through Pythonia.

To install those dependencies, first you should create and activate a new virtual environment for Python:

```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
```

Then install the dependencies in it:
```bash
pip install -r requirements.txt
```

### Installing the model

The LLM will be downloaded through the Python functions,
however we cannot run them using Pythonia or else it will timeout.

Fortunately the solution is simple, we can just download the model in advance:

```
python download-model.py
```

This is done automatically when using Docker.

### CTransformers

This project relies on CTransformers called through Pythonia.

To install ctransformers:

```bash
pip install ctransformers
# or this, depending on your Python environment:
# pip3 install ctransformers
```

For GPU (CUDA) support set environment variable CT_CUBLAS=1 and install from source using:

```bash
CT_CUBLAS=1 pip install ctransformers --no-binary ctransformers
# or this, depending on your Python environment:
# CT_CUBLAS=1 pip3 install ctransformers --no-binary ctransformers
```

### Building and run without Docker

```bash
nvm use
npm i
npm run start
```

### Building and running with Docker

```bash
npm run docker
```

This script is a shortcut executing the following commands:

```bash
docker build -t webapp-factory-wizardcoder-ctransformers .
docker run -it -p 7860:7860 webapp-factory-wizardcoder-ctransformers
```

Attention! If you have a Mac, you may have trouble running the project on your machine.

You will see the following error message because Docker won't be able to use the pre-generated binaries for `libctransformers.so` due to architecture incompatibility:

```
🌉 OSError: /home/user/.local/lib/python3.11/site-packages/ctransformers/lib/avx2/libctransformers.so: cannot open shared object file: No such file or directory]
```

However if you run your project on a Hugging Face space, you should be just fine :)

### Deployment to Hugging Face

The standard free CPU instance (16 Gb) will not be enough for this project, you should use the upgraded CPU instance (32 Gb)

