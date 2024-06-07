# Crop Disease Identification and Management with Machine Learning
This project involves the development of a mobile application for detecting crop diseases using machine learning. The app utilizes a TensorFlow Lite model for real-time inference, providing farmers with actionable insights to manage crop health effectively.

## Contributors
- Jeffrey Asiedu-Brako : [@ziegler121](https://www.github.com/ziegler121)
- Emmanuel Kyeremeh : [@emmanuelkyeremeh](https://github.com/emmanuelkyeremeh)


## Project Aim and Objectives
- Review literature on similar scholarly publications
- Collect data on diseases affecting tomato and pepper crops
- Train and develop a Machine Learning Model to aid the identification and management of crop diseases
- Build a Mobile App for the Model
- Test the Model


## METHODOLOGY AND IMPLEMENTATION
Every general machine learning task including deep learning has a standardized approach which needs to be followed in order to obtain the best results. This is known as the Machine Learning workflow which is shown below:
![Machine Learning Workflow image](https://drive.google.com/uc?export=view&id=1ZviuEP_vGuBGIhExYLygphSfWbNp1t_W)

### DATA COLLECTION
**Description of Dataset**
The PlantVillage dataset, an openly accessible resource, features a variety of plant disease categories. For this project, we focused on 12 classes relevant to tomato and pepper crops, narrowing down from the original 38 classes and 54,305 images. The dataset was split into training (80%) and validation/testing (20%) subsets to ensure robust model performance.
![Sample images from the PlantVillage Dataset](https://drive.google.com/uc?export=view&id=10XGh64TyRWrzTbSn01QD-EPCK0SpiFiZ)
*Sample images from the PlantVillage Dataset*

## Data Pre-Processing and Augmentation
Color images from the PlantVillage dataset were resized to 224x224 pixels to meet the input requirements of the MobileNetV2 model. Pixel values were rescaled from [0, 255] to [0, 1] to aid neural network training. To prevent overfitting, data augmentation techniques such as random flips, mirror images, and rotations up to 20% were applied. These augmentations were generated on-the-fly during training to enhance model robustness and accuracy in classifying real-world images.

## Model Selection and Design

### Choice of MobileNet-V2
MobileNet-V2 was chosen for its efficiency and suitability for mobile devices. Its design uses depth-wise separable convolutions, reducing computation while maintaining high accuracy.

### Customizing the Top Layers
The top layers were fine-tuned to recognize crop diseases by replacing the original classification head with densely connected layers, tailored for our specific task.

### Hyperparameter Tuning
Key hyperparameters were fine-tuned to optimize performance:
- **Learning Rate:** Adjusted to balance between fast convergence and avoiding divergence.
- **Batch Size:** Selected based on computational resources and dataset characteristics.
- **Optimization Algorithm:** Used Adam for adaptive learning.
- **Early Stopping:** Implemented to prevent overfitting.
- **Learning Rate Schedules:** Applied to help the model converge to a better solution.

The details are listed in the table below:
![Hyperparameter specifications](https://drive.google.com/uc?export=view&id=1zyeDadSd_GdbF-oUyM_C3W-vXNIyIOL-)

A summary of the entire Network Architecture is shown below:
![Model summary](https://drive.google.com/uc?export=view&id=15BBmPYw9INGZD2i8u9Pf77R_eBluQl8n)

## Training and Evaluation

Training and evaluation were conducted on Google Colab, leveraging its cloud-based environment for enhanced computational power. The model was trained over 20 epochs with early stopping to prevent overfitting. By the 20th epoch, the model achieved training and validation accuracies of 93.58% and 91.29%, respectively.
*MOdel Training and Validation Accuracies(left) and Trainng and Validation loss(right) as a function of epoch number*

Additionally, while validation accuracy offers insight into how the model generalizes to unfamiliar data, the ultimate assessment lies in predictions made on unseen data (test data). Graphical depictions of the model’s predictions on a subset of the test data are provided below, accompanied by the model’s confidence score for each prediction.
![Model predictions](https://drive.google.com/uc?export=view&id=130pyPQj6NIJrfLyvihq6Etb4C6TrHoSP)

### Conversion to TensorFlow Lite
After training, the model was converted to TensorFlow Lite for optimal deployment on mobile and edge devices. This conversion preserved accuracy while enhancing performance and memory efficiency.

- **Pruning:** Removed less important connections, reducing model size and accelerating inference without compromising accuracy.
- **Quantization:** Reduced the precision of numerical values, shrinking the model from 8MB to approximately 2.4MB, speeding up inference and reducing memory demands.

![Quantized Model](https://drive.google.com/uc?export=view&id=1QI1i7SySZnmgJ8gdiuaUpPe7fRSInZV5)

### Model Verification
Post-conversion, the model’s accuracy was validated to ensure the optimization procedures did not adversely affect its proficiency in identifying crop diseases. The TensorFlow Lite conversion process resulted in a lightweight yet accurate model suitable for mobile applications.


## Mobile App Deployment
The deployment of the crop disease identification solution culminated in a user-friendly mobile app built using React Native into which the TensorFlow Lite model was integrated. 
![interface](https://drive.google.com/uc?export=view&id=1g5qHpPwDmXyO1uaXyYGREtKADuzw1M_a)
*App User Interface*

### User Interaction and Inference
- Image Upload: Users can upload images of crop leaves directly from their bobile devices
- Real-Time Inference: The TensorFlow Lite model analyzes the image to identify potential diseases.
![inference](https://drive.google.com/uc?export=view&id=1OUkugtCPtTCXfs5UuvzZImNHsU9oo7Qy)
- Prediction Display: Shows detected diseases with confidence levels in clear format
![model predict](https://drive.google.com/uc?export=view&id=1AI7aGpPiYLaiEATqFV34K7Rb5ngvzFjm)
- Guidance and Recommendations: Offers practical steps for disease management and treatment
![recommend](https://drive.google.com/uc?export=view&id=1yOq99VvbRlVW6Zt43fn4kxDlqEzJGptm)
