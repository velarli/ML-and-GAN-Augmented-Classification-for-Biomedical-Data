Overview

This project implements a full workflow for analyzing physiological signals (heart rate and respiratory rate), detecting out-of-range values, generating synthetic data with a GAN, and training a classifier to verify signal validity and anomalies.

🅰️ A. Signal Preprocessing and Dataset Construction

- Load and clean raw physiological data.
- Define physiological thresholds and create out-of-range flags (out_of_range_hr, out_of_range_rr).
- Identify valid vs. invalid readings using neighborhood-based logic.
- Normalize features with MinMaxScaler to prepare for generative modeling.

🅱️ B. GAN-Based Data Augmentation and Classification

- Train a GAN (Generator + Discriminator) to learn the distribution of HR/RR measurements.
- Generate synthetic samples that expand the dataset and improve class balance.
- Combine real + synthetic data to create an augmented dataset.
- Train a Random Forest classifier to detect:
  - valid in-range readings
  - valid out-of-range readings
  - invalid/noisy readings
- Evaluate with accuracy, confusion matrix and classification report.

🎨 Visualization

Color-coded plots highlight signal behavior:
- Red: both HR and RR out of range
- Orange: HR out of range
- Yellow: RR out of range
- Gray: normal readings
This reveals patterns, anomalies, and sensor noise.

💡 Key Benefits

- Improved classifier robustness through synthetic data.
- Better detection of rare anomalies.
- Clear visual interpretation of physiological signal behavior.
- End-to-end pipeline ready for real-world monitoring or research applications.
