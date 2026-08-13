🐱🐶 Cat vs Dog Image Classification using PyTorch
📌 Project Overview
This project is an image classification system for classifying images as Cat or Dog using Deep Learning with PyTorch.
The project contains two CNN approaches:
A custom Convolutional Neural Network (CNN)
Transfer Learning using a pretrained MobileNetV2
The final model uses MobileNetV2 with fine-tuning to improve classification performance.
The complete implementation is provided in a Jupyter Notebook.

🎯 Objective
The main objective of this project is to build a deep learning model that can:
Classify an image as Cat or Dog
Train using GPU/CUDA when available
Apply image augmentation during training
Evaluate the model using test data
Calculate training and testing accuracy
Generate a confusion matrix
Predict a single new image
Display prediction confidence
Save and load the trained model

🛠️ Technologies Used
Python
PyTorch
Torchvision
Scikit-learn
NumPy
Pandas
Pillow
Matplotlib
Seaborn
Jupyter Notebook
CUDA

📂 Project Structure
CCN/
│
├── cat_dog_classification.ipynb
├── requirements.txt
├── cat_dog_model.pth
└── README.md

cat_dog_model.pth is the saved PyTorch model file generated after training.

📦 Installation
1. Clone the repository
git clone cat_dog_classification


2. Open the project directory
cd Cat-Dog-Classification

3. Install the required libraries
pip install -r requirements.txt

4. Start Jupyter Notebook
jupyter notebook

Then open:
cat_dog_classification.ipynb


📚 Dataset
The project uses an image dataset containing two classes:
Cat
Dog

The images are loaded using torchvision.datasets.ImageFolder.
The dataset directory should follow this structure:
train/
│
├── cat/
│   ├── image1.jpg
│   ├── image2.jpg
│   └── ...
│
└── dog/
    ├── image1.jpg
    ├── image2.jpg
    └── ...

Important
The original notebook contains a local Windows dataset path.
For example:
C:\Users\...\train

This path will not work on another computer.
You should change the dataset path in the notebook to the location of your dataset.

🖼️ Image Preprocessing
Images are resized to:
224 × 224

Training Augmentation
The training images use:
Resize
Random Horizontal Flip
Random Rotation
Color Jitter
Tensor conversion
ImageNet normalization
Example:
transform_train = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.RandomHorizontalFlip(),
    transforms.RandomRotation(15),
    transforms.ColorJitter(
        brightness=0.3,
        contrast=0.3
    ),
    transforms.ToTensor(),
    transforms.Normalize(
        [0.485, 0.456, 0.406],
        [0.229, 0.224, 0.225]
    )
])

Testing
Testing images do not use augmentation.
Only resizing, tensor conversion, and normalization are applied.
This prevents random transformations from affecting evaluation.

✂️ Train/Test Split
The dataset is divided into:
80% → Training
20% → Testing

A stratified split is used so that the Cat/Dog class distribution is maintained between training and testing datasets.
train_idx, test_idx = train_test_split(
    range(len(labels)),🐱🐶 Cat vs Dog Image Classification using PyTorch
📌 Project Overview
This project is an image classification system for classifying images as Cat or Dog using Deep Learning with PyTorch.
The project contains two CNN approaches:
A custom Convolutional Neural Network (CNN)
Transfer Learning using a pretrained MobileNetV2
The final model uses MobileNetV2 with fine-tuning to improve classification performance.
The complete implementation is provided in a Jupyter Notebook.

🎯 Objective
The main objective of this project is to build a deep learning model that can:
Classify an image as Cat or Dog
Train using GPU/CUDA when available
Apply image augmentation during training
Evaluate the model using test data
Calculate training and testing accuracy
Generate a confusion matrix
Predict a single new image
Display prediction confidence
Save and load the trained model

🛠️ Technologies Used
Python
PyTorch
Torchvision
Scikit-learn
NumPy
Pandas
Pillow
Matplotlib
Seaborn
Jupyter Notebook
CUDA

📂 Project Structure
Cat-Dog-Classification/
│
├── cat_dog_classification.ipynb
├── requirements.txt
├── cat_dog_model.pth
└── README.md

cat_dog_model.pth is the saved PyTorch model file generated after training.

📦 Installation
1. Clone the repository
git clone YOUR_GITHUB_REPOSITORY_URL

2. Open the project directory
cd Cat-Dog-Classification

3. Install the required libraries
pip install -r requirements.txt

4. Start Jupyter Notebook
jupyter notebook

Then open:
cat_dog_classification.ipynb


📚 Dataset
The project uses an image dataset containing two classes:
Cat
Dog

The images are loaded using torchvision.datasets.ImageFolder.
The dataset directory should follow this structure:
train/
│
├── cat/
│   ├── image1.jpg
│   ├── image2.jpg
│   └── ...
│
└── dog/
    ├── image1.jpg
    ├── image2.jpg
    └── ...

Important
The original notebook contains a local Windows dataset path.
For example:
C:\Users\...\train

This path will not work on another computer.
You should change the dataset path in the notebook to the location of your dataset.

🖼️ Image Preprocessing
Images are resized to:
224 × 224

Training Augmentation
The training images use:
Resize
Random Horizontal Flip
Random Rotation
Color Jitter
Tensor conversion
ImageNet normalization
Example:
transform_train = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.RandomHorizontalFlip(),
    transforms.RandomRotation(15),
    transforms.ColorJitter(
        brightness=0.3,
        contrast=0.3
    ),
    transforms.ToTensor(),
    transforms.Normalize(
        [0.485, 0.456, 0.406],
        [0.229, 0.224, 0.225]
    )
])

Testing
Testing images do not use augmentation.
Only resizing, tensor conversion, and normalization are applied.
This prevents random transformations from affecting evaluation.

✂️ Train/Test Split
The dataset is divided into:
80% → Training
20% → Testing

A stratified split is used so that the Cat/Dog class distribution is maintained between training and testing datasets.
train_idx, test_idx = train_test_split(
    range(len(labels)),
    test_size=0.2,
    stratify=labels,
    random_state=42
)


🧠 Model 1: Custom CNN
The project first implements a custom CNN architecture.
The network contains four convolutional blocks:
Input Image
     ↓
Block 1
     ↓
Block 2
     ↓
Block 3
     ↓
Block 4
     ↓
Global Average Pooling
     ↓
Linear Classifier
     ↓
Cat / Dog

The CNN uses:
Convolutional layers
Batch Normalization
ReLU activation
Max Pooling
Dropout
Adaptive Average Pooling
Fully Connected Layer
The final classifier produces two outputs:
0 → Cat
1 → Dog


🚀 Model 2: Transfer Learning with MobileNetV2
The project also uses a pretrained MobileNetV2 model from Torchvision.
model = models.mobilenet_v2(pretrained=True)

Most of the pretrained layers are frozen:
for param in model.parameters():
    param.requires_grad = False

The last feature layers are unfrozen for fine-tuning.
A new classifier is added for the two classes:
Cat
Dog

The classifier architecture is:
MobileNetV2 Features
        ↓
     Dropout
        ↓
   Linear Layer
        ↓
      ReLU
        ↓
     Dropout
        ↓
   Linear Layer
        ↓
    Cat / Dog


⚙️ Training
The model is trained using:
Loss Function
nn.CrossEntropyLoss()

Optimizer
Adam

with:
Learning Rate = 0.0001
Weight Decay  = 0.0001

Epochs
50

Batch Size
32


📉 Learning Rate Scheduler
The project uses:
ReduceLROnPlateau

The learning rate is reduced when the training loss stops improving.

🖥️ GPU / CUDA
The notebook checks whether CUDA is available:
device = torch.device(
    "cuda" if torch.cuda.is_available() else "cpu"
)

The model and input images are moved to the GPU:
model = model.to(device)

images = images.to(device)
labels = labels.to(device)

GPU Requirement
The notebook currently requires a CUDA-compatible NVIDIA GPU because it contains:
if not torch.cuda.is_available():
    raise RuntimeError("CUDA GPU not found!")

If you want the notebook to also work on CPU, remove this check and use the automatic device selection.

📊 Model Evaluation
The model is evaluated using the test dataset.
The project calculates:
Test Loss
Test Accuracy
Training Accuracy
Example output:
Test Loss: X.XXXX
Test Accuracy: XX.XX%
Train Accuracy: XX.XX%


🔍 Single Image Prediction
The trained model can classify an individual image.
The image is:
Loaded using Pillow
Converted to RGB
Resized to 224 × 224
Normalized
Sent to the GPU
Passed through the model
The model returns:
Cat confidence
Dog confidence
Prediction

Example:
Cat confidence: 95.32%
Dog confidence: 4.68%

Prediction: Cat


📈 Confusion Matrix
The project generates a confusion matrix using Scikit-learn.
The matrix contains:
                Predicted
              Cat       Dog

Actual Cat     TP        FN

Actual Dog     FP        TN

The confusion matrix helps visualize which images were correctly and incorrectly classified.
The notebook uses:
Matplotlib
Seaborn
Scikit-learn
to create the visualization.

💾 Saving the Model
After training, the model weights are saved using:
torch.save(
    model.state_dict(),
    "cat_dog_model.pth"
)

The saved model file is:
cat_dog_model.pth


🔄 Loading the Model
The saved weights can be loaded later:
model = cat_dog_classifation(num_class=2)

model.load_state_dict(
    torch.load("cat_dog_model.pth")
)

model.eval()

Make sure that the architecture used when loading the weights matches the architecture used when the weights were saved.

⚠️ Important Note About the Saved Model
The notebook trains two different models:
Custom CNN
MobileNetV2
If you save the MobileNetV2 model:
torch.save(model.state_dict(), "cat_dog_model.pth")

you should load it using the MobileNetV2 architecture, not the custom cat_dog_classifation architecture.
For example:
model = models.mobilenet_v2(weights=None)

model.classifier = nn.Sequential(
    nn.Dropout(0.3),
    nn.Linear(model.last_channel, 256),
    nn.ReLU(),
    nn.Dropout(0.2),
    nn.Linear(256, 2)
)

model.load_state_dict(
    torch.load("cat_dog_model.pth")
)

model.eval()


📁 Requirements
The required Python libraries are listed in:
requirements.txt

Install them using:
pip install -r requirements.txt


🔮 Future Improvements
Possible improvements include:
Add more training images
Use a larger dataset
Add validation data
Implement early stopping
Save the best model based on validation accuracy
Add precision, recall and F1-score
Try ResNet or EfficientNet
Create a Streamlit web application
Deploy the model as an API
Add real-time webcam prediction


👨‍💻 Author
Surya Prakash Nayak

⭐ Project
If you find this project useful, consider giving the repository a ⭐ on GitHub.

    test_size=0.2,
    stratify=labels,
    random_state=42
)


🧠 Model 1: Custom CNN
The project first implements a custom CNN architecture.
The network contains four convolutional blocks:
Input Image
     ↓
Block 1
     ↓
Block 2
     ↓
Block 3
     ↓
Block 4
     ↓
Global Average Pooling
     ↓
Linear Classifier
     ↓
Cat / Dog

The CNN uses:
Convolutional layers
Batch Normalization
ReLU activation
Max Pooling
Dropout
Adaptive Average Pooling
Fully Connected Layer
The final classifier produces two outputs:
0 → Cat
1 → Dog


🚀 Model 2: Transfer Learning with MobileNetV2
The project also uses a pretrained MobileNetV2 model from Torchvision.
model = models.mobilenet_v2(pretrained=True)

Most of the pretrained layers are frozen:
for param in model.parameters():
    param.requires_grad = False

The last feature layers are unfrozen for fine-tuning.
A new classifier is added for the two classes:
Cat
Dog

The classifier architecture is:
MobileNetV2 Features
        ↓
     Dropout
        ↓
   Linear Layer
        ↓
      ReLU
        ↓
     Dropout
        ↓
   Linear Layer
        ↓
    Cat / Dog


⚙️ Training
The model is trained using:
Loss Function
nn.CrossEntropyLoss()

Optimizer
Adam

with:
Learning Rate = 0.0001
Weight Decay  = 0.0001

Epochs
50

Batch Size
32


📉 Learning Rate Scheduler
The project uses:
ReduceLROnPlateau

The learning rate is reduced when the training loss stops improving.

🖥️ GPU / CUDA
The notebook checks whether CUDA is available:
device = torch.device(
    "cuda" if torch.cuda.is_available() else "cpu"
)

The model and input images are moved to the GPU:
model = model.to(device)

images = images.to(device)
labels = labels.to(device)

GPU Requirement
The notebook currently requires a CUDA-compatible NVIDIA GPU because it contains:
if not torch.cuda.is_available():
    raise RuntimeError("CUDA GPU not found!")

If you want the notebook to also work on CPU, remove this check and use the automatic device selection.

📊 Model Evaluation
The model is evaluated using the test dataset.
The project calculates:
Test Loss
Test Accuracy
Training Accuracy
Example output:
Test Loss: X.XXXX
Test Accuracy: XX.XX%
Train Accuracy: XX.XX%


🔍 Single Image Prediction
The trained model can classify an individual image.
The image is:
Loaded using Pillow
Converted to RGB
Resized to 224 × 224
Normalized
Sent to the GPU
Passed through the model
The model returns:
Cat confidence
Dog confidence
Prediction

Example:
Cat confidence: 95.32%
Dog confidence: 4.68%

Prediction: Cat


📈 Confusion Matrix
The project generates a confusion matrix using Scikit-learn.
The matrix contains:
                Predicted
              Cat       Dog

Actual Cat     TP        FN

Actual Dog     FP        TN


The confusion matrix helps visualize which images were correctly and incorrectly classified.
The notebook uses:
Matplotlib
Seaborn
Scikit-learn
to create the visualization.

💾 Saving the Model
After training, the model weights are saved using:
torch.save(
    model.state_dict(),
    "cat_dog_model.pth"
)

The saved model file is:
cat_dog_model.pth


🔄 Loading the Model
The saved weights can be loaded later:
model = cat_dog_classifation(num_class=2)

model.load_state_dict(
    torch.load("cat_dog_model.pth")
)

model.eval()

Make sure that the architecture used when loading the weights matches the architecture used when the weights were saved.

⚠️ Important Note About the Saved Model
The notebook trains two different models:
Custom CNN
MobileNetV2
If you save the MobileNetV2 model:
torch.save(model.state_dict(), "cat_dog_model.pth")

you should load it using the MobileNetV2 architecture, not the custom cat_dog_classifation architecture.
For example:
model = models.mobilenet_v2(weights=None)

model.classifier = nn.Sequential(
    nn.Dropout(0.3),
    nn.Linear(model.last_channel, 256),
    nn.ReLU(),
    nn.Dropout(0.2),
    nn.Linear(256, 2)
)

model.load_state_dict(
    torch.load("cat_dog_model.pth")
)

model.eval()


📁 Requirements
The required Python libraries are listed in:
requirements.txt

Install them using:
pip install -r requirements.txt


🔮 Future Improvements
Possible improvements include:
Add more training images
Use a larger dataset
Add validation data
Implement early stopping
Save the best model based on validation accuracy
Add precision, recall and F1-score
Try ResNet or EfficientNet
Create a Streamlit web application
Deploy the model as an API
Add real-time webcam prediction

👨‍💻 Author
Surya Prakash Nayak

⭐ Project
If you find this project useful, consider giving the repository a ⭐ on GitHub.
