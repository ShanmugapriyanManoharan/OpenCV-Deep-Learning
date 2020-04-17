#YOLOv2 Custom Dataset

#1 Detection Using A Pre-Trained Model

```
git clone https://github.com/pjreddie/darknet
cd darknet
make
```

### Downloading the weight:
```
wget https://pjreddie.com/media/files/yolov2.weights
```

### Run the detector:
```
./darknet detect cfg/yolov2.cfg yolov2.weights data/dog.jpg
```

# 2 Labelling the Dataset

Note:  The image format should be in .jpg and not in .PNG

Label the images using LabelImg (with YOLO and not in Pascal VOC format)

Then run the generate.py code to separate the train and test data

Open cfg/voc.data (make the changes):

```
classes= 1
train = train.txt
valid = test.txt
names = data/objectclass.names
backup = backup
```

Create in data/objectclass.names to the class name: CustomObjectname

Create in cfg/objectclass.data to the class name: CustomObjectname

Open cfg/yolov2.cfg:

```
batches:12
subdivision:8
line 234:  filter:  (5 + n) * 3, here n = number of classes, which is 1.  (for yolov2-tiny:  (5 + n) * 5)
So filters =30
classes = 1
```

Open the Makefile:

```
GPU=1
CUDNN=1
```
save the file

```
make
```

#3 Training

```
./darknet detector train cfg/coco.data cfg/yolov2.cfg darknet19\_448.conv.23 > train.log
```

#4 Testing

```
./darknet  detector  test  cfg/voc.data  cfg/yolov2.cfg  yolov270000.weights  Images/imagefile.jpg -out myfile
```

For running a video:
```
./darknet detector demo cfg/coco.data cfg/yolov2.cfg yolov2\_70000.weights <video file>
```