# MultiMedia_ActionPrediction_Project3

This repository is created as a deliverable for Project 3 for CS-523 course offered in Spring 2017 at University of Illinois at Chicago.

This repository is created as a deliverable for Project 2 for CS-523 course offered in Spring 2017 at University of Illinois at Chicago.

## Project Members:
1. Kruti Sharma
2. Hengbin Li
3. Shreyas Kulkarni

Generative Adversarial Network have an extensive use in generating images, faces etc. The same network has an application in predicting next frame. Here we show the next action prediction using GANs

This project implements a generative adversarial network to predict future frames of video, as detailed in 
["Deep Multi-Scale Video Prediction Beyond Mean Square Error"](https://arxiv.org/abs/1511.05440) by Mathieu, 
Couprie & LeCun. Their official code (using Torch) can be found at: https://github.com/coupriec/VideoPredictionICLR2016. The official code implemented by dyelax (in TensorFlow) can be found at: https://github.com/dyelax/Adversarial_Video_Generation, which shows the prediction of next frames from Ms. Pacman video game dataset.

## Dataset

This repository is trained on sequence of images of human actions like walk, slide, bend etc. The video sets of Human Actions were collected from http://www.wisdom.weizmann.ac.il/~vision/SpaceTimeActions.html. Each of the videos were than converted into frames and saved in respective directory.

The training, testing and clips directory generated for Human Actions Dataset is in the following format:

    Data
      Human Actions
        Train
          daria_bend
            daria_bend_frame0.jpg
            daria_bend_frame1.jpg

            ......
          daria_walk
            daria_walk_frame0.jpg
            daria_walk_frame1.jpg
            ....
           ......
           .....
          ....... 
          lena_skip2
            lena_skip2_frame0.jpg
            lena_skip2_frame1.jpg
            .....

        Test
          daria_bend
            daria_bend_frame0.jpg
            .....

          denis_bend
            denis_bend_fram0.jpg
            ......

        Clips
          0.npz
          1.npz
          .....

        TestClips
          0.npz
          1.npz
          .....

Clips and TestClips are generated by processing the images in Train and Test directories. The training and testing of the network is done on the clips generated. In order to run the repo, please follow the below instructions:

## How to Train/Test:

1. Clone or download the repository on your local machine
2. Copy the entire repository folder and paste it into the root folder of jupyter notebook.
3. If you want to train on the Human Actions Dataset, the videos can be downloaded from http://www.wisdom.weizmann.ac.il/~vision/SpaceTimeActions.html
4. Once the videos are downloaded, run the following command on each of the directory (eg: walk, slide etc.) to convert the videos into frmaes.
                python convert_video_to_jpg.py --v=skip

5. The above command takes an input a folder - containing the videos and generates the frames for each of the videos in respective folder i.e. if skip folder has a video: daria_skip.avi, denis_skip.avi etc, then this python file create folders inside skip as: daria_skip, denis_skip - with each of these folder containing images obtained from the respective videos.
6. Repear Step 4 for all the folder containing videos.
7. Once the frames are generated, transfer all the individual folders into a data/Human_Actions/Train directory. Copy some 20% images frames from Train directory to Test directory.
8. Once the images are generated and present in Train and Test directory (following the same folder structure as shown above), we can run generate_clips.py to process the images into npz file format.

            python generate_clips.py --t=data/Human_Actions/Train/ --c=data/Human_Actions/Clips/ --n=1000

9. The above command will run on Training data set and generate clips (npz) and store in data/Human_Actions/Clips. For now we have given the n=1000 which means it will generate 1000 clips. For a good training and testing, we must generate atleast 100,000+ clips. The same command must run for Test directory as:

            python generate_clips.py --t=data/Human_Actions/Test/ --c=data/Human_Actions/Clips/ --n=1000

10. Once the clips are generated for both Train and Test data set, we can now train the network and simultaneously test. Test runs are done for every 5000 iterations and images are stored in data/Human_Actions/Save/Images/Default/Test with Step_Numbers. We also save the different scaled images - both ground truth and generated at every 1000 iterations in: data/Human_Actions/Save/Images/Default/Step_1000 and so on.

            Train: python main_prediction.py --test_dir=data/Human_Actions/Train --recursions=1 

            Test: python main_prediction.py --test_dir=data/Human_Actions/Test --recursions=1 --test_only

(Note: A Test or Train directory must have some sub-folders inside with each subfolder having atleast 5+ images.)
 
11. There is also a Jupyter Notebook: Project3UI.ipynb that can be used Step-By-Step to perform all the above steps. The jupyter notebook has all the commands in sequence which can be executed first to produce the images from a video, then process the clips and then train and test the network.
12. To run the Jupyter Notebook, configure the Train and Test directories for your dataset under data. All the directories must be placed in Code folder to run any python file.
      

# Results from our Trained and Tested Network :

---------Original:--------------Ground Truth:----------------Generated:-----------

![alt text](https://github.com/skruti10/MultiMedia_ActionPrediction_Project3/blob/master/Code/data/Human_Actions/Save/Images/Default/NewTest_3/Step_0/originalInput_GIF.gif?raw=true)
![alt text](https://github.com/skruti10/MultiMedia_ActionPrediction_Project3/blob/master/Code/data/Human_Actions/Save/Images/Default/NewTest_3/Step_0/ogen_GIF.gif?raw=true)
![alt text](https://github.com/skruti10/MultiMedia_ActionPrediction_Project3/blob/master/Code/data/Human_Actions/Save/Images/Default/NewTest_3/Step_0/ogt_GIF.gif?raw=true)


---------Original:--------------Ground Truth:----------------Generated:-----------

![alt text](https://github.com/skruti10/MultiMedia_ActionPrediction_Project3/blob/master/Code/data/Human_Actions/Save/Images/Default/NewTest_3/Step_0/originalInput_GIF1.gif?raw=true)
![alt text](https://github.com/skruti10/MultiMedia_ActionPrediction_Project3/blob/master/Code/data/Human_Actions/Save/Images/Default/NewTest_3/Step_0/ogen_GIF1.gif?raw=true)
![alt text](https://github.com/skruti10/MultiMedia_ActionPrediction_Project3/blob/master/Code/data/Human_Actions/Save/Images/Default/NewTest_3/Step_0/ogt_GIF1.gif?raw=true)


