# AI-Story-to-Video-Generator-using-Hugging-Face-Models

# AI Story-to-Video Generator 🎬

An intelligent Python application that automatically generates engaging 30-second videos from AI-created stories using Hugging Face models for text generation, image creation, and audio narration.

## 🌟 Features

- **Dynamic Story Generation**: Creates unique short stories using advanced language models
- **Visual Scene Creation**: Generates 6 high-quality images corresponding to each story sentence
- **Emotional Audio Narration**: Produces natural-sounding speech with emotional context
- **Automated Video Assembly**: Combines all elements into a polished 30-second video
- **Robust Fallback System**: Works even when API services are unavailable
- **Customizable Themes**: Easy to modify story themes and generation parameters

## 🎯 How It Works

```
Story Prompt → AI Text Generation → Scene Descriptions
     ↓                                      ↓
Audio Narration ← Video Assembly ← Image Generation
```

1. **Story Creation**: Generates a 6-sentence story based on random themes
2. **Image Generation**: Creates visual representations for each sentence
3. **Audio Production**: Converts story to speech with emotional emphasis
4. **Video Compilation**: Assembles images and audio into final video

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- Hugging Face account (for API access)
- At least 4GB RAM recommended

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ai-story-video-generator.git
   cd ai-story-video-generator
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Get your Hugging Face API key**
   - Visit [Hugging Face Settings](https://huggingface.co/settings/tokens)
   - Create a new token with read permissions
   - Copy the token for the next step

4. **Configure the application**
   ```python
   # In the main script, replace:
   HF_API_KEY = "your_hugging_face_api_key_here"
   # With your actual API key:
   HF_API_KEY = "hf_xxxxxxxxxxxxxxxxxxxx"
   ```

5. **Run the generator**
   ```python
   python story_video_generator.py
   # Or in Jupyter notebook:
   main()
   ```

## 📦 Required Dependencies

```txt
torch>=1.9.0
transformers>=4.20.0
diffusers>=0.21.0
moviepy>=1.0.3
pillow>=9.0.0
soundfile>=0.10.3
requests>=2.28.0
numpy>=1.21.0
opencv-python>=4.5.0
pyttsx3>=2.90
```

## 🎛 Configuration Options

### Model Selection
```python
class Config:
    TEXT_MODEL = "microsoft/DialoGPT-medium"      # Text generation
    IMAGE_MODEL = "runwayml/stable-diffusion-v1-5"  # Image generation  
    AUDIO_MODEL = "microsoft/speecht5_tts"        # Text-to-speech
```

### Video Settings
```python
VIDEO_DURATION = 30  # Total video length in seconds
IMAGE_DURATION = 5   # Duration per image in seconds
NUM_IMAGES = 6       # Number of images to generate
```

### Story Themes
Customize story themes in `StoryGenerator.generate_story_prompt()`:
```python
themes = [
    "A magical forest where trees whisper secrets",
    "An astronaut discovering a new planet",
    "A young artist finding inspiration in a bustling city",
    # Add your own themes here
]
```

## 📂 Project Structure

```
ai-story-video-generator/
├── story_video_generator.py    # Main application
├── requirements.txt           # Dependencies
├── README.md                 # This file
└── story_video_output/       # Generated content (created automatically)
    ├── generated_story.txt   # Story text
    ├── generated_images/     # Scene images
    │   ├── scene_1.png
    │   └── ...
    ├── story_audio.wav      # Audio narration
    └── final_story_video.mp4 # Final video
```

## 🎨 Sample Output

The generator produces:

- **Story Example**:
  ```
  1. In a mystical forest, ancient trees swayed gently in the moonlight.
  2. A young wanderer discovered a hidden path glowing with ethereal light.
  3. Strange creatures with luminescent eyes watched from the shadows.
  4. The wanderer followed the path to a clearing filled with floating crystals.
  5. Each crystal hummed with a different magical melody.
  6. As dawn broke, the wanderer realized they had found their true home.
  ```

- **Generated Files**:
  - 6 high-quality scene images (512x512 pixels)
  - Emotional audio narration
  - 30-second MP4 video combining all elements

## 🔧 Troubleshooting

### Common Issues

**1. API Rate Limits**
- Wait a few minutes between requests
- The system automatically falls back to local models

**2. CUDA/GPU Issues**
```bash
# For CPU-only installation:
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

**3. MoviePy Errors**
```bash
# Install imageio-ffmpeg:
pip install imageio-ffmpeg
```

**4. Audio Generation Issues**
- Ensure `pyttsx3` is installed for local TTS
- Check system audio drivers are working

### Performance Tips

- **For faster generation**: Use smaller models in config
- **For better quality**: Increase image generation steps
- **For longer videos**: Adjust `VIDEO_DURATION` and `IMAGE_DURATION`

## 🎪 Advanced Usage

### Custom Model Integration

```python
# Add your own models:
class CustomConfig(Config):
    TEXT_MODEL = "your-custom/text-model"
    IMAGE_MODEL = "your-custom/image-model"
    AUDIO_MODEL = "your-custom/audio-model"
```

### Batch Generation
```python
# Generate multiple videos:
for i in range(5):
    print(f"Generating video {i+1}")
    video_path = main()
    if video_path:
        # Rename to avoid overwriting
        new_name = f"story_video_{i+1}.mp4"
        os.rename(video_path, os.path.join(config.OUTPUT_DIR, new_name))
```

### Custom Story Input
```python
# Use your own story:
custom_sentences = [
    "Your first sentence here.",
    "Your second sentence here.",
    # ... up to 6 sentences
]

# Skip story generation and use custom sentences directly
image_paths = []
for i, sentence in enumerate(custom_sentences):
    image_prompt = image_gen.create_image_prompt(sentence, i)
    image = image_gen.generate_image_api(image_prompt, i)
    # ... continue with image saving
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup
```bash
# Install development dependencies
pip install -e .
pip install pytest black flake8

# Run tests
pytest tests/

# Format code
black story_video_generator.py
```

## 📋 Roadmap

- [ ] Support for longer videos (1-5 minutes)
- [ ] Multiple narration voices
- [ ] Background music generation
- [ ] Interactive web interface
- [ ] Batch processing capabilities
- [ ] Custom video transitions
- [ ] Multi-language support
- [ ] Cloud deployment options

## 🐛 Known Issues

- Large models may require significant RAM (8GB+ recommended)
- First-time model downloads can be slow
- Some TTS models may not work on all systems
- Video encoding requires ffmpeg

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Hugging Face](https://huggingface.co/) for providing amazing AI models
- [MoviePy](https://zulko.github.io/moviepy/) for video processing capabilities  
- [Stable Diffusion](https://stability.ai/stable-diffusion) for image generation
- The open-source AI community for continuous innovation

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/RashidNoor42/AI-Story-to-Video-Generator-using-Hugging-Face-Models/issues)
- **Discussions**: [GitHub Discussions](https://github.com/RashidNoor42/AI-Story-to-Video-Generator-using-Hugging-Face-Models/discussions)
- **Email**: rnoor6309@gmail.com

## 🔗 Related Projects

- [Text-to-Image Generation](https://github.com/CompVis/stable-diffusion)
- [Transformers Library](https://github.com/huggingface/transformers)
- [MoviePy Documentation](https://moviepy.readthedocs.io/)

---

**Made with ❤️ and AI** | Star ⭐ this repo if you found it useful!
