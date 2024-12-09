# DBAL: Discriminator-Based Active Learning (Discriminator is a Strong Data Sampler)

This repository serves as a technical documentation of DBAL (Discriminator-Based Active Learning), a novel active learning strategy that uses a discriminator to dynamically select the most valuable data for labeling based on its output distribution.

> **Important Notice**: Due to **confidentiality requirements**, the source code is **currently not available for public release**. However, a demo version jupyter script 'dbal_demo.ipynb' is opened for checking the feasibility of this project. We will **consider making the code public in the future**. Additionally, **only a small subset of the data is offered** here, due to license consideration. Thank you very much for your understanding. :-D

> **重要提示**：由于**保密要求**，源代码**目前不对外公开发布**。然而，我们提供了一个用作演示的 jupyter 脚本 'dbal_demo.ipynb' 以便您检查本项目的可行性。我们将**考虑在未来公开代码**。此外，考虑到许可证等因素，这里**仅提供数据的一小部分子集**。非常感谢您的理解。:-D

## Running DBAL Demo Version
You need to put the downloaded and decompressed 'data_demo' file (which is a subset of the original dataset) on the same directory with 'dbal_demo.ipynb', then you can simply run 'dbal_demo.ipynb' for testing DBAL. :-D
If you haven't downloaded 'data_demo' yet, please download it from https://pan.baidu.com/s/1OJ03_hJ0GL3bcDKais135Q (verification code: fvvb).

## Project Dependencies
Required Python packages:
- numpy
- pandas
- torch
- torchvision
- Pillow
- tqdm
- matplotlib

Note: Other imported packages like os, shutil, glob are Python standard libraries which don't require additional installation.

## Overview of DBAL

Active learning aims to achieve optimal model performance with minimal labeled data by intelligently selecting the most informative samples for labeling. DBAL improves upon existing approaches by:

- Using a simple yet effective discriminator-based architecture
- Leveraging the target model's probability distributions as features
- Employing an easily trainable sampling strategy
- Achieving superior performance compared to traditional methods

## Architecture

DBAL consists of two main components:

1. **Classifier**: A modified ResNet that serves as both the target model and feature extractor
   - Four residual blocks with batch normalization and ReLU activation
   - Dropout layer before final fully connected layer
   - Optimized for small-scale datasets

2. **Discriminator**: A binary classifier that distinguishes labeled from unlabeled data
   - Four fully connected layers with ReLU activation
   - Final sigmoid activation layer
   - Trained using binary cross-entropy loss

## How It Works

1. The classifier processes images and outputs probability distributions
2. These distributions are used as features by the discriminator
3. The discriminator learns to distinguish between labeled and unlabeled data
4. During sampling, data points that the discriminator is least confident about being labeled are selected for labeling
5. This process iteratively improves the classifier's performance

## Implementation Details

### Requirements
- PyTorch
- NumPy
- scikit-learn

### Key Parameters
- Initial label pool: 300 images
- Batch size for sampling: 300 images
- Classifier training: 400 epochs
- Discriminator training: 50 epochs
- Optimizer settings:
  - Classifier: SGDM with learning rate 5×10^-4
  - Discriminator: Adam with learning rate 5×10^-6

### Data Preprocessing
1. Resize to 256x256
2. Random crop to 150x150
3. Random horizontal flip (50% probability)
4. Random affine transformations
5. Color jittering
6. Normalization using dataset statistics

## Results

DBAL outperforms several baseline methods:
- +2.88% improvement over Entropy Sampling
- +3.17% improvement over Random Sampling
- +62.53% improvement over VAAL

## License

This project is licensed under the MIT License.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
