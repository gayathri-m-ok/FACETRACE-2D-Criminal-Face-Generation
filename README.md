# FaceTrace: 2D Criminal Face Generation

FaceTrace is a generative AI system in Python that helps create suspect faces from eyewitness descriptions. The user types a text description of a person (facial features, age, hair, expression), and the system generates a realistic face, lets the user refine it, and compares it against faces stored in a database to find close matches.

Computer vision project for generating and editing human faces from text prompts using StyleGAN2-ADA, CLIP-based guidance, and diffusion-based inpainting with manual editing.

## Features

- **Text-to-face generation**: describe the person in plain text through an interactive Gradio interface.
- **Two generators**: faces are produced with Stable Diffusion XL (with ControlNet) and StyleGAN2-ADA (pretrained on FFHQ).
- **Automatic best-match selection**: CLIP (ViT-L/14) scores each candidate against the description and the closest one is selected.
- **Prompt-based editing with masking**: draw a mask over a region (cheek, eyes, hair), describe the change (for example "small scar on left cheek" or "blue sunglasses"), and Stable Diffusion inpainting regenerates only that area.
- **Manual editing**: draw directly on the face to make changes by hand.
- **Iterative refinement**: a "Continue Editing" button reloads the latest result for repeated edits. Every output is saved together with its mask.
- **Face database and similarity check**: final faces are saved to a database, and a generated face is compared against stored faces to find close matches, supporting forensic identification.
- **Evaluation**: CLIP embeddings, VisualBERT and semantic similarity measure how closely a generated face matches the description. OpenCV handles face processing and matching.

## How it works

1. **Describe**: enter a text description of the person.
2. **Generate**: Stable Diffusion XL and StyleGAN2-ADA each produce a candidate face.
3. **Select**: CLIP scores both candidates and picks the closest match to the description.
4. **Edit**: refine the face with mask-based inpainting or manual drawing, as many times as needed.
5. **Save and match**: store the final face in the database and run the similarity check against stored faces.

## Tech stack

| Area | Tools |
|---|---|
| Language | Python |
| Deep learning | PyTorch |
| Generative models | Stable Diffusion XL, ControlNet, StyleGAN2-ADA, Stable Diffusion Inpainting |
| Vision-language | CLIP (ViT-L/14), VisualBERT |
| Image processing | OpenCV, Pillow, NumPy |
| Interface | Gradio |
| Environment | Kaggle notebook (GPU) |

## Screenshots

![Screenshot 1](Screenshot%202025-11-23%20111013.png)
![Screenshot 2](Screenshot%202025-11-23%20111151.png)
![Screenshot 3](Screenshot%202025-11-26%20201716.png)
![Screenshot 4](Screenshot%202025-11-26%20225827.png)

## How to run

1. Open `2d-face-generation-main.ipynb` in Kaggle (or any GPU environment).
2. Install the dependencies:
   ```bash
   pip install torch diffusers transformers gradio pillow numpy opencv-python
   pip install git+https://github.com/openai/CLIP.git
   ```
3. Download the pretrained FFHQ StyleGAN2-ADA model (`ffhq.pkl`) and set its path in the notebook.
4. Load the Stable Diffusion XL and inpainting pipelines.
5. Run all cells. Gradio launches the interface and prints a local and a public link.

## Example prompts

- `portrait photo of a middle-aged man with brown hair and glasses`
- Edit prompts: `thin black mustache`, `small scar on left cheek`, `blue sunglasses`

## Notes

- This project is for research and learning. Generated faces are synthetic and should not be used as the only basis for identifying a real person.
- Results depend on the prompt, the random seed and GPU availability.

## Author

**Gayathri Mohandas**
B.Tech, Computer Science and Engineering, Amrita Vishwa Vidyapeetham
GitHub: [gayathri-m-ok](https://github.com/gayathri-m-ok)
