## Project Name
Classifying Images Based on Healthy and Unhealthy Skin

This project classifies images based on healthy and unhealthy skin. In a world where many of us may worry about conctracting new illnesses or our friends and family who may have those illnesses, this project serves as a great way to detect if someone may or may not be healthy by observing a certain part of the body: the skin. This project has real-life applications, as it can be an idea used in medical places of work and can be done from a safe distance.


![add image descrition here](direct image link here)



## The Algorithm
The algorithm of sorting healthy and unhealthy skin works by first being trained by being shown a series of images that are healthy and unhealthy. Through the resnet tool, AI learns certain features of healthy and unhealthy skin, like a series of bumps that the unhealthy skin photos would have. After the AI knows what images are healthy and unhealthy skin, the AI is shown a new set of images, labels them "healthy" or "unhealthy" from their pre-trained knowledge, and exports them to "healthy" and "unhealthy" output folders. Only "healthy" and "unhealthy" were the options for classifying the images, as determined by the categories defined in the labels.txt file in the project folder.


## Running this project

1. Add steps for running this project.
2. Make sure to include any required libraries that need to be installed for your project to run.

0. Make sure that resnet and googlenet have been installed. This can be done by doing this command: sudo apt-get install libpython3-dev python3-numpy, changing to the docker container (from the jetson-inference folder) by doing ./docker/run.sh, changing directories to jetson-inference/tools, and doing then doing this command: ./download-models.sh You should see a menu pop up. Then, make sure that there is a star next to resnet and googlenet. This signifies that resnet and googlenet are downloaded. Also, make sure that PyTorch does not have a star next to it, as it does not need to be downloaded.

1. Create your dataset by collecting photos. You can use a website like "Kaggle" to find some collections of photos. You will need to have 2 categories of photos. When trained, the AI will sort images into the 2 categories. I downloaded photos of skin that corresponded to people that were healthy or unhealthy. So, my two categories were healthy skin and unhealthy skin. Once you have your photos, create a folder for your dataset. I titled mine "newproject." In this folder, create 3 more folders with titles "test", "train" and "val"(validation). Use lowercase letters. In each of these folders, create 1 folder with the name of one of your categories and 1 folder with the name of the other category. Then, cut and paste your images into the 2 folders of the test, train, and val folders. Make sure that you paste the images of category 1 to test, train, and val's category 1 folders and do the same for category 2. For example, my category 1 was "healthy." So, I pasted my "healthy" photos to the test, train, and val "healthy" folders. Note that about 5% of your photos should be pasted into val, about 10% or so in test, and the remaining 85% in train. Also, create a labels.txt file in your dataset folder (which was the one I titled "newproject"). Type the name of 1 category, press enter, then type the name of the other category. Use lowercase letters for the labels.txt file. Turn the dataset folder into a zip file and then upload the file to MediaFire. Click on the folder in MediaFire, and then copy the link address of the file (AKA copy the link of the BLUE download button).

2. Go into your Linux Terminal/PuTTY. Download the dataset by typing wget <insert link address> 

3. Unzip the file. This can be done by typing sudo apt install unzip - Then, type unzip <insert name of dataset folder>

4. Go to the Docker container by first going to the jetson-inference folder. This can be done by doing cd jetson-inference - Then, type ./docker/run.sh

5. Inside the Docker container, change directories. Type cd jetson-inference/python/training/classification - Now, we are in the classification folder. Train the AI with the dataset by doing python3 train.py --model-dir=models/<dataset folder name> data/<dataset folder name>

6. Not changing directories, generate resnet18.onnx to process the images we want to test. This can be done by typing: python3 onnx_export.py --model-dir=models/<dataset folder name>

7. Still not changing directories, set the NET and DATASET variables. Type NET=models/<dataset folder name> - Then, type DATASET=data/<dataset folder name> - These variables will be used in the command to process our images.

8. Make a place for our output files to go. Type $DATASET/test_output_<Name of Category 1> $DATASET/test_output_<Name of Category 2>

9. Test 1 image. Copy the name of an image in the Category 1 folder of your test folder. Type imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/<Name of Category 1>/<Copied Image Name>.jpg <Insert a New Name for Image>.jpg
  
10. Test the rest! Type imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/<Category 1 Name> $DATASET/test_output_<Category 1 Name> - This will test all Category 1 images. 
  
Then, type imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/<Category 2 Name> $DATASET/test_output_<Category 2 Name> - This will test all Category 2 images.
  
11. Look at the results!! One way to see your results is to go to your JetsonNano file explorer. Go to jetson-inference --> python --> training --> classification --> data - You should then see your 2 output folders! Click on each to see how accurate your AI was! On each image, there will be a text box indicating how close the AI believes your image is related to each of your categories. 




[View a video explanation here](video link)
