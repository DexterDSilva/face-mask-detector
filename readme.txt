COVID-19: Face Mask Detector with OpenCV, Keras/TensorFlow, and Deep Learning
by Adrian Rosebrock on May 4, 2020

In this tutorial, you will learn how to train a COVID-19 face mask detector with OpenCV, Keras/TensorFlow, and Deep Learning.

Last month, I authored a blog post on detecting COVID-19 in X-ray images using deep learning.

Readers really enjoyed learning from the timely, practical application of that tutorial, so today we are going to look at another COVID-related application of computer vision, this one on detecting face masks with OpenCV and Keras/TensorFlow.

I was inspired to author this tutorial after:

Receiving numerous requests from PyImageSearch readers asking that I write such a blog post
Seeing others implement their own solutions (my favorite being Prajna Bhandary’s, which we are going to build from today)
If deployed correctly, the COVID-19 mask detector we’re building here today could potentially be used to help ensure your safety and the safety of others (but I’ll leave that to the medical professionals to decide on, implement, and distribute in the wild).

pwd:
Users/dexterdsilva/Documents/Developer/MachineLearning/pyimage/face-mask-detector

env:
py3cv4tf2 or py3cv4tf2tor

https://www.pyimagesearch.com/2020/05/04/covid-19-face-mask-detector-with-opencv-keras-tensorflow-and-deep-learning/


(py3cv4tf2tor) Dexters-MacBook:face-mask-detector dexterdsilva$ tree --dirsfirst --filelimit 12
.
├── dataset
│   ├── with_mask [690 entries exceeds filelimit, not opening dir]
│   └── without_mask [686 entries exceeds filelimit, not opening dir]
├── examples
│   ├── example_01.png
│   ├── example_02.png
│   └── example_03.png
├── face_detector
│   ├── deploy.prototxt
│   ├── readme.txt
│   └── res10_300x300_ssd_iter_140000.caffemodel
├── generate-mask-images
│   └── observations-master
│       ├── experiements
│       │   ├── data
│       │   │   ├── with_mask
│       │   │   ├── without_mask
│       │   │   └── readme.txt
│       │   └── dest_folder
│       │       ├── test
│       │       │   ├── with_mask [97 entries exceeds filelimit, not opening dir]
│       │       │   └── without_mask [97 entries exceeds filelimit, not opening dir]
│       │       ├── train
│       │       │   ├── with_mask [658 entries exceeds filelimit, not opening dir]
│       │       │   └── without_mask [657 entries exceeds filelimit, not opening dir]
│       │       ├── val
│       │       │   ├── with_mask [71 entries exceeds filelimit, not opening dir]
│       │       │   └── without_mask [71 entries exceeds filelimit, not opening dir]
│       │       ├── test.csv
│       │       └── train.csv
│       ├── mask_classifier
│       │   ├── Data_Generator
│       │   │   ├── __pycache__
│       │   │   │   ├── Augment_img.cpython-37.pyc
│       │   │   │   ├── __init__.cpython-37.pyc
│       │   │   │   ├── __main__.cpython-37.pyc
│       │   │   │   ├── mask.cpython-36.pyc
│       │   │   │   └── mask.cpython-37.pyc
│       │   │   ├── images
│       │   │   │   ├── blue-mask.png
│       │   │   │   └── default-mask.png
│       │   │   ├── loop_through_folder.py
│       │   │   └── mask.py
│       │   ├── alarm.wav
│       │   ├── inference.py
│       │   ├── label_detect.py
│       │   ├── requirements.txt.
│       │   ├── training.ipynb
│       │   └── webcam_detect.py
│       └── README.md
├── COVID-19:\ Face\ Mask\ Detector\ with\ OpenCV,\ Keras:TensorFlow,\ and\ Deep\ Learning\ -\ PyImageSearch.pdf
├── COVID-19_\ Face\ Mask\ Detector\ with\ OpenCV,\ Keras_TensorFlow,\ and\ Deep\ Learning\ -\ PyImageSearch.pdf
├── detect_mask_image.py
├── detect_mask_video.py
├── mask_detector.model
├── plot.png
├── readme.txt
└── train_mask_detector.py

25 directories, 33 files