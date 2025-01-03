<div align="fill">
<h1>Strike_Detection_ML</h1>
  
Computer vision project aiming to train a model to recognize 'strikes' in Mixed Martial Arts.

![test_optimized_12345 (online-video-cutter com) (2)](https://github.com/user-attachments/assets/1bbdffa9-a937-4fc6-800c-53141c686507)

<br>

Earlier this year Facebook released its new Segment Anything Model (SAM2) which is a foundational model for solving promptable visual segmentation in images and videos. It excels in workflows that involve detecting discrete objects or parts of objects and creating masks for these parts. Masks are a more precise form of annotating image data which until now have been much more time consuming to create than using bounding boxes or keypoints. Being curious and excited about this new development is what inspired this project to train a model to recognize fighters, strikes/significant strikes and misses in MMA footage.

<br>

![image](https://github.com/user-attachments/assets/357b3784-a254-4954-b6e5-1e0601fd3d60)

<h2>Training</h2>

Initially I wrote a python script to integrate SAM2 into a browswer-based labeling workflow, however this method proved cumbersome and slow. Instead I started using Label-Studio as my annotating platform integrated with a SAM2 backend for labeling and generating masks. These masks were 'pretty good' and while they were faster than manually creating the masks, a lot required manual adjustment so were still time-consuming to create. I had wanted subscribe to Label-Studio Premium which offers automated learning on labeling patterns meaning that after labeling something 3 or 4 times, the backend 'learns' the object being tracked over frames and can generate labels for the rest of the batch. However, Label-Studio hasn't replied to my subscription requests (probably because I'm not a company) yet so I was only able to label 200 frames representing 40 'moments' comprised of 5 frames each.

<br>

<img src="https://github.com/user-attachments/assets/2ed3b636-2aa1-4eab-a9a3-661e62c2af25" alt="vlcsnap-2024-12-21-01h19m41s642-strike-0" width="195"/>
<img src="https://github.com/user-attachments/assets/5bb28f4c-ad38-4f80-b70f-6d2cd0405fee" alt="vlcsnap-2024-12-21-01h19m42s506-strike-0" width="195"/>
<img src="https://github.com/user-attachments/assets/0b98ec3b-b932-4276-a7a4-6b89d0ee5df5" alt="vlcsnap-2024-12-21-01h19m43s309-strike-0" width="195"/>
<img src="https://github.com/user-attachments/assets/c484a10e-addc-4e7a-b502-e7bc300c265f" alt="vlcsnap-2024-12-21-01h19m44s306-strike-0" width="195"/>

<br>

I had planned to [train a model with the 3DCNN architecture](https://github.com/AndreF343/Strike_Detection_ML/blob/main/3DCNN_Pipeline.ipynb) which excels on inferring relationships in spatio-temporal data. However this architecture was too RAM-intensive for my google colab runtime to handle. Additionally, even if I was able to reduce RAM usage by batching the training, I still did not have enough data points to make a difference so instead I decided to feed my dataset to a pre-trained model using the open source CV framework MMAction2. With the MMAction2 framework I was able to supply my data [to the pretrained Temporal Segment Network (TSN) model](https://github.com/AndreF343/Strike_Detection_ML/blob/main/TSN_Pipeline.ipynb) to generate the gifs included in this readme.

<br>

![test_optimized_7 (online-video-cutter com)](https://github.com/user-attachments/assets/e7752d59-dc62-4b78-a4bc-8147caf16d5b)

<br>

<h2>Result</h2>

While the model's accuracy is not production-ready, the accuracy for having only 40 data points was quite impressive. There is clear room for tuning the model's efficiency and parameter configuration, but the ultimate bottle-neck remains the dataset size. If Label-Studio ever does get back to me about using their integrated ML backend solutions, I may revisit this project to improve it's accuracy and expand the number of detectable classes.

Included in this repository are the scripts used to train the [3DCNN model](https://github.com/AndreF343/Strike_Detection_ML/blob/main/3DCNN_Pipeline.ipynb) and the [TSN model](https://github.com/AndreF343/Strike_Detection_ML/blob/main/TSN_Pipeline.ipynb) (higher accuracy) using the MMAction2 framework.

</div>
