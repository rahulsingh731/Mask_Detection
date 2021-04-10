## Getting Started
### Conda (Recommended)

```bash
# Tensorflow CPU
conda env create -f conda-cpu.yml
conda activate yolov4-cpu

# Tensorflow GPU
conda env create -f conda-gpu.yml
conda activate yolov4-gpu
```

### Pip
```bash
# TensorFlow CPU
pip install -r requirements.txt

# TensorFlow GPU
pip install -r requirements-gpu.txt
```

## Adding Variables file 
Use the link to download the file: https://drive.google.com/file/d/17IDb8ixnD-0k-paEYtR-hG5ma75sv44R/view?usp=sharing
Add the above file in checkpoints/custom-416/variables.

## Using Custom Trained YOLOv4 Weights


USE MY Face Mask Detection TRAINED CUSTOM WEIGHTS: https://drive.google.com/file/d/11i2uwT0D-vx3HF3AHL3MXXxs564L3jDb/view?usp=sharing

Copy and paste your custom .weights file into the 'data' folder.

### Counting Total People with Mask and Non Mask (total objects or per class)
I have used a custom function within the file [core/functions.py] that can be used to count and keep track of the number of objects detected at a given moment within each image or video. It can be used to count total objects found or can count number of objects detected per class.

#### Count Total Objects
To count total objects all that is needed is to add the custom flag "--count" to your detect.py or detect_video.py command.
```
# Run yolov4 model while counting total objects detected
python detect.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --images ./data/images/dog.jpg --count
```

#### Count Objects Per Class(i.e Only Mask or Non Mask)
To count the number of objects for each individual class of your object detector you need to add the custom flag "--count" as well as change one line in the detect.py or detect_video.py script. By default the count_objects function has a parameter called <strong>by_class</strong> that is set to False. If you change this parameter to <strong>True</strong> it will count per class instead.

```
# Run yolov4 model while counting objects per class
python detect.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --images ./data/images/image.jpg --count
```
Running the above command will count the number of objects detected per class and output it to your command prompt or shell as well as on the saved detection as so:
<p align="center"><img src="data/helpers/perclass_count.png" width="640"\></p>

<strong>Note:</strong> You can add the --count flag to detect_video.py commands as well!

<a name="info"/>

```
# Run Face Mask Detection
python detect.py --weights ./checkpoints/custom-416 --size 416 --model yolov4 --images ./data/images/image.jpg --plate
``
## Running Face Mask Detection with detect_video.py is done with the following command.
```
python detect_video.py --weights ./checkpoints/custom-416 --size 416 --model yolov4 --video ./data/video/<input_path>.mp4 --output ./detections/<output>.avi --plate
```

## Command Line Args Reference

```bash

detect.py:
  --images: path to input images as a string with images separated by ","
    (default: './data/images/kite.jpg')
  --output: path to output folder
    (default: './detections/')
  --[no]tiny: yolov4 or yolov4-tiny
    (default: 'False')
  --weights: path to weights file
    (default: './checkpoints/yolov4-416')
  --framework: what framework to use (tf, trt, tflite)
    (default: tf)
  --model: yolov3 or yolov4
    (default: yolov4)
  --size: resize images to
    (default: 416)
  --iou: iou threshold
    (default: 0.45)
  --score: confidence threshold
    (default: 0.25)
  --count: count objects within images
    (default: False)
  --dont_show: dont show image output
    (default: False)
  --info: print info on detections
    (default: False)
  --crop: crop detections and save as new images
    (default: False)
    
detect_video.py:
  --video: path to input video (use 0 for webcam)
    (default: './data/video/video.mp4')
  --output: path to output video (remember to set right codec for given format. e.g. XVID for .avi)
    (default: None)
  --output_format: codec used in VideoWriter when saving video to file
    (default: 'XVID)
  --[no]tiny: yolov4 or yolov4-tiny
    (default: 'false')
  --weights: path to weights file
    (default: './checkpoints/yolov4-416')
  --framework: what framework to use (tf, trt, tflite)
    (default: tf)
  --model: yolov3 or yolov4
    (default: yolov4)
  --size: resize images to
    (default: 416)
  --iou: iou threshold
    (default: 0.45)
  --score: confidence threshold
    (default: 0.25)
  --count: count objects within video
    (default: False)
  --dont_show: dont show video output
    (default: False)
  --info: print info on detections
    (default: False)
  --crop: crop detections and save as new images
    (default: False)
```

### References  

   Huge shoutout goes to theAIGuysCode for creating the backbone of this repository:
  * [yolov4-custom-functions](https://github.com/theAIGuysCode/yolov4-custom-functions)
