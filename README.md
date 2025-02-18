# YouTube Video Question Answering

A simple Python-based workflow that enables question answering for YouTube videos using open-source AI models. The system transcribes video content using OpenAI's Whisper and performs question answering using RoBERTa from Hugging Face.

## Features

- YouTube video audio extraction
- Speech-to-text transcription using Whisper
- Question answering capabilities using RoBERTa
- Support for custom question prompts
- Audio playback in Jupyter/Colab environments

## Prerequisites

- Python 3.7+
- FFmpeg (for audio processing)
- Internet connection for model downloads

## Installation

1. Install the required packages:
```bash
pip install yt-dlp whisper-openai transformers torch
```

2. Ensure FFmpeg is installed on your system:
- For Ubuntu/Debian: `sudo apt-get install ffmpeg`
- For macOS: `brew install ffmpeg`
- For Windows: Download from [FFmpeg website](https://ffmpeg.org/download.html)

## Usage

1. Import required libraries:
```python
import yt_dlp
import whisper
from transformers import pipeline
import IPython.display as ipd
```

2. Download and process YouTube video:
```python
video_url = "YOUR_YOUTUBE_URL"
audio_file = download_audio(video_url)
```

3. Transcribe the audio:
```python
model = whisper.load_model("base")
result = model.transcribe(audio_file)
transcript = result['text']
```

4. Set up question answering:
```python
qa_pipeline = pipeline('question-answering', model='deepset/roberta-base-squad2')
question = "Your question here"
result = qa_pipeline(question=question, context=transcript)
```

## Example

```python
# Process Steve Jobs' Stanford speech
video_url = "https://www.youtube.com/watch?v=UF8uR6Z6KLc"
audio_file = download_audio(video_url)

# Ask a question about the speech
question = "What are the 5 key messages that Steve Jobs wanted to convey?"
result = qa_pipeline(question=question, context=transcript)
print("Answer:", result['answer'])
```

## Limitations

- Audio quality affects transcription accuracy
- Context length is limited by RoBERTa's maximum token limit
- Processing time depends on video length and computational resources
- Internet connection required for initial model downloads


## License

This project is licensed under the MIT License.

## Acknowledgments

- OpenAI's Whisper for transcription
- Hugging Face's Transformers library
- yt-dlp for YouTube video processing
