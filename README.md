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

## Reproduce in Google Colab

**Prerequisites:** a Google account with Drive access, Google Colab, and a few JPG or PNG input images. The notebook expects Colab; a local Python installation does not provide `google.colab.drive`.

1. Open Google Colab, choose **File → Open notebook → GitHub**, and enter `https://github.com/ChuaJiaSheng/opencv-face-dataset`. Select `notebooks/prepare_face_dataset.ipynb` and save a working copy.
2. In Google Drive, create `MyDrive/face_dataset/input` and put your test images there. Use images containing a single person if all output files will carry that person's label.
3. Add and run an initial dependency cell if OpenCV is missing:

   ```python
   %pip install opencv-python
   ```

4. Set the configuration cell:

   ```python
   image_directory = "/content/gdrive/MyDrive/face_dataset/input"
   person_name = "person_01"
   OUTPUT_DIR = "/content/gdrive/MyDrive/face_dataset/cropped/"
   ```

5. Run the cells in order. Complete the Drive authorization when `drive.mount('/content/gdrive')` runs.
6. Open the `cropped` folder in Drive and inspect the saved images.

**Expected result:** each detected face is saved as a numbered JPG such as `person_01_0.jpg`; the notebook prints the saved path. An input with no detected face produces a no-detections message and no crop. Successful execution alone does not guarantee correct face detection.

**Troubleshooting:** if the input directory is missing, check the Drive mount and exact path; if no images are found, check extensions and put files directly in `input`; if crops are wrong, use clearer frontal images and review detector parameters. Use a new output directory or label for a second run to avoid overwriting earlier crops.

For a local copy of the notebook:

```sh
git clone https://github.com/ChuaJiaSheng/opencv-face-dataset.git
cd opencv-face-dataset
```

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
