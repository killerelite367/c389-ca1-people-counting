# C389 CA1 People Counting Assistant

The project starts with a YOLO detector for **person_left** and **person_right**. The T4 video extension uses **ByteTrack** to follow IDs through a user-marked waiting area and crossing line. The Gradio demo displays an annotated video, counts, and a table of observed waiting time by ID.

| Where to start | What it contains |
|---|---|
| [T4 video Gradio notebook](notebooks/04_t4_video_gradio.ipynb) | Upload and mark a clip, process it, and download the results. |
| [Improved checkpoint](models/improved/) | The exact 100-epoch best.pt used in the saved T4 example, with its SHA-256. |
| [Training notebook](notebooks/01_train_improved.ipynb) | Dataset setup, YOLO26n training and image evaluation. |
| [Image Gradio notebook](notebooks/02_image_gradio.ipynb) | Lesson 4 image demo with direction counts. |
| [Earlier T4 tuning notebook](notebooks/03_t4_notebook_reference.ipynb) | Historical reference for the original tuning and evaluation workflow. |
| [Model comparison](evaluation/README.md) | Verified image test metrics, training plots, and saved T4 outputs. |
| [Original model](models/original/) | Where the teammate adds the earlier checkpoint and evidence. |

## Run the T4 demo

**Local Jupyter.** Clone this repository and open notebooks/04_t4_video_gradio.ipynb from the checkout. Run sections 1–11 in order. Section 9 finds the included model from the repository root or notebook folder.

**Colab.** Open the same notebook, choose a GPU runtime and run sections 1–11. Section 9 checks for a checkout at /content/c389-ca1-people-counting and can also load artifacts/L3/best.pt from **c389 ca1 final (improved model)** in your Drive. If your copy is in a different location, set MODEL_PATH in section 9.

Open the Gradio link, upload an MP4 or MOV, and select **Load video**. Click four corners of the waiting area and two endpoints of the crossing line. Select **Process video**. Use the results ZIP to keep the video, settings and CSVs together.

The default is a qualifying stationary wait of at least **1 second** within the polygon. The >= symbol marks an incomplete wait. The app counts crossing-line events by eligible track ID, including people who previously waited. The saved analysis has a separate **crossed_without_observed_wait** category for the T4 comparison.

## Training and clips

The training notebook uses the team's Roboflow YOLO dataset version 4. Set ROBOFLOW_API_KEY using Colab Secrets or enter it at the secure prompt. Use the team dataset when reproducing the 100-epoch model. Training images and video clips are in the team's [Drive project folder](https://drive.google.com/drive/folders/1se1ukgZAupW_4Y-dL7tmdAltEr9gN-tp), which requires separate Drive access. The notebooks are included with their cell outputs cleared. Saved metrics and plots are under evaluation/.
