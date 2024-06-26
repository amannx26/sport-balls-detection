# sport-ball-classifier


A classification model classify between 7 different sport balls using Resnet-18

 ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/557c9f92-3d3d-413f-849e-7e75ba939943)

 # How it works?
 creating a classifier to distinguish 7 sport balls with ResNet-18 and Jetson Inference, the algorithm includes steps like collecting data, training the model, and using it to classify images.

 ## How to do this??
Steps to run :  
 1. You have to install jetson inteference and Docker from https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md
 2.run the training script and Change directories into jetson-inference/python/training/classification/data
 3.Run this command to download the dataset
   wget https://nvidia.box.com/shared/static/o577zd8yp3lmxf5zhm38svrbrv45am3y.gz -O cat_dog.tar.gz
 4.Run this command to unzip the file you downloaded.
   tar xvzf cat_dog.tar.gz
 5.cd back to nvidia/jetson-inference/
 6.To prevent potential memory errors later on, ensure your system can allocate more memory for tasks by running this command in your terminal while    in the jetson-inference directory.
   echo 1 | sudo tee /proc/sys/vm/overcommit_memory
 7. After completing the previous step in the jetson-inference folder, execute ./docker/run.sh to start the docker container. You may need to re-  
    enter your NVIDIA password during this process.
 8. From inside the Docker container, change directories so you are in jetson-inference/python/training/classification
 9. To train the network using the training script, specify the --model-dir where the model should be saved and the path to your data directory.    
    Here’s an example command with additional options for batch size, workers, and epochs:
    python3 train.py --model-dir=models/sportballs data/sportballs --batch-size=32 --workers=4 --epochs=50
    Explanation of the options:
    --model-dir=models/cat_dog: Specifies the directory where the trained model will be saved.
    data/cat_dog: Path to the directory containing your training data.
    --batch-size=32: Sets the number of samples in each batch during training. Adjust this based on your system's memory capacity and training 
       dataset size.
    --workers=4: Number of worker processes to use for data loading during training. Increasing this can speed up data processing if your system 
       supports it.
    --epochs=50: Number of complete passes through the training dataset. Adjust based on how many iterations of training you want to perform.

   


You have to install jetson inteference and Docker from https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md

After installing Jetson Inference and Docker as per the provided link, here are the steps to create and set up your GitHub repository for a classification model that distinguishes between 7 different sport balls using ResNet-18: 
.












# Project Name

 Add short description of project here > 

![add image descrition here](direct image link here)

## The Algorithm

Add an explanation of the algorithm and how it works. Make sure to include details about how the code works, what it depends on, and any other relevant info. Add images or other descriptions for your project here. 

## Running this project

1. Add steps for running this project.
2. Make sure to include any required libraries that need to be installed for your project to run.

[View a video explanation here](video link)
