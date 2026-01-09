Corn Futures Price Prediction Model
Project Overview
This project implements a hybrid deep learning architecture designed to predict the percentage change in corn future prices. By fusing high-dimensional satellite imagery with quantitative market indicators and environmental data, the model aims to capture both long-term crop development trends and short-term market volatility.

The core approach utilizes a Convolutional Neural Network (CNN) for feature extraction from satellite data, coupled with a Long Short-Term Memory (LSTM) network to process time-series sequences.

Methodology
1. Data Fusion & Feature Engineering
The model processes a diverse set of inputs to create a unified representation of the market and crop conditions.

Satellite Imagery & Compression: We utilize ResNet-50 to extract features from satellite vectors. These high-dimensional outputs (2048 dimensions) are compressed to 64 dimensions to preserve the most predictive features while maintaining computational efficiency.

Market & Environmental Indicators:

Market Momentum: Relative Strength Index (RSI) and Bollinger Bands are used to quantify market volatility and momentum.

Crop Development: Growing Degree Days (GDD) are calculated to track temperature accumulation relevant to crop maturity.

Data Standardization: All numerical features are standardized to ensure stable convergence during model training.

2. Contextual Embeddings
To address the irregularities inherent in agricultural and temporal data, we implemented several embedding strategies:

Area Embeddings: Learnable vectors are assigned to each corn-producing county to capture location-specific nuances, such as soil composition and historical yield traits, that cannot be derived from satellite imagery alone.

Time Embeddings: We explicitly encode the days elapsed between observations. This allows the LSTM to differentiate between actual crop growth and variations caused by irregular satellite revisit times.

Cyclic Seasonality: Dates are converted into sine/cosine pairs. This transformation preserves the cyclical nature of the annual calendar, helping the model recognize seasonal growth patterns across year boundaries.

Model Architecture
Hybrid CNN-LSTM Design
The system uses a two-stage architecture:

Feature Extraction (CNN): Processes spatial data from satellite images.

Sequence Prediction (LSTM): A specialized Recurrent Neural Network designed for time-series data. The LSTM is responsible for "remembering" long-term trends while filtering out daily noise.

Training Objectives & Stabilization
Target Metric: The model is trained to predict percentage change rather than absolute price. This reduces bias toward specific price levels and focuses the model on directional market movement.

Gradient Clipping: We cap error signals during backpropagation to prevent "exploding gradients," ensuring the model remains stable even during drastic market shifts.

Regularization: A Dropout rate of 0.4 (40%) is applied to prevent overfitting, forcing the network to learn robust generalizations rather than memorizing the training data.

Future Improvements
Integration of real-time weather forecasts.

Expansion of the Area Embeddings to cover international corn-producing regions.
