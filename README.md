# OOD_Detection
[--->> View Paper <<---](https://drive.google.com/file/d/1gbOGJ_RghqT8PtpEbiBvCCxduZxK5ZMR/view?usp=drive_link)

Out-of-Distribution (OOD) detection refers to the task of identifying whether a given input comes from the data distribution the model was trained on (in-distribution) or from a different distribution (out-of-distribution).

## Algorithms for OOD Detection:
### Maximum Softmax Probability:
The idea here is that a deep neural network, when confronted with an OOD sample, might be overconfident in its incorrect classification.
This method examines the maximum softmax probability of the network's output. For in-distribution samples, this value is expected to be high, while for OOD samples, even if it's high, the class label might not make sense.
A threshold is set on this probability to differentiate between in-distribution and OOD samples.

### ODIN with Temperature Scaling:
ODIN stands for "Out-of-Distribution detector for Neural networks". It's an enhancement of the Maximum Softmax Probability method.
The method involves adding a small perturbation to the input data and adjusting the softmax temperature. Both of these help in increasing the separation between in-distribution and OOD samples' softmax scores, making OOD detection more reliable.

### Energy-based Detection:
This method is based on the observation that neural networks assign lower energies to data from the training distribution and higher energies to out-of-distribution data.
The energy of a sample can be defined in various ways, including the negative log-likelihood or other criteria, depending on the architecture.
By setting a threshold on the energy levels, one can detect OOD samples.

### Outlier Exposure:
This approach involves explicitly training a model with in-distribution data labeled as positive and a diverse set of OOD data labeled as negative.
During training, the model is exposed to these outliers (OOD data) and learns to distinguish them from in-distribution data.

## Dataset and Network:
### Resnet20 trained on CIFAR-10:
Resnet20 is a variant of the ResNet (Residual Network) architecture with 20 layers. ResNets are known for their skip connections, which help in training deep networks by allowing gradients to flow through these connections, preventing the vanishing gradient problem.
CIFAR-10 is a dataset consisting of 60,000 32x32 color images in 10 classes, with 6,000 images per class. This dataset is used for the in-distribution samples in the project.

### OOD Samples:
CIFAR-100: Similar to CIFAR-10 but consists of 100 classes with fewer images per class.
SVHN (Street View House Numbers): A dataset derived from Google Street View images and consists of house numbers.
MNIST: A dataset of handwritten digits with 28x28 grayscale images.
Uniform Noise: Random noise generated uniformly.
Gaussian Noise: Random noise generated based on a Gaussian or normal distribution.

For this project, we are trained a Resnet20 on CIFAR-10 to recognize in-distribution samples and then tested its ability to detect whether other datasets (CIFAR-100, SVHN, MNIST) and noise (Uniform and Gaussian) are in or out-of-distribution using the algorithms listed.



## Out-of-Distribution (OOD) Detection Performance

This table presents the OOD detection performance of various model architectures using different methods. The metrics AUROC (Area Under the Receiver Operating Characteristic curve) and FPR@.95TPR (False Positive Rate at a True Positive Rate of 0.95) are used to evaluate the models.

| Model Architecture     | In-Distribution/Out-of-Distribution | OOD Detection Method      | AUROC | FPR @ .95TPR |
|------------------------|-------------------------------------|---------------------------|-------|--------------|
| ResNet-20              | CIFAR10/MNIST                       | Baseline                  | 0.853 | 0.463        |
| ResNet-20              | CIFAR10/MNIST                       | ODIN (T=1000)             | 0.903 | 0.438        |
| ResNet-20              | CIFAR10/MNIST                       | Energy                    | 0.904 | 0.401        |
| ResNet-20              | CIFAR10/MNIST                       | ODIN (T=1000)             | 0.914 | 0.345        |
| ResNet-10              | CIFAR10/MNIST                       | ODIN (T=1000)             | 0.786 | 0.530        |
| ResNet-30              | CIFAR10/MNIST                       | ODIN (T=1000)             | 0.921 | 0.292        |
| Wide ResNet-20         | CIFAR10/MNIST                       | ODIN (T=1000)             | 0.935 | 0.236        |
| Narrow ResNet-20       | CIFAR10/MNIST                       | ODIN (T=1000)             | 0.834 | 0.426        |
| ResNet-20              | CIFAR5/SVHN                         | Baseline with CIFAR1 OE   | 0.589 | 0.866        |
| ResNet-20              | CIFAR5/SVHN                         | Baseline with CIFAR5 OE   | 0.545 | 0.905        |
| ResNet-20              | CIFAR5/SVHN                         | Baseline with CIFAR20 OE  | 0.558 | 0.868        |
| ResNet-20              | CIFAR5/SVHN                         | Baseline with CIFAR50 OE  | 0.745 | 0.728        |
| ResNet-20              | CIFAR5/SVHN                         | Baseline with CIFAR100 OE | 0.815 | 0.546        |
| ResNet-20              | CIFAR5/Other5                       | Baseline with CIFAR1 OE   | 0.454 | 0.999        |
| ResNet-20              | CIFAR5/Other5                       | Baseline with CIFAR5 OE   | 0.428 | 0.998        |
| ResNet-20              | CIFAR5/Other5                       | Baseline with CIFAR20 OE  | 0.620 | 0.894        |
| ResNet-20              | CIFAR5/Other5                       | Baseline with CIFAR50 OE  | 0.679 | 0.819        |
| ResNet-20              | CIFAR5/Other5                       | Baseline with CIFAR100 OE | 0.702 | 0.723        |
| ResNet-20              | CIFAR10/SVHN                        | Baseline with Robust OE   | 0.922 | 0.329        |
| ResNet-20              | CIFAR10/Other5                      | Baseline with Robust OE   | 0.772 | 0.689        |
| ResNet-20              | CIFAR10/MNIST                       | Baseline with Robust OE   | 0.997 | 0.005        |
| ResNet-20              | CIFAR10/Uniform                     | Baseline with Robust OE   | 0.965 | 0.037        |
| ResNet-20              | CIFAR10/Gaussian                    | Baseline with Robust OE   | 0.971 | 0.031        |
| ResNet-20              | CIFAR10/MNIST                       | Energy with Robust OE     | 0.830 | 0.912        |
| ResNet-20              | CIFAR10/SVHN                        | Energy with Robust OE     | 0.894 | 0.439        |
| ResNet-20              | CIFAR10/CIFAR100                    | Energy with Robust OE     | 0.781 | 0.847        |
| ResNet-20              | CIFAR10/Uniform                     | Energy with Robust OE     | 1.0   | 0.0          |
| ResNet-20              | CIFAR10/Gaussian                    | Energy with Robust OE     | 1.0   | 0.0          |

