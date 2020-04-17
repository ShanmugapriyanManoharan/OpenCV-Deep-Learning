# Object Detection Document

# 1 Requirements

Download the tensorflow model:
```
https://github.com/tensorflow/models
```

Download thepre-trained model(in this case,fasterrcnninceptionv2coco):
```
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
```
Copy the unzip folder of this repository and paste it into the models/research/ob-jectdetection

Download the repositoryHow To Train an Object Detection Classifierfor Multiple Objects Using TensorFlow (GPU) on Windows 10:
```
https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10
```
Copy the content of this repository and paste it into the models/research/objectdetection

# 2 Anaconda Environment Setup

Create a new environment:
```
conda create -n shanjana pip python=3.7
```

Activate the environment:
```
conda activate shanjana
```

Install the git:
```
conda install git
```

Update the pip:
```
python -m pip install –upgrade pip
```

Install tensorflow-gpu:
```
pip install tensorflow-gpu==1.14.0
or
conda install tensorflow-gpu==1.14.0
```

Install other required packages using conda and pip:
```
conda install -c anaconda protobuf
pip install pillow
pip install lxml
pip install Cython
pip install contextlib2
pip install jupyter
pip install matplotlib
pip install pandas
pip install opencv-python
```

Install ipykernel:
```
conda install -c anaconda ipykernel
```

Create Jupyter Kernel:
```
python -m ipykernel install -–user -–name shanjana –-display-name ”Tensorflow-GPU=1.14”
```

# 3 Setting up the environment variable for PYTHON-PATH

A PYTHONPATH variable must be created that points to the\models,\models\research,and\models\research\slim directories.

```
set PYTHONPATH = ~\ObjectDetection\models;
~\ObjectDetection\models\research;
~\ObjectDetection\models\research\slim
```

Note:Every time the ”shanjana” virtual environment is exited, the PYTHON-PATH  variable  is  reset  and  needs  to  be  set  up  again.
You  can  use  
```
echo%PYTHONPATH%
```
to see if it has been set or not.

# 4 Compiling the Protobufs

Change the directory: ~\ObjectDetection\models\research

Copy and paste the following command into the command line and press Enter:

```
protoc –pythonout=..\objectdetection\protos\anchorgenerator.proto
.\objectdetection\protos\argmaxmatcher.proto
.\objectdetection\protos\bipartitematcher.proto
.\objectdetection\protos\boxcoder.proto
.\objectdetection\protos\boxpredictor.proto
.\objectdetection\protos\eval.proto
.\objectdetection\protos\fasterrcnn.proto
.\objectdetection\protos\fasterrcnnboxcoder.proto
.\objectdetection\protos\gridanchorgenerator.proto
.\objectdetection\protos\hyperparams.proto
.\objectdetection\protos\imageresizer.proto
.\objectdetection\protos\inputreader.proto
.\objectdetection\protos\losses.proto
.\objectdetection\protos\matcher.proto
.\objectdetection\protos\meanstddevboxcoder.proto
.\objectdetection\protos\model.proto
.\objectdetection\protos\optimizer.proto
.\objectdetection\protos\pipeline.proto
.\objectdetection\protos\postprocessing.proto
.\objectdetection\protos\preprocessor.proto
.\objectdetection\protos\regionsimilaritycalculator.proto
.\objectdetection\protos\squareboxcoder.proto
.\objectdetection\protos\ssd.proto
.\objectdetection\protos\ssdanchorgenerator.proto
.\objectdetection\protos\stringintlabelmap.proto
.\objectdetection\protos\train.proto
.\objectdetection\protos\keypointboxcoder.proto
.\objectdetection\protos\multiscaleanchorgenerator.proto
.\objectdetection\protos\graphrewriter.proto
.\objectdetection\protos\calibration.proto
.\objectdetection\protos\flexiblegridanchorgenerator.proto
```
This creates a namepb2.py file from every name.proto file in the\objectdetection\protosfolder.

```
python setup.py build
python setup.py install
```

# 5 Verify the tensorflow setup

```
C:\ObjectDetection\models\research\objectdetection>jupyter notebook objectdetectiontutorial.ipynb
```

Note:If the images are not displayed in the jupyter notebook.
Then commentout the below lines will allow the images to be shown in the jupyter notebook:in utils ->visualizationutils.py
```
import matplotlib #matplotlib.use(’Agg’) # pylint: disable=multiple-statements
import matplotlib.pyplot as plt # pylint:  disable=g-import-not-at-top
```

# 6 Gather and Label Pictures
Gather all the available images and place 20% of them to the ~\objectdetection\images\testdirectory,
and 80% of them to the ~\objectdetection\images\train directory.

For labelling the Image, Install LabelImg and label images:
```
pip install LabelImg
```

# 7  Training Data Generation

From the\objectdetection folder:
```
python xml_to_csv.py
```
This creates a train_labels.csv and test_labels.csv file in the\objectdetection\images folder.

To generate the TF records:  open the generatetfrecord.py file in a text editorand replace the label map.
```
#Do the required labelmap:
def class_text_to_int(row_label):
    if row_label == 'CustomObjectname':
        return 1
    else:
        None
```

Then, generate the TFRecord files by issuing these commands from the\objectdetection folder:
```
python generate_tfrecord.py --csv_input=images\train_labels.csv --image_dir=images\train --output_path=train.record
python generate_tfrecord.py --csv_input=images\test_labels.csv --image_dir=images\test --output_path=test.record
```

# 8 Label  Map  Creation  and  Training  Configu-ration

From ~\objectdetection\training directory, open the labelmap.pbtxt:
```
item {
  id: 1
  name: 'Insulator'
}
```

Copy the fasterrcnninceptionv2pets.config from the \objectdetection\samples\configs directory and paste it into \objectdetection\training directory.

Make the below listed changes:

```
numclasses = 1
finetunecheckpoint:
~/ObjectDetection/models/research/objectdetection/fasterrcnninceptionv2coco20180128/model.ckpt
In the train_input_reader section, change input_path and labelmap_path to:
input_path : ”~/ObjectDetection/models/research/objectdetection/train.record”
labelmap_path: ”~/ObjectDetection/models/research/objectdetection/training/labelmap.pbtxt”
Change num_examples to the number of images you have in the\images\testdirectory.
numexamples = 71
In the eval_input_reader section, change input_path and labelmap_path to:
input_path : ”~/ObjectDetection/models/research/objectdetection/test.record”
labelmap_path: ”~/ObjectDetection/models/research/objectdetection/training/labelmap.pbtxt”
```

# 9 Training the model

Copy  the  train.py  file  from \objectdetection\legacy  folder  and  paste  it  into the \objectdetection directory.

From  the \objectdetection  directory,  issue  the  following  command  to  begin training:

```
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/faster_rcnn_inception_v2_pets.config
```

Training as to go on till the loss drops below 0.05 and becomes stable and themodel will save after every 1000 steps or so.

To monitor the training using tensorboard, follow this command in new com-mand windows (from\models\research\objectdetection directory):

```
tensorboard -–logdir=training
```

For example:  https:\\localhost\8008 to paste and enter in the web browser.

# 10 Export  the  Inference  Graph  and  Test  the model

From the \objectdetection directory:
```
python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-XXXX --output_directory inference_graph
```

Note: Replace XXXX with the model saved in the \objectdetection\training directory.

Finally, run any of the below to test the model:

```
object_detection_image.py
object_detection_video.py
object_detection_webcam.py
```

