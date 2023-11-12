# Deep Learning for Aircraft Recognition
A CNN model trained to classify and identify various military aircraft through satellite imagery
https://drive.google.com/drive/folders/1abQQCeZ92jGfF2C1GjnJQW8Mw_Jk9cw2

-------------------------------------------------------------------------------------------------

## Abstract

Today, many military branches around the world are investing in Computer Vision for Intelligence, Surveillance and Reconnaissance (ISR). Some applications related to this field include, recognition of military vehicles in social media [1], recognition of camouflaged military targets [2], and battlefield object detection [3]. Military superpowers such as the United States are investing heavily in AI and Deep Learning, with image recognition as one of the main applications [4]. The main objective of this field is to enhance ISR capabilities. Nowadays, combat and reconnaissance drones are becoming increasingly significant and crucial in modern militaries around the world. One of the crucial elements in UAVs and UCAVs are the imaging capabilities from high altitudes. However, as it stands today, reconnaissance and remote intelligence gathering is still done through satellite imagery. This project focuses on the essentials of how Computer Vision can be used by militaries for ISR purposes.

## Objective

In this project, we use a Convolutional Neural Network to classify a variety of military aircraft through satellite imagery. The project’s aim is to build a Convolutional Neural Network with the capability to distinguish and accurately classify aircraft through a snapshot of satellite imagery.  Additionally, the model should be able to identify and detect all types of aircraft when presented with a large snapshot of an airbase, as well as classifying snapshots of a single aircraft type. Through the use of training data, the model will be accurate  enough to identify individual aircraft in addition to being scalable to a large dataset.

## Design

### **Dataset Description**

We developed a dataset composed of 9 different military aircraft, as well as a dataset for various backgrounds, such as the concrete tarmac of air bases or sandy grounds for certain boneyards and air bases throughout the world. Overall, the dataset is composed of 6,300 images, each being 120 x 120, with each aircraft type containing ~ 610 - 660 images.

The aircraft types included in this dataset are:

![Capture](https://user-images.githubusercontent.com/19809069/115973276-c1de3080-a521-11eb-885a-4bdfdebb1288.JPG)

### **Dataset creation**

Due to the lack of pre-existing publicly accessible datasets on military aircraft, we were forced to create our own through satellite imagery taken by Google Maps. We visited many different air force bases belonging to the United States throughout the world, taking individual snapshots of different types of military aircraft. The specific aircraft belong to the categories shown in the table below. 

![Capture](https://user-images.githubusercontent.com/19809069/115973223-58f6b880-a521-11eb-88ca-bd76ed276f21.JPG)


To account for abstraction, we decided to augment our dataset using the  ImageDataGenerator function provided by Keras. This function allowed us to take 1 image and create (n*) number of images with different rotations, zoom level and horizontal flips of the same original image. For example, the B-2 image shown above can be flipped or rotated into figure 1, shown below. This method of data augmentation ensures that the dataset is balanced and decreases overfitting in the long run. It accounted for differently orientated images of aircraft taken at random positions and zoom levels.

![Capture](https://user-images.githubusercontent.com/19809069/115973235-6d3ab580-a521-11eb-9df6-2494bc57a17a.JPG)

### **Convolutional Neural Network model design**

The model was designed based on two crucial aspects, one being  our relatively small dataset and the second was to minimize cross validation loss as much as possible. To avoid overfitting, a relatively small model with less complexity is crucial given a small dataset size. Our convolutional neural network is composed of the following:

![Capture](https://user-images.githubusercontent.com/19809069/115973253-880d2a00-a521-11eb-8d4a-64df9310180d.JPG)

### **Model summary**

![Capture](https://user-images.githubusercontent.com/19809069/115973258-99563680-a521-11eb-96d1-4c93e491fb84.JPG)


With the help of the hyperparameter tuning  function provided by Keras, we were able to find a model which focused on achieving the highest cross validation accuracy and the lowest cross validation loss value.  The statistics for the model can be seen in Figure 2. The highest cross validation accuracy the model was able to achieve is ~ 91%, with the lowest cross validation accuracy achieved being ~ 0.3322. The training accuracy is ~ 98% and the training loss is ~ 0.0610. The model was compiled with the Adam optimizer with a learning rate of 0.0001 using the sparse categorical cross entropy loss method. The model was fitted with 30 epochs, a batch size of 64 and a validation split of .30.

![Capture](https://user-images.githubusercontent.com/19809069/115973270-aa06ac80-a521-11eb-956f-ac18f40f731e.JPG)

## Results

We tested the model’s practical capabilities by using the predict function on several wide body snapshots of air force bases around the world. This was done in order to test two main capabilities of the model; the model’s ability to successfully identify and detect any type of aircraft, and its ability to identify the category that the detected aircraft belongs to. The model’s ability to detect aircraft can be seen in Figures 4, 5, 6 , 7. Furthermore, the model’s ability to accurately classify an aircraft can be seen in Figures 8, 9, 10, 11. During our testing phase, we noticed that the model tended to misclassify certain types of aircrafts. Taking a deeper look, we realize that the model can often have a hard time distinguishing between aircraft types with a high degree of similarities. For example, The E-3 and C-135 are both extremely similar aircrafts with more or less the same measurements and features. This means that the model needs to be trained to further identify unique characteristics rather than the general shape of the aircraft, which can be common amongst other aircrafts. This can be achieved through a more complex model, given that we expand on our dataset and improve its quality in terms of pixelation, data augmentation and balancing. 

![Capture](https://user-images.githubusercontent.com/19809069/115973342-521c7580-a522-11eb-84fc-b7b7aa8812d5.JPG)

![Capture](https://user-images.githubusercontent.com/19809069/115973333-3b761e80-a522-11eb-8fe2-e1f9fb8f1a58.JPG)

![Capture](https://user-images.githubusercontent.com/19809069/115973316-079af900-a522-11eb-8739-a2370ec4ccb5.JPG)

![Capture](https://user-images.githubusercontent.com/19809069/115973323-1d102300-a522-11eb-9a92-c13b67382829.JPG)

![Capture](https://user-images.githubusercontent.com/19809069/115973330-2b5e3f00-a522-11eb-9ff2-823d32ee25b2.JPG)


## Conclusion

The biggest take away from this experiment is the quality of the dataset and its significant effect on the model’s practical capabilities. Despite reaching a high cross validation accuracy of ~ 91%, the model can be trained to perform much better in both training and a practical setting. As described earlier in the results analysis, possessing a high quality dataset is crucial and beneficial for the model. The biggest improvement that we can make is to expand our dataset to around 15,000 images, 1,500 images for each category. Each category must include a high quality image with varying degrees of rotation, zoom levels and as well cut off points, where only distinguishable features are exposed. These improvements can drastically improve the accuracy of the model by minimizing misclassifications and generalizing to account for noise encountered in practical use.


## References

[1] T. Hiippala, Recognizing Military Vehicles in Social Media Images Using Deep Learning (2017), Proceedings of the 2017 IEEE International Conference on Intelligence and Security Informatics.

[2] A. Khashman, Automatic Detection of Military Targets Utilising Neural Networks and Scale Space Analysis (2000), RTO IST Symposium on “New Information Processing Techniques for Military Systems”.

[3] S. Liu & Z. Liu, Multi-Channel CNN-based Object Detection for Enhanced Situational Awareness (2017), NATO Science and Technology Organisation Proceedings.

[4] RAND Corporation, Military Applications of Artificial Intelligence (2020), RAND Research Reports.

