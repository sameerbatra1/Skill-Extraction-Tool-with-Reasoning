# Skill-Extraction-Tool-with-Reasoning

A fine-tuned Phi-2 language model for extracting skills from job descriptions using Chain-of-Thought (CoT) reasoning and knowledge distillation from DeepSeek R1.

## 📋 Overview

This project leverages Microsoft's Phi-2 model, fine-tuned specifically for skill extraction from job descriptions. By combining Phi-2's strong reasoning capabilities (trained on high-quality textbook data) with knowledge distillation from DeepSeek R1, this model provides detailed, step-by-step skill extraction with transparent reasoning.

### Key Features

- **Chain-of-Thought Reasoning**: Model explains its extraction process step-by-step
- **Knowledge Distillation**: Trained using outputs from DeepSeek R1 for enhanced accuracy
- **Efficient Fine-tuning**: Uses LoRA/PEFT for parameter-efficient training
- **4-bit Quantization**: Optimized for inference with reduced memory footprint
- **Phi-2 Foundation**: Built on Phi-2's 2.7B parameter model with strong reasoning abilities

## 🚀 Quick Start (3 Easy Steps!)

### Step 1: Get Hugging Face Token

1. Create a free account at [Hugging Face](https://huggingface.co/join)
2. Go to [Settings → Access Tokens](https://huggingface.co/settings/tokens)
3. Click "New token" → Give it a name → Select "Read" access → Create
4. **Copy your token** (you'll need it in Step 3)

### Step 2: Download Files from GitHub
Download these two items from this repository:

1. **`model_adapters/`** folder - Contains the fine-tuned LoRA adapter weights
2. **`Running_Model.ipynb`** - The Colab notebook for inference

### Step 3: Run in Google Colab
#### 3.1 Open the Notebook
- Or upload `Running_Model.ipynb` to [Google Colab](https://colab.research.google.com)
#### 3.2 Enable GPU
1. Go to **Runtime** → **Change runtime type**
2. Select **T4 GPU** (free tier)
3. Click **Save**
#### 3.3 Add Your Hugging Face Token
In Colab, you have two options[file:143]:
**Option A: Use Colab Secrets (Recommended)**
1. Click the 🔑 icon in the left sidebar
2. Add secret: Name = `HF_TOKEN`, Value = (paste your token)
3. Enable "Notebook access" toggle
**Option B: Add Token Directly in Code**
In the second code cell, uncomment and add your token:
```python
token = 'your_hugging_face_token_here'
```
#### 3.4 Upload Adapter Files
Upload the `model_adapters` folder to your Colab environment:
**Option A: Upload Directly to Colab**
```python
from google.colab import files
import zipfile
```
Upload the model_adapters folder (zipped)
```python
uploaded = files.upload()
# unzip
!unzip model_adapters.zip -d /content/
```
**Option B: Use Google Drive** (Recommended for repeated use)
1. Upload `model_adapters` folder to your Google Drive
2. In the notebook, mount Drive and update the path:
```pyhton
from google.colab import drive
drive.mount('/content/drive')
```
Update adapter_path in the code cell
```python
adapter_path = "/content/drive/MyDrive/model_adapters"
```
#### 3.5 Run All Cells

Click **Runtime** → **Run all** and wait 2-3 minutes for:
- Dependencies to install
- Model to load (~5GB download on first run)
- Adapter to load
You should see: `✓ Model with adapter loaded successfully!`
## 📝 Usage Examples
The notebook includes a ready-to-use function and example job descriptions

## 🔧 Technical Details

### Model Architecture
- **Base Model**: Microsoft Phi-2 (2.7B parameters)
- **Fine-tuning**: LoRA with r=8, alpha=16
- **Target Modules**: q_proj, v_proj
- **Quantization**: 4-bit NF4[file:143]

### Training Approach
- **Knowledge Distillation**: DeepSeek R1 outputs as training targets
- **Chain-of-Thought**: Model provides reasoning alongside skill extraction
- **Data**: Job descriptions with annotated skills and CoT reasoning paths

### Why Phi-2?
- Trained on high-quality textbook and code data
- Strong reasoning and instruction-following capabilities
- Efficient 2.7B parameter size (runs on free T4 GPU)
- Excellent performance-to-size ratio

## ⚡ Performance

- **Inference Time**: ~10-15 seconds per job description on T4 GPU
- **Memory Usage**: ~6-7GB VRAM (fits on free Colab)
- **Model Size**: 
  - Base model: ~5GB (downloaded once, cached)
  - Adapter: ~33MB
- **Quality**: Extracts both technical and soft skills with detailed reasoning[file:143]

## 🔍 Example Job Descriptions

The notebook includes two complete examples[file:143]:
1. **Capital One Senior Lead Software Engineer** - Full stack role with cloud and microservices
2. **Nuro Applied Research Scientist** - ML/LLM role with autonomous vehicles focus

## 💡 Tips

- **First run takes 5-10 minutes** to download the base Phi-2 model
- **Subsequent runs are much faster** (~30 seconds to load)
- **Adjust generation parameters** in the function if needed:
  - `max_tokens=512` - Increase for longer outputs
  - `min_tokens=50` - Minimum generation length
  - `temperature=0.7` - Lower for more focused outputs

## 🐛 Troubleshooting

**"HF_TOKEN not found"**: Make sure you've added your Hugging Face token using one of the methods in Step 3.3[file:143]

**Out of Memory**: Make sure you selected T4 GPU runtime. If still issues, restart runtime and try again.

**Adapter not loading**: Verify the `adapter_path` points to the correct location of your `model_adapters` folder[file:143]

**Slow first run**: This is normal - Phi-2 model download is ~5GB. Use the time to grab coffee! ☕

## 🤝 Contributing

Contributions welcome! Feel free to:
- Report issues or bugs
- Suggest improvements
- Share your results
- Add more example job descriptions

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- **Microsoft** for the Phi-2 base model
- **DeepSeek** for the R1 model used in knowledge distillation
- **Hugging Face** for transformers and PEFT libraries
- **Google Colab** for free GPU access

## 📧 Contact

Questions? Open an issue on GitHub.

## 🔗 References

- [Phi-2 Model Card](https://huggingface.co/microsoft/phi-2)
- [PEFT Documentation](https://huggingface.co/docs/peft)
- [DeepSeek R1](https://github.com/deepseek-ai/DeepSeek-R1)

---

**System Requirements**: Google Colab with free T4 GPU (15GB VRAM)

**Total Setup Time**: 3-5 minutes (first run: 10 minutes with model download)
