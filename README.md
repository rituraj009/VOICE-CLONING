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

Step 1: Install the BARK model
```
pip install git+https://github.com/suno-ai/bark.git
```

Step 2: GPU Configuration (Optional)
```
import os
os.environ["SUNO_OFFLOAD_CPU"] = "False"
os.environ["SUNO_USE_SMALL_MODELS"] = "True"
```
These environment variables can be set to utilize GPU power (SUNO_OFFLOAD_CPU = "False") or to utilize CPU power (SUNO_OFFLOAD_CPU = "True"). Adjust the settings based on your hardware capabilities.

Step 3: Import Required Modules
```
from bark import SAMPLE_RATE, generate_audio, preload_models
from IPython.display import Audio
import nltk
import numpy as np
```

* SAMPLE_RATE represents the audio sampling rate used by BARK.
* generate_audio is a function that converts text prompts into audio.
* preload_models is a function to download and load necessary BARK models.
* Audio is used to display audio data as an interactive audio player in the notebook.
* nltk is used for sentence tokenization.
* numpy is imported as np for array operations

Step 4: Define the Script and Split Sentences
```
script = """
Hey Raj,
John here from the Recruitment Team at OpeninApp. 
Thank you so much for expressing interest and applying for the role of AI Engineer Intern.
As part of the next steps in our screening process, please complete the technical assessment attached in the PDF below and share a screen recording explaining your code.
You can choose 1 of the 2 assignments below. Deadlines are mentioned within each file. We look forward to hearing from you once the assessment is completed.
""".replace("\n", " ").strip()

sentences = nltk.sent_tokenize(script)
```
* The script variable contains the text that will be converted to speech.
* nltk.sent_tokenize is used to split the script into individual sentences.

Step 5: Generate Audio Pieces with Pauses
```
SPEAKER = "v2/en_speaker_6"
silence = np.zeros(int(0.25 * SAMPLE_RATE))

pieces = []
for sentence in sentences:
    audio_array = generate_audio(sentence, history_prompt=SPEAKER)
    pieces += [audio_array, silence.copy()]

Audio(np.concatenate(pieces), rate=SAMPLE_RATE)
```

* SPEAKER represents the selected preset of the voice.
* silence is an array of zeros representing a quarter second of silence.
* The loop iterates over each sentence, generating audio for each sentence and appending it to the pieces list along with a copy of the silence array.
* Finally, the Audio function is used to concatenate and play the audio pieces.

This implementation demonstrates how to use the BARK model to convert text into synthesized speech, approximate the voice of a specific person, and introduce pauses between sentences for natural speech flow.

NOTE: The speaker preset (SPEAKER) can be adjusted according to the desired voice characteristics.
Visit the link to see the various speaker presets available with bark model 
https://suno-ai.notion.site/8b8e8749ed514b0cbf3f699013548683?v=bc67cff786b04b50b3ceb756fd05f68c

