# sport-ball-classifier


A classification model classify between 7 different sport balls using Resnet-18

 ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/557c9f92-3d3d-413f-849e-7e75ba939943)

 # How it works?
 
 creating a classifier to distinguish 7 sport balls with ResNet-18 and Jetson Inference, the algorithm includes steps like collecting data, training the model, and using it to classify images.

## How to do this??
You must setup your jetson-nano first,you can see the tutorial here:
https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#setup-headless

Steps to run :
1. You have to install jetson-inteference and Docker from https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md
 
  2.run the training script and Change directories into jetson-inference/python/training/classification/data
  
  3.Run this command:
  wget https://nvidia.box.com/shared/static/o577zd8yp3lmxf5zhm38svrbrv45am3y.gz -O cat_dog.tar.gz
     ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/4aedaf3c-04c7-4a63-a3d2-ae8f30ec6a55)
 
  4.Run this command to unzip the file you downloaded.
      tar xvzf cat_dog.tar.gz
      ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/5cd726ce-b338-4219-82ca-80d38435f37f)
 
  
  5.cd back to nvidia/jetson-inference/
  
   
  6.To prevent potential memory errors later on, ensure your system can allocate more memory for tasks by running this command in your terminal while    in the jetson-inference directory.
     echo 1 | sudo tee /proc/sys/vm/overcommit_memory
  
  7. After completing the previous step in the jetson-inference folder, execute ./docker/run.sh to start the docker container. You may need to re-  
      enter your NVIDIA password during this process.
     ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/aa59c330-baf4-41d9-9c90-a6a3068f63df)
 
  
  9. From inside the Docker container, change directories so you are in jetson-inference/python/training/classification
     ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/25954928-480b-47f3-b8d8-e57dd6a32e1e)
 
  
  11. To train the network using the training script, specify the --model-dir where the model should be saved and the path to your data directory.    
      Here’s an example command with additional options for batch size, workers, and epochs:
  
      python3 train.py --model-dir=models/sportballs data/sportballs --batch-size=32 --workers=4 --epochs=50
 
      Explanation of the options:
 
 
       --model-dir=models/cat_dog: Specifies the directory where the trained model will be saved.
     
 
      --batch-size=32: Sets the number of samples in each batch during training. 
     
  
      --workers=4: Number of worker processes to use for data loading during training. 
   
      --epochs=50: Number of complete passes through the training dataset.
 ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/2722b084-c10a-43df-88f1-f0d0e13d247e)
 While it's running, you can stop it anytime with Ctrl+C. You can also restart training later using the --resume and --epoch-start flags, allowing you to test the model without waiting for training to finish.
    
 Additional Information:
 
 Run python3 train.py --help for details on available options, including different networks you can experiment with using the --arch flag.
 
 If you haven't adjusted memory settings and encounter out-of-memory errors, you can enable overcommitting memory by running this command in your terminal:
 echo 1 | sudo tee /proc/sys/vm/overcommit_memory
 This allows your system to allocate more memory for tasks, potentially resolving memory-related issues during execution.
 
  12.Make sure you are in the docker container and in jetson-inference/python/training/classification
  13.Run the onnx export script.
  python3 onnx_export.py --model-dir=models/sportballs
  14.Look in the jetson-inference/python/training/classification/models/sportballs folder to see if there is a new model called resnet18.onnx there.   That is your re-trained model!
  ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/ec2f40dd-eb21-42a9-9761-94c146b32709)
 
  Our Next Step Is processing images!
  To test how your network performs on images, you can use ImageNet command line arguments.
  15.Exit the docker container by pressing Ctl + D.
  16.On your nano, navigate to the jetson-inference/python/training/classification directory.
  17.Use ls models/sportballs/ to make sure that the model is on the nano. You should see a file called resnet18.onnx.
  ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/985a01cb-88fe-4a67-b876-1bd88fe301bc)
  18.Set the NET and DATASET variables:
 NET=models/sportballs
 DATASET=data/sportballs
  19.Run this command to see how it operates on an image from the cat folder.For example we want to classify football
  imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/football/football_119.jpg football.jpg
  19.Open VS Code to view the image output
  ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/e30c1cd8-3c59-434b-9869-1478b9fde7a9)
 
 
 
 ![image](https://github.com/amannx26/sport-balls-detection/assets/173274284/423dd2bf-e48b-4766-98bc-94137d54de73)




If you have any problem you may watch this tutorial
https://www.youtube.com/watch?v=sN6aT9TpltU&t=1159s








