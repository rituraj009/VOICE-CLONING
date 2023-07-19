# VOICE-CLONING
## AI ML Assignment 2- VOICE CLONING

## Task
Create a voice cloning model that can generate a synthetic voice that sounds like a specific person. The model should be able to generate speech from text input and reproduce the unique vocal characteristics of the target speaker.

## Solution 
1. To accomplish this task, I have leveraged the BARK model, which is a text-to-audio model.
2. BARK can generate text-to-audio conversions while customizing the voice to sound like a specific person.
3. Although BARK doesn't support custom voice cloning, we can use its speaker presets to approximate the target speaker's voice.
4. BARK also has the capability to produce nonverbal communication like laughing, sighing, and crying.
5. BARK supports 100+ speaker presets across supported languages.


## Hardware Requirements
1. BARK is compatible with both CPU and GPU.
2. The full version of BARK requires 12 GB VRAM.
3. However, for users with GPUs having limited VRAM (e.g., less than 4GB), a smaller version of the BARK model is available.
4. The smaller version of the model can fit into GPUs with less than 4GB VRAM or can be run on CPU standalone.

Note: Running the full version of BARK on GPUs with limited VRAM is possible but might result in slower processing times as the GPU needs to handle memory constraints by swapping data between VRAM and system RAM.

## Code Implementation

Step 1: Install the BARK model:
```
pip install git+https://github.com/suno-ai/bark.git
```
