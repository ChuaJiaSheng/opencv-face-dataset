# OpenCV Face Dataset Preparation

A Google Colab notebook that finds faces in existing images and saves rectangular face crops into a Google Drive folder. It prepares image data using OpenCV's Haar cascade detector; it does not train or evaluate a face-recognition model.

**Stack:** Python · OpenCV · Google Colab · Google Drive

## Processing workflow

1. Mount Google Drive in Colab.
2. List supported images in the selected input directory.
3. Read each image and convert it to grayscale.
4. Detect faces using `haarcascade_frontalface_default.xml`.
5. Crop each detected rectangle from the original colour image.
6. Save the crops with a person label and a running number.

## Run in Colab

1. Open [notebooks/prepare_face_dataset.ipynb](notebooks/prepare_face_dataset.ipynb) in Google Colab.
2. Install the dependency if it is missing:

   ```python
   %pip install opencv-python
   ```

3. Set the three configuration values in the notebook:

   ```python
   image_directory = "/content/gdrive/MyDrive/face_dataset/input"
   person_name = "person_01"
   OUTPUT_DIR = "/content/gdrive/MyDrive/face_dataset/cropped/"
   ```

4. Put your input images in the chosen Drive folder, run the cells in order, and approve the Drive mount for your own account.
5. Inspect the resulting crops before using them in a dataset.

The notebook uses `google.colab.drive`. For local Python use, replace the Drive mount and Colab paths with local directories; installing OpenCV alone does not provide the Colab module.

## Inputs and outputs

| Item | Behaviour |
| --- | --- |
| Supported extensions | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff` |
| Directory traversal | Files in the selected directory; no recursive subfolder scan |
| Detector settings | `scaleFactor=1.1`, `minNeighbors=5`, `minSize=(30, 30)` |
| Output names | `<person_name>_<number>.jpg` |
| Multiple faces | Each detected face is saved as a separate crop |
| Unreadable images or no detections | A message is printed and processing continues |

## Repository guide

- [Notebook](notebooks/prepare_face_dataset.ipynb): configuration, detection functions, and directory-processing call.
- [requirements.txt](requirements.txt): OpenCV dependency.
- No source images, cropped faces, trained models, or executed notebook outputs are included.

## Limitations

All faces found in a run receive the same `person_name`; the code does not identify which person appears in an image. Input ordering is not explicitly sorted, so filenames are not a stable identity mapping. The counter restarts at zero for each run and existing output names can be overwritten. Detection quality and crop correctness need manual review.
