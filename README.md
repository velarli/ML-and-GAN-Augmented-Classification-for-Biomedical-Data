Overview

This project implements a complete machine-learning workflow for the analysis, labeling, augmentation, and classification of physiological vital-sign signals, specifically heart rate (HR) and respiratory rate (RR).
The system combines traditional preprocessing techniques with Generative Adversarial Networks (GANs) to create synthetic data and improve classification performance in low-data environments.

The notebook integrates:

Signal preprocessing

Out-of-range detection

Validity labeling

GAN-based synthetic data generation

Dataset augmentation

Decision-tree-based classification (Random Forest)

Visual analytics with color-coded anomaly representation

A. Signal Preprocessing, Range Labeling and GAN-Based Dataset Construction

This section describes the initial modeling pipeline, which prepares the vital-sign data and constructs the dataset used in subsequent modeling steps:

1. Data Cleaning and Preparation

Loads raw physiological measurements.

Fixes invalid values, converts datatypes, and ensures consistent numeric formatting.

Selects relevant variables:

Heart Rate

Respiratory Rate

Person Presence Status

2. Range-Based Labeling

The system evaluates whether each reading is within expected physiological thresholds:

Heart Rate thresholds (Hz)

Respiratory Rate thresholds (Hz)

Two binary flags are generated:

out_of_range_hr

out_of_range_rr

3. Validity Classification

To distinguish noise/artifacts from meaningful anomalies, each sample is evaluated in relation to its neighbors.
The label valid_reading identifies:

1 → valid measurements

0 → invalid or artifact readings

4. Feature Scaling

Data is normalized to [0, 1] using MinMaxScaler, preparing it for GAN training.

This completes the construction of the base dataset used for generative modeling.

B. GAN-Based Data Augmentation and Classification Tree Modeling for Signal-Range Verification

This section describes the formal GAN training and classification modeling process, designed to enhance classifier performance through synthetic data augmentation.

1. GAN Architecture

A standard adversarial setup is used:

Generator
Produces synthetic HR/RR/presence samples from random noise.

Discriminator
Distinguishes real data from generator-produced synthetic data.

Both networks are trained using binary cross-entropy and optimized adversarially.

2. GAN Training Procedure

Training alternates between:

Training the discriminator using real vs. synthetic samples.

Training the generator through the combined GAN to fool the discriminator.

This iterative process allows the generator to learn the statistical structure of the physiological signals.

3. Synthetic Data Generation + Augmentation

Once trained, the GAN generates synthetic vital-sign measurements that:

mimic real physiological patterns

expand the dataset’s distribution

provide examples of rare or borderline cases

The synthetic data is:

Inversely scaled back to original units

Assigned labels

Combined with real data to form an augmented dataset

4. Classification Tree Modeling

A Random Forest classifier is trained on the augmented dataset to classify:

in-range readings

out-of-range readings

invalid or noisy measurements

Performance metrics include:

Accuracy

Confusion matrix

Classification report (precision, recall, F1-score)

🎨 Visualization of Vital-Sign Signals

The notebook includes a color-coded visualization of HR and RR:

Red → both signals out of range

Orange → HR out of range

Yellow → RR out of range

Gray → normal readings

These plots help identify:

clusters of anomalies

isolated noise artifacts

correlations between HR and RR deviations

🧪 Key Technical Components

Python, NumPy, Pandas

Scikit-Learn (MinMaxScaler, RandomForestClassifier)

TensorFlow / Keras (GAN implementation)

Matplotlib for visualization

💡 Purpose and Benefits

This dual-stage modeling approach (A + B):

Enhances classification robustness

Addresses data scarcity through synthetic generation

Improves anomaly detection in vital-sign signals

Provides visually interpretable diagnostics

Supports future integration into real-time monitoring systems
