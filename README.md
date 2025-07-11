# T5 Custom Implementation

## About 
For reference purposes, this shows how to train a T5 model for sentence completion and question answering tasks
using a custom dataset. The dataset does not need to be made up of actual sentences. In this case, they are just items.

## Requirements
### For Local Environment 
Install using pip
- Transformers
- Datasets
- Acceleration
- Pytorch
- Jupyterlab

### For Docker Container Environment

Install using the dockerfile
    
    FROM pytorch/pytorch:2.7.1-cuda12.6-cudnn9-runtime

    # Set environment variables
    ENV DEBIAN_FRONTEND=noninteractive

    # Install system dependencies
    RUN apt-get update && \
        apt-get install -y \
            git \
            python3-pip \
            python3-dev \
            unzip

    # Upgrade pip
    RUN python3 -m pip install --upgrade pip

    # Install PyTorch and torchvision
    RUN pip3 install transformers datasets jupyterlab sentencepiece accelerate

    # Set the working directory
    WORKDIR /app/codes-box

## Installation
Clone the repository to the local environment or in the codes-box when using docker container

## Implementation
There are 3 kinds of T5 implementation done in this repo.

**1. Question Answering Task**

Basically, it takes an input and tries to answer back according to the sentence pairs found in the dataset. 
In this case, an item with various attributes is the input and the output is the corresponding element that can
be attached to it.

Run the ```t5_question_answering.ipynb``` to try it.

**2. Sentence Completion Task**

This task takes in incomplete input and completes the missing items. In this case, an incomplete item (e.g., missing series) will be filled with the possible values seen in the training.

Run the ```t5_sentence_completion.ipynb``` to try it.

**3. Question Answerinh and Sentence Completion Task**

This is simply the combination of the two tasks. First the model completes an incomplete item input. Then, the model will 
suggest a corresponding element to the item it has completed. The model knows which task to perform by putting a prefix 
before the input.  ```complete_item: ``` is used for completing the input and ```generate_element: ``` for suggesting the
corresponding element.

Run the ```t5_combination_qa_sc.ipynb``` to try it.