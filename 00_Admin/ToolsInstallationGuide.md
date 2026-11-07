# About

This file will contain all of the tools used within the project and their necessary installations.

# Python

The team has chosen to run Python 3.14.

## Python Packages

The python packages used can be installed with

```bash
pip install opencv-python pytesseract numpy
```

# ffmpeg

For easy processing of images and videos, users can install ffmpeg. On Windows, this can be done using

```cmd
winget install ffmpeg
```

As an example of how to use it to extract one frame from a video, the command below can be used to extract the frame at 3 minutes and 49 seconds.

```cmd
ffmpeg -ss 00:03:49 -i recording_oct_5.mp4 -frames:v 1 half_b_half_doppler.png
```

# OCR

For ocr, Tesseract OCR was used. On Windows, this can be installed from: https://github.com/UB-Mannheim/tesseract/wiki.
