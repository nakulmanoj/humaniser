# AI Text Humanizer

A fine-tuned Phi-3 model that converts formal/neutral text into casual, conversational language that gets past AI detectors like Quillbot and ZeroGPT. Trained on Reddit comments to capture natural human writing style.

## Features

- Converts formal text to casual, conversational tone
- Maintains meaning while making text more approachable
- Removes excessive formality and corporate speak
- Fine-tuned on 1400+ examples of natural human writing

## Examples

**Input:** "The meeting has been scheduled for next Tuesday at 3 PM."

**Output:** "We're meeting next Tuesday at 3."

---

**Input:** "Please ensure all documents are submitted before the deadline."

**Output:** "Make sure you get all your docs in before the deadline."

## Quick Start

### Installation
```bash
# Clone the repository
git clone <your-repo-url>
cd humaniser

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install torch transformers datasets peft accelerate bitsandbytes
```

### Usage
```bash
# Open the inference notebook
jupyter notebook inference.ipynb

# Or run directly in Python - see inference.ipynb for the humanise() function
```

Basic usage:
```python
from inference import humanise

text = "The package has been delivered to your residence."
result = humanise(text)
print(result)  # "Package arrived at your place."
```

## Project Structure
```
humaniser/
├── inference.ipynb          # Run this for quick inference
├── train.ipynb             # Training script (optional)
├── prepare_data.ipynb      # Data preparation (optional)
├── data.json               # Raw training data
├── trained.json            # Formatted training data
└── README.md
```

## Training Your Own Model

1. Add your data to `data.json` (input/output pairs)
2. Run `prepare_data.ipynb` to format the data
3. Run `train.ipynb` to train (takes ~30 mins on modern GPU)
4. The trained model saves to `humaniser_lora/`

See the notebooks for detailed instructions.

## Model Details

- **Base Model**: microsoft/phi-3-mini-4k-instruct
- **Method**: LoRA fine-tuning
- **Training Data**: 1400+ Reddit comment pairs
- **Hardware**: Trained on consumer GPU (8GB VRAM)

## Requirements

- Python 3.8+
- CUDA-capable GPU with 8GB+ VRAM
- 10GB disk space

## Limitations

- Best for English text under 200 words
- Optimized for casual/conversational style
- May occasionally add creative details

## License

MIT

## Acknowledgments

- [Transformers](https://github.com/huggingface/transformers) by Hugging Face
- [Phi-3](https://huggingface.co/microsoft/phi-3-mini-4k-instruct) by Microsoft
- [PEFT](https://github.com/huggingface/peft) for LoRA training