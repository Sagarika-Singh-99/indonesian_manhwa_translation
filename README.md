## Crossing Language Borders: A Pipeline for Indonesian Manhwa Translation

## Overview
This repository contains the `FINAL_CODE_DEMO.ipynb` notebook, a complete pipeline designed for object detection, OCR (Optical Character Recognition), and translation tasks on images, particularly for analyzing and translating speech bubbles in manhwa (Korean comics). Th translation task focuses on doing Indonesian to Eng translations.

The pipeline includes all of the following steps:
- **Object Detection**: Using YOLOv5 for detecting bounding boxes around speech bubbles.
- **OCR**: Extracting text from the speech bubbles using Tesseract.
- **Translation**: Translating extracted text into the desired language which is done using pre-trained models `final_model`(is included in the zip folder).
- **Overlay**: Rendering translated text back onto the original images.

---

## Prerequisites
This project is tested and should run on **Narnia**. Running locally on other environments may require additional configuration steps. If you encounter errors, we highly recommend switching to **Google Colab**.

### Required Libraries
The following libraries and tools are required. Ensure they are installed before running the notebook:
- `tesseract-ocr`
- `pytesseract`
- `opencv-python`
- `ultralytics`
- `sacremoses`
- Hugging Face Transformers library (`transformers`)

Use the following commands to install missing dependencies in Colab:
```bash
!apt-get install -y tesseract-ocr tesseract-ocr-ind
!pip install pytesseract opencv-python ultralytics sacremoses
```
---

## Pre-trained Models
Training the models from scratch takes over **2 hours**. To save time, we have provided a pre-trained model that you can directly use. Please ensure the following files are available:

1. **Object Detection Model**: Located at `weights/best.pt` in the Drive path referenced in the notebook.
2. **Translation Model**: Located at `/content/drive/MyDrive/NLP_pro/final_trans_model`.(Please change the path according to your needs)

If these files are missing or incorrectly configured, the notebook may fail to execute.

---

## File Path locations
Please note that there are many files, please change the file path location accordingly. 

1. trained_model_path = ".../NLP_pro/yolo_training/manhwa_yolo_training_res2/weights/best.pt" : This contains the path to our fine-tuned Yolov5xu best.pt model for detecing speech bubbles. 
2. test_images_dir = ".../NLP_pro/manhwa_test_2" : This contains 11 images for running the model on. 
3. output_images_dir = ".../NLP_pro/manhwa_test_results/predictions" : Images with bounding boxes will be saved here. 
4. output_crops_dir = ".../NLP_pro/manhwa_test_results/speech_bubble_crops" : Extracted speech bubbles will be saved here. 
5. bbox_output_dir = ".../NLP_pro/manhwa_test_results/test_bbox" : Extracted bounding box dimensions will be saved here. 
6. ocr_results_dir = ".../NLP_pro/manhwa_test_results/speech_bubble_ocr_results" : OCR results will be saved here (json).
7. translations_dir = ".../NLP_pro/manhwa_test_results/speech_bubble_translations" : Translations will be saved here (json).
8. translated_images_dir = ".../NLP_pro/manhwa_test_results/translated_images" : Final translated images will be saved here. 
9. translation_model_path = ".../NLP_pro/final_trans_model" : This contains the path to the fine-tuned MarianMT model for best.pt model to use for translation. 

---

## Pipeline Steps
### 1. Object Detection
The YOLOv5 model detects the speech bubbles in the images and generatesthe bounding boxes.
- Detected bounding boxes are saved as JSON files.

### 2. OCR
Tesseract OCR extracts the text from the detected bounding boxes.
- Outputs are saved as JSON files.

### 3. Translation
The extracted text is then translated using the pre-trained translation model.
- Outputs are saved as JSON files.

### 4. Overlay Translations
The translated text is rendered back onto the original images while also using the original font.
- Final images with translations are saved.

---

## Input and Output
### Input
- Test images should be stored in the directory specified by `test_images_dir` (e.g., `/content/drive/MyDrive/NLP_pro/manhwa_test_2`).

### Output
- Processed images with bounding boxes and translations are saved in:
  - `output_images_dir`: Images with bounding boxes.
  - `translated_images_dir`: Images with translated text.
- Intermediate outputs:
  - `output_crops_dir`: Cropped speech bubbles.
  - `ocr_results_dir`: OCR results.
  - `translations_dir`: Translations in JSON format.
 
---



