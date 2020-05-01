# Speed Estimation using Optical Flow

# Preprocessing

```
python video_to_frames.py
```
This code will convert the train & test video into frames and store it into the folder.

```
python video_to_frames_and_optical_flow.py
```
This code will convert the flow_train & flow_test video into frames and store it into the folder.

# Training using the Google Colab

1. Zip the 'data' folder and upload to the Google Drive.

2. Open the 'Speedestimation.ipynb' in the google colab.

3. Mount your drive with the google colab.

4. Create a folder named 'output' inside the 'data' folder  -> /data/output/

5. Run the first cell in the 'Speedestimation.ipynb' to get the 'data' folder from
google drive and unzip the 'data' folder.

6. Now training can be started.

7. Output video will be saved in the output folder 
