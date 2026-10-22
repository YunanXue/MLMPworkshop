# Easy Start Guide for Segment Anything (SAM)

This project uses a model called SAM to find objects in an image and save the object masks as files.

You do not need to understand the code to start. Just copy and paste the commands below in order.

## What this project does

- Looks at a single image
- Finds object masks automatically
- Saves the mask images in a folder
- Creates a CSV file with mask details

For the sample image in this project, the output will be stored in:

```
output_masks/demo_run/
```

or, in this repository, the example folder is:

```
output_masks/demo_run/
```

---

## 1) Open a terminal in the project folder

Make sure you are in the project root folder. In your terminal, run:

```bash
cd /home/Desktop/
git clone https://github.com/facebookresearch/segment-anything.git
cd segment-anything
```

If you are already in the folder, you can skip this step.

---

## 2) Create a virtual environment
This project requires Python 3.8+ and PyTorch / TorchVision. The repo README states:
- `python>=3.8`
- `pytorch>=1.7`
- `torchvision>=0.8`

This keeps the project packages separate from the rest of your computer.
Use this command to activate the environment:

```bash
uv venv
source .venv/bin/activate
```

If `uv` is not installed yet, run:

```bash
pip install uv
```

Then run the two commands above again.

---

## 3) Install the required Python packages

Copy and paste this whole block:

```bash
uv pip install --upgrade pip
uv pip install numpy torch torchvision
uv pip install -e .
uv pip install opencv-python pycocotools matplotlib onnxruntime onnx
```

This installs the base Python libraries plus the extra tools needed for mask creation and image handling.

---

## 4) Create a 'requirements.txt' in segment-anything folder
create a 'requirements.txt' and paste this in the 'requirements.txt' and save:
```bash
numpy
torch>=1.7
torchvision>=0.8
```

Then install it manually:
```bash
uv pip install -r requirements.txt
```

---


## 5) Download the model file

This project needs the pre-trained SAM model file.

Download it here:

```bash
wget https://dl.fbaipublicfiles.com/segment_anything/sam_vit_h_4b8939.pth
```

After downloading, make sure the file is in the project root folder:

```bash
ls
```

You should see a file named:

```bash
sam_vit_h_4b8939.pth
```

---


## 6) Run the model on the sample image

This is the main command that runs the automatic mask generator.

### If your computer has a GPU

```bash
python scripts/amg.py \
  --checkpoint ./sam_vit_h_4b8939.pth \
  --model-type vit_h \
  --input ./assets/masks1.png \
  --output ./output_masks/demo_run \
  --device cuda
```

### If your computer does NOT have a GPU

```bash
python scripts/amg.py \
  --checkpoint ./sam_vit_h_4b8939.pth \
  --model-type vit_h \
  --input ./assets/masks1.png \
  --output ./output_masks/demo_run \
  --device cpu
```

---

## 6) What should happen next?

The script will process the image and create output in a new folder.

You should see something like this:

```bash
output_masks/demo_run/
└── masks1/
    ├── 0.png
    ├── 1.png
    ├── 2.png
    ├── ...
    └── metadata.csv
```

- `0.png`, `1.png`, etc. are the generated mask images
- `metadata.csv` contains information about each mask

---

## 7) Want to use your own image?

Replace the input path with your own image file.

Example:

```bash
python scripts/amg.py \
  --checkpoint ./sam_vit_h_4b8939.pth \
  --model-type vit_h \
  --input ./my_image.png \
  --output ./my_output_folder \
  --device cpu
```

Just make sure your image is inside the project folder or give the full path.

---

## 8) Common problems and easy fixes

### Problem: `uv: command not found`

Install it:

```bash
pip install uv
```

### Problem: Python version issues

This project works best with Python 3.8 or newer.

Check your version:

```bash
python --version
```

### Problem: model file not found

Make sure the checkpoint file is in the project root folder and named exactly:

```bash
sam_vit_h_4b8939.pth
```

### Problem: CUDA not available

Use the CPU version of the command.

---




## 9) Notes

This project is based on the official Meta Segment Anything repository, but the commands above are written for a beginner-friendly setup.

If you want to make this even easier, you can later add a shell script that runs all the steps with one click.

---




## One real failure

Category: Environment / dependency mismatch

Root cause:
The repository does not ship with a requirements.txt or pyproject.toml. The README expects a PyTorch stack and optional packages, but the exact dependency versions are not pinned in the repo itself. This can lead to version conflicts if the environment is created with incompatible Python or PyTorch packages.

Minimal fix:
Use a compatible Python version and install the supported stack explicitly:
uv venv
source .venv/bin/activate
uv pip install numpy torch torchvision
uv pip install -e .
This keeps the environment aligned with the project’s documented requirements without guessing unsupported versions.

---



## Repo map

Environment: Local Python project environment using uv/venv with PyTorch, OpenCV, and SAM dependencies installed.

Entry point: scripts/amg.py

Model: sam_vit_h_4b8939.pth (SAM ViT-H checkpoint)

Input: ./assets/masks1.png

Output: ./output_masks/demo_run/

---



## AI agent check
I used VS Code Copilot.

It suggested checking the missing project dependencies, confirming the environment setup, and running the correct SAM mask-generation command with the project checkpoint file and input image.

I used the repository’s actual inference command: python scripts/amg.py --checkpoint ./sam_vit_h_4b8939.pth --model-type vit_h --input ./assets/masks1.png --output ./output_masks/demo_run --device cuda

I verified that the command exited successfully from the repo root and produced output in the specified output directory.


---
**Reviewer:**
Qiyuan Xia
Reproduction result: PASS
