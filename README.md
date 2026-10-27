# OpenCV Face Dataset Preparation

A notebook that detects faces in existing images and saves cropped face images for a dataset.

**Technology:** Python, OpenCV and Google Colab.

## Run or inspect

Open `notebooks/prepare_face_dataset.ipynb` in Google Colab. It uses `google.colab.drive` to mount your Drive. Set `image_directory`, `OUTPUT_DIR` and `person_name` for your own input images before running.

Install `opencv-python` if your environment does not include OpenCV. The supplied `requirements.txt` lists that dependency. The code expects existing image files and uses a Haar cascade; it does not train a recognition classifier. Notebook outputs and execution counts have been cleared. No face dataset is included.

## Repository preparation

Source and required assets were organised from existing coursework. Build outputs and IDE state are excluded. Original reports, slides and course handouts remain in the separate full backup; they are not bundled for public upload. Real credentials and original database records are not included. See the collection `UPLOAD_GUIDE.md` for upload steps and preparation notes.

## Validation status

The preparation checked file paths, Python syntax where applicable, structured files, credential removal and package integrity. Windows desktop apps, Flutter apps, hardware and online services have not been built or run in this environment.
