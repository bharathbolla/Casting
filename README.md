# CHANNEL PRUNING USING INVERTED ARCHITECTURE

### This paper was presented in ICCR-2021 [ICCR 2021  - Efficient Deep Learning.pdf](https://github.com/sabeesh90/Channel_Pruning-Casting_Detetction/files/7783093/ICCR.2021.-.Efficient.Deep.Learning.pdf)

#### Authors - Mohan Kingom, Bharath Kumar Bolla, Sabeesh E

<img src="https://user-images.githubusercontent.com/48343095/147536928-e3a0a0c9-fc56-42bc-b123-32595d3f8c32.png" width="500"  height = "750"/>


<h2> Scope of the Paper </h2>
Identifying defective casting products using Deep learning needs to be faster and more robust as this is critical in a factory setting where 1000s of products are passed through the conveyor belt. Here we have revisited techniques that shall aid speeding a deep learning model and make them lighter for deployment on low computing devices. Custom and Transfer learning models have been used and evaluated using accuracy, F1 scores and latency of prediction on a CPU. <br>

- Reducing model size using custom architectures <br>
- Will data augmentation help in this scenario?<br>

<h2> Channel Pruning  - Tapering Network </h2>
The concept of channel pruning has been implemented here where in there is a sequential reduction in the number of channels. Though this is contrary to conventional deeplearning architectures, the authors have leveraged on the fact that sufficient features are learnt during the initial convolutions as they are passed through "multiple similar convolution" layers and then the networks is gradually condensed as they approach the softmax layer. A trade off exists between the loss of information / accuracy and the "depth of tapering'. The more the network is tapered there is more loss of information. Hence an ideal depth is to be identified at which there is no significant loss of information. This varies with every architecture and dataset the neural networks are trained on.

Custom Architectures|Transfer learning architectures
:-------------------------:|:-------------------------:
![image](https://user-images.githubusercontent.com/48343095/147533782-92bb9360-a509-4490-b024-08ee48198f38.png) | ![image](https://user-images.githubusercontent.com/48343095/147533793-12f4d26f-b62e-4c26-a999-06c640468180.png)

<h2> Architectures </h2>
The model architecture is shown below.

Custom Architectures|Transfer learning architectures
:-------------------------:|:-------------------------:
![image](https://user-images.githubusercontent.com/48343095/147533950-000d3075-800e-4653-8b37-ed81362862ed.png)| ![image](https://user-images.githubusercontent.com/48343095/147533959-087b783a-4246-4db2-b2ac-8de3069cc540.png)

Custom models have the highest accuracy with the lowest inference times. This is in spite of the "tapering" network the model has been trained using, hence confirming our hypothesis that "Channel pruning may yet be an effective way to reach peak accuracies if pruned  judiciously"

<h2> Effect on Accuracy </h2>
<img src="https://user-images.githubusercontent.com/48343095/147534955-c7b23c63-e511-4109-9c7a-10be30596ebb.png" width="700"  height = "250"/>

<h2> Inference Times </h2>
<img src="https://user-images.githubusercontent.com/48343095/147534984-bcc979e0-4f4b-45a6-9ba0-a688134fa133.png" width="700"  height = "300"/>

From the images below it is seen that Resnet performs 9 times slower than the custom architecture followed by Nasnet and MobileNet. This can be attributed to the number of training parameters in the neural network.

inf time on varying test size|inf time on varying test size - ratio
:-------------------------:|:-------------------------:
![image](https://user-images.githubusercontent.com/48343095/147535550-002889a8-69c7-4062-a404-376a6a95c4e2.png) | ![image](https://user-images.githubusercontent.com/48343095/147535569-18a374fa-731b-4f24-9e5e-532950f9b1cf.png)

<h2> Model Size / F1 score analysis </h2>
The same is evident from the model size and parameter ratio, as seen below where transfer learning architectures have nearly 4000x times more parameters and 1000x times bigger than a custom model.

Model Size| F1 scores
:-------------------------:|:-------------------------:
![image](https://user-images.githubusercontent.com/48343095/147535703-143768c9-dce0-4aa3-a249-a420a99826a9.png) | ![image](https://user-images.githubusercontent.com/48343095/147535711-88fb2e9e-2880-4d9f-a764-016fcc336685.png)


<h2> Effect of Augmentation </h2>
Also it is seen that , augmentation plays a deterious effect both on the normal and the augmented test dataset in terms of F1 scores. This can be attributed to the fact that, as in our case "specificty is more important", any alterations in the input image will result in mis-classifications as a "NORMAL PIECE WOULD APPEAR DEFECTIVE DUE TO THE EFFECT OF AUGMENTATIONS AND WILL ULTIMATELY RESULT IN THE MODEL MISCLASSIFIYING IT AS DEFECTIVE".  

Effect of Augmentations|
:-------------------------:|
![image](https://user-images.githubusercontent.com/48343095/147536513-cd9541d2-82bb-4630-a005-af44129748f0.png)




