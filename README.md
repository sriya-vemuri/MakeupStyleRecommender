# Deep Learning Based Makeup Style Recommendation

A deep learning project that predicts structural facial attributes from face images and recommends makeup styles such as Natural, Lip Focus, or Full Glam. This project was built as a data-driven beauty AI system to support personalized styling, virtual try-on experiences, and more confident product recommendations.

## Overview

Many people are unsure which makeup style best suits their facial features. A look that works well for one person may not complement another person’s facial structure in the same way. In beauty retail and digital beauty platforms, this creates an opportunity for more personalized recommendations.

This project builds a deep learning system that uses face images to predict structural facial attributes such as high cheekbones, big lips, or arched eyebrows, and then maps those predictions into makeup style recommendations. The goal is to make beauty guidance more personalized, interactive, and data-driven.

## Business Problem

Beauty brands, e-commerce platforms, and virtual try-on applications increasingly rely on personalized customer experiences. However, users often struggle to decide which makeup look suits them best.

A recommendation system like this can help improve:

- customer engagement
- confidence in beauty product selection
- personalized virtual styling
- product conversion rates
- digital assistant capabilities for beauty brands

By recommending styles based on facial attributes, the system can act as an AI beauty advisor that supports both discovery and decision-making. :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

## Dataset

This project uses the CelebA dataset, a large-scale facial image dataset commonly used in computer vision tasks.

The dataset includes:

- over 200,000 aligned celebrity face images
- 40 binary facial attributes per image

Examples of attributes include:

- `Arched_Eyebrows`
- `Big_Lips`
- `High_Cheekbones`
- `Oval_Face`
- `Heavy_Makeup`
- `Wearing_Lipstick`

For this project, a subset of structural facial attributes was used as model targets, while makeup-related attributes and a neutralized style rating were used to build the style recommendation logic. A random sample of 60,000 images was selected to make training computationally manageable. :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5}

## Project Workflow

### 1. Data Cleaning and Preparation

The dataset was cleaned and prepared by:

- loading the CelebA attribute file into a structured table
- converting attribute values from `-1/1` to binary `0/1`
- selecting ten structural facial attributes as prediction targets
- retaining two makeup-related attributes for style scoring
- attaching each image filename to its full image path
- randomly subsampling 60,000 images for training efficiency
- splitting the sample into training and validation sets with a fixed random seed

This created a reproducible and structured dataset ready for deep learning. :contentReference[oaicite:6]{index=6}

### 2. Image Transformation

Images were processed for model training using standard computer vision transformations.

For the training set:

- resize to `128 x 128`
- random horizontal flips
- slight rotations
- mild brightness and contrast changes
- normalization using ImageNet statistics

For the validation set:

- resize
- normalization only

This helped improve generalization while keeping validation consistent. :contentReference[oaicite:7]{index=7}

### 3. Modeling

The task was framed as a multi-label classification problem because a face can have multiple structural attributes at the same time.

The model used:

- pretrained `ResNet-50` backbone
- transfer learning from ImageNet weights
- dropout layer with rate `0.5`
- custom fully connected output layer with 10 units
- sigmoid activation for attribute probabilities

The model predicts structural facial features from an input face image, and those predictions are then passed into a style engine that recommends one of several makeup styles. :contentReference[oaicite:8]{index=8} :contentReference[oaicite:9]{index=9}

### 4. Style Recommendation Logic

Beyond attribute prediction, the project includes a recommendation layer that translates predicted facial attributes into makeup looks.

The style engine aggregates predictions and maps them into style categories such as:

- Natural
- Lip Focus
- Full Glam

The system also includes an `analyze_single_image` style of workflow for processing external user-input images and producing a user-friendly recommendation with confidence-based reasoning. :contentReference[oaicite:10]{index=10}

## Evaluation

The model was evaluated using accuracy, micro-averaged F1, per-class precision, and per-class recall.

Reported observations include:

- the model performed much better than a random baseline
- it performed best on `Full Glam`
- it struggled more with subtle looks such as `Natural`
- class imbalance in the dataset affected prediction quality
- validation performance plateaued earlier than training performance

The presentation reports the following illustrative performance values:

- Full Glam F1: `0.82`
- Average Micro-F1: `0.65`
- Natural Look F1: `0.45`
- Random Baseline: `0.15`

These results suggest that the model learned useful patterns, but dataset bias limited its ability to distinguish underrepresented and subtle makeup styles. :contentReference[oaicite:11]{index=11} :contentReference[oaicite:12]{index=12}

## Implementation Challenges

Several practical modeling challenges emerged during development:

- class imbalance due to overrepresentation of glam-heavy celebrity images
- overfitting on the training data
- computational limitations due to dataset size and model complexity

Solutions explored included:

- weighted loss functions
- dropout layers
- image augmentation
- using a pretrained ResNet-50 backbone instead of training from scratch

These steps improved performance, but some residual bias remained in the model outputs. :contentReference[oaicite:13]{index=13} :contentReference[oaicite:14]{index=14}

## Business Impact

If deployed effectively, this system could support a range of beauty-tech applications.

Potential value includes:

- AI-powered virtual beauty advisors
- personalized product recommendations
- more engaging beauty apps and try-on experiences
- improved user confidence during purchase decisions
- curated style-to-product mapping for ecommerce

The project demonstrates how computer vision and deep learning can be used to create an interactive recommendation engine for the beauty industry. :contentReference[oaicite:15]{index=15} :contentReference[oaicite:16]{index=16}

## Deployment Considerations

A production deployment would likely involve:

- selfie upload through a mobile or web interface
- backend preprocessing for resizing and normalization
- inference through the trained ResNet-based model
- style recommendation generation through the style engine
- returning suggested looks, reasoning, and linked products or tutorials

Important deployment concerns include:

- inference latency because ResNet-50 is computationally heavy
- need for lighter models or model quantization
- sensitivity to image quality and cropping
- server-side hardware cost
- variability caused by poor network conditions or lower-end devices

The report suggests future deployment may benefit from lighter backbones such as ResNet-18 or edge inference approaches. :contentReference[oaicite:17]{index=17} :contentReference[oaicite:18]{index=18}

## Ethical Considerations

This project raises important fairness and representation concerns.

Key risks include:

- underrepresentation of certain demographics in the dataset
- reinforcing narrow or outdated beauty standards
- uneven performance across skin tones, facial structures, or age groups
- possible negative effects on user self-perception
- privacy concerns related to facial image handling

To reduce these risks, any real-world deployment should include:

- fairness audits across diverse demographic groups
- balanced and more representative training data
- transparent communication that recommendations are suggestions, not judgments
- explicit consent and secure handling of uploaded face images
- user control through multiple ranked recommendations instead of a single prescribed look

These concerns were highlighted directly in both the presentation and final report. :contentReference[oaicite:19]{index=19} :contentReference[oaicite:20]{index=20}

## Tech Stack

- Python
- PyTorch
- torchvision
- ResNet-50
- Pandas
- NumPy
- image preprocessing and augmentation workflows
- transfer learning
- multi-label classification

## Use Case

This project is best suited for:

- beauty brands building virtual stylist tools
- ecommerce platforms offering personalized beauty recommendations
- makeup and skincare apps with selfie-based experiences
- beauty-tech teams experimenting with AI recommendation engines
- digital assistants that map facial attributes to product suggestions

## Key Takeaways

- facial attribute prediction can support personalized makeup recommendations
- transfer learning with ResNet-50 provides a strong foundation for this task
- the model performed well on dominant makeup classes like Full Glam
- class imbalance remained a major limitation for subtle styles
- fairness, representation, and privacy are critical for real-world deployment
- this is most practical as a decision-support tool rather than a fully autonomous beauty system

## Team

Section A Team 13:

- Amna Mahmood
- Samir Dar
- Chloe Hu
- Sriya Vemuri
- Kerry Chen
- Calida Mathias :contentReference[oaicite:21]{index=21}

## Future Improvements

Potential next steps include:

- balancing the dataset more aggressively
- oversampling underrepresented natural looks
- testing lighter architectures such as ResNet-18
- applying model distillation or quantization for deployment
- running fairness audits across diverse user groups
- improving subtle style detection
- building a web or mobile interface for real-time recommendations
- linking style predictions directly to curated product sets
