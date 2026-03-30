# audio_dataset_remaining

# 🎯 Multimodal Mood Prediction from Lecture Content

## 📂 Dataset

The dataset consists of lecture audio files and corresponding transcripts.
Due to large file size, the dataset is hosted on Google Drive:

👉 **Download Dataset:**
https://drive.google.com/drive/folders/1ggKc5yT8AAUMtzXj4fF6Pn4rcpLs_ahN?usp=drive_link


## 📊 Dataset Details

* Total samples: ~120+
* Audio format: WAV (trimmed to 20 mins)
* Text format: Transcripts (.txt)

## 🛠️ Pipeline

1. Video → Audio conversion
2. Audio trimming (20 mins)
3. Speech-to-text transcription (Whisper)
4. Feature extraction
5. Multimodal model (Audio + Text)

## 🚀 Models Used
* BERT (text)
* LSTM / XGBoost (audio)
* Fusion model

## 📌 Note
Due to GitHub size limitations, audio files are stored externally.



## 🔊 Transcription Code (Whisper)
The following Python script was used to convert audio files into text transcripts using OpenAI Whisper.
CODE:

import os
import whisper

model = whisper.load_model("base")

folder = "."

for file in os.listdir(folder):
    if file.endswith(".wav"):
        
        txt_filename = file.replace(".wav", ".txt")
        
        # ✅ SKIP if already processed
        if os.path.exists(txt_filename):
            print(f"Skipping (already done): {file}")
            continue
        
        print(f"Processing: {file}")
        
        result = model.transcribe(file)
        
        with open(txt_filename, "w", encoding="utf-8") as f:
            f.write(result["text"])
        
        print(f"Saved: {txt_filename}")
print("All files transcribed successfully!")

### ⚙️ Installation

pip install openai-whisper

### 🚀 Run the script

python transcribe.py

### 📌 Features

* Automatically processes all `.wav` files
* Skips already transcribed files (resume capability)
* Saves output as `.txt` files
