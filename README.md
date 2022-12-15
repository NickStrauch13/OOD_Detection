# OOD_Detection
Various OOD detection algorithms:
1. Maximum Softmax Probability
2. ODIN with temperature scaling
3. Energy-based detection
4. Outlier Exposure

Primarily using Resnet20 trained on CIFAR-10 for in-distribution samples.
Using CIFAR-100, SVHN, MNIST, Uniform Noise, and Gaussian Noise for OOD samples.




Model Architecture
In-Distribution/
Out-of-Distribution
OOD Detection Method
AUROC
FPR@.95TPR
ResNet-20
CIFAR-10/MNIST
Baseline
0.853
0.463
ResNet-20
CIFAR-10/MNIST
ODIN (T=1000)
0.903
0.438
ResNet-20
CIFAR-10/MNIST
Energy
0.904
0.401
ResNet-20
CIFAR-5/SVHN
Baseline with OE
0.922
0.329
ResNet-20
CIFAR-5/Other5
Baseline with OE
 0.772
0.689
ResNet-20
CIFAR-5/MNIST
Baseline with OE
 0.997
0.005
ResNet-20
CIFAR-5/Uniform
Baseline with OE
 0.965
0.037
ResNet-20
CIFAR-5/Gaussian
Baseline with OE
0.971
0.031
ResNet-20
CIFAR-10/MNIST
ODIN (T=1000)
0.914
0.345
ResNet-10
CIFAR-10/MNIST
ODIN (T=1000)
0.786
0.530
ResNet-30
CIFAR-10/MNIST
ODIN (T=1000)
0.921
0.292
Wide ResNet-20
CIFAR-10/MNIST
ODIN (T=1000)
0.935
0.236
Narrow ResNet-20
CIFAR-10/MNIST
ODIN (T=1000)
0.834
0.426


