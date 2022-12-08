
# Tensorflow add-on summary box

## Introduction
Add-on implementation for Tensorflow object detection. **Summary table** will be displayed at the right top corner of the inference image. Also, this add-on enable to save details of detection data (class, score(%), xmin, ymin, xmax, ymax) in csv format on the inference run. The fontsize can either be assigned manually in the code ([visualization_utils.py](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/visualization_utils.py#L47-L50)) or adjusted automatically based on the screen width (see line :[1128](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/visualization_utils.py#L1128)). This add-on will be useful to capture the summarized overview of the object detection at a glance. 😼
![](screenshot.png)</br>

## How to Apply

1. After cloning this repo, replace the following files.
- models/research/object_detection/utils/visualization_utils.py
- models/research/object_detection/Object_detection_image_tf2.py

2. install & reload dependencies
```bash
pip install tabulate=0.9.0
```
```bash
cd models/research/
```
```bash
python -m pip install .
```

## How to run
Configure [Object_detection_image_tf2.py](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/Object_detection_image_tf2.py) file before run.
```python
# IMAGE_NAME
IMAGE_NAME = ‘targe_image1.jpg'
# IMAGE_SAVE_NAME
IMAGE_SAVE_NAME = 'targe_image1_result'

# Path to frozen detection graph .pb file, which contains the model that is used
# for object detection.
PATH_TO_PB = '/PATH/TO/BE/CONFIGURED/PB_folder/saved_model'
# Path to label map file
PATH_TO_LABELS = '/PATH/TO/BE/CONFIGURED/labelmap.pbtxt'
# Path to image
PATH_TO_IMAGE = os.path.join(CWD_PATH,'test_images',IMAGE_NAME)

# Number of classes the object detector can identify
NUM_CLASSES = 20
```

Run [Object_detection_image_tf2.py](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/Object_detection_image_tf2.py) under models/research/object_detection/ 
```bash
python Object_detection_image_tf2.py
```
If you want to specify GPU
```bash
export CUDA_VISIBLE_DEVICES=0 && python Object_detection_image_tf2.py
```

## If you want to adjust the table format
Edit header at [Line:1140](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/visualization_utils.py#L1140)
```python
  headers=["Class              ", "total%", "  Qty  "]
```
Or edit multiplier of auto fontsize
```python
    Summary_FontSIZE = int(im_width * 0.02)
```

## if you want to change font color and size
Edit values at [Line:47~50](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/visualization_utils.py#L47-L50) of [visualization_utils.py](https://github.com/boguss1225/tensorflow-summary-box-addon/blob/main/visualization_utils.py)
```python
# Set config for summary box (HM)
FontSIZE = 10
Auto_Fontsize=True
Summary_FontSIZE = 20
FontColor = 'white'
```

## Debug
- If font size is not working, that might be case matter.. "a"rial
```python
# use whatever works
font = ImageFont.truetype('Arial.ttf', Summary_FontSIZE)
font = ImageFont.truetype(‘arial.ttf', Summary_FontSIZE)
```

## Reference
- https://pypi.org/project/tabulate/
- Tensorflow base: https://github.com/tensorflow/models/tree/master/research/object_detection

