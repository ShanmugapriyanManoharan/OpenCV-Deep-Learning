# YOLOv2 Custom Dataset

# 1 Detection Using A Pre-Trained Model

```
git clone https://github.com/pjreddie/darknet
cd darknet
make
```

### Downloading the weight:
```
wget https://pjreddie.com/media/files/yolov3.weights
```

### Run the detector:
```
./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg
```

# 2 Labelling the Dataset

Note:  The image format should be in .jpg and not in .PNG

Label the images using LabelImg (in Pascal VOC format)

```
git clone https://github.com/Isabek/XmlToTxt.git
```

Place the XML file into the XML folder and run the below command:

```
python xmltotxt.py -xml xml -out out
```
the output will be saved in the OUT folder

or

Label the images using LabelImg (in YOLO and not in Pascal VOC format)

Run the below code to separate the train and test data
```
import glob, os


dataset_path = 'AnnotatedImages'

# Percentage of images to be used for the test set
percentage_test = 20;

# Create and/or truncate train.txt and test.txt
file_train = open('train.txt', 'w')  
file_test = open('test.txt', 'w')

# Populate train.txt and test.txt
counter = 1  
index_test = round(100 / percentage_test)
#print(index_test)
for pathAndFilename in glob.iglob(os.path.join(dataset_path, "*.jpg")):  
    title, ext = os.path.splitext(os.path.basename(pathAndFilename))
   
    if counter == index_test+1:
        counter = 1
        file_test.write(dataset_path + "/" + title + '.jpg' + "\n")
    else:
        file_train.write(dataset_path + "/" + title + '.jpg' + "\n")
        counter = counter + 1
```

# 3 Configuration

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

Open cfg/yolov3.cfg:

```
Line 6:  set batch=24 #this means we will be using 24 images for every trainingstep
Line  7:  set  subdivisions=8 #the  batch  will  be  divided  by  8  to  decrease  GPUVRAM requirements
Line 603:  set filters=18 #(classes + 5)*3 in our case filters=18
Line 689:  set filters=18 #(classes + 5)*3 in our case filters=18
Line 776:  set filters=18 #(classes + 5)*3 in our case filters=18
Line 610:  classes = 1
Line 696:  classes = 1
Line 783:  classes = 1
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

# 4 Training

```
./darknet detector train cfg/coco.data cfg/yolov3.cfg darknet53.conv.74 > train.log
```

# 5 Testing

```
./darknet  detector  test  cfg/voc.data  cfg/yolov3.cfg  yolov3_30000.weights  Images/imagefile.jpg -out myfile
```

For running a video:
```
./darknet detector demo cfg/coco.data cfg/yolov3.cfg yolov3_30000.weights <video file>
```