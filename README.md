🌀 DeepCyclone: Hybrid AI for Hurricane Forecasting
A Multi-Modal Deep Learning Framework for Predicting Rapid Intensification (RI) in Tropical Cyclones using GOES-16 Satellite Imagery.

📌 Project Overview
Rapid Intensification (RI) of hurricanes is one of the most challenging forecasting problems in meteorology. This project introduces DeepCyclone, a hybrid neural network that fuses Computer Vision (CNN) with Atmospheric Physics (MLP).
By constructing a custom data pipeline that streams raw satellite data from NOAA's GOES-16 (AWS S3), this system analyzes both the visual structure of the storm core and thermodynamic parameters (wind speed) to detect early warning signs of intensification.

⚙️ Key Features
Automated Data Pipeline: Custom Python script to fetch, decode, and crop high-frequency satellite imagery (NetCDF) from AWS Open Data based on IBTrACS coordinates.
Geospatial Engineering: Implements complex coordinate transformations (Lat/Lon to Geostationary Projection) using pyproj to accurately center the storm eye.
Hybrid Architecture: A Dual-Input Neural Network processing:
Visual Input: 100x100 IR Satellite Imagery (via CNN).
Physical Input: Current Wind Speed (via MLP).

🧠 Model Architecture
The model utilizes a multi-modal approach:
Branch 1 (CNN): 3 Convolutional blocks to extract spatial features (eye wall structure, cloud texture).
Branch 2 (MLP): Dense layers to process scalar environmental variables.
Fusion Layer: Concatenates visual and physical vectors to predict the probability of RI (>30 kt increase in 24h).

📊 Experimental Results & Analysis
Experiment 1: Baseline Model
Outcome: The model showed rapid convergence on training data but plateaued validation accuracy.
Interpretation: Clear signs of Overfitting due to the limited dataset size ($N=50$), indicating the architecture works but requires more data to generalize.
Experiment 2: Data Augmentation
Outcome: After applying random rotation and zooming, the model exhibited Underfitting.
Scientific Analysis:
Complexity Mismatch: Augmentation increased the problem complexity significantly.
Capacity Limit: The lightweight CNN architecture lacked the parameter capacity to map the increased variance.
Conclusion: This experiment confirms that while the pipeline is robust, future improvements require scaling the dataset to N > 1,000 unique events rather than artificially augmenting a small sample.

🚀 How to Run
This project was developed in Google Colab.
Clone the repository.
Install dependencies:

Bash
pip install s3fs xarray netCDF4 pyproj matplotlib

Run the Jupyter Notebook DeepCyclone_Main.ipynb.

🔮 Future Work
Scale Dataset: Automate the pipeline to download 5 years of Atlantic Hurricane data (2018-2023).
Architecture Upgrade: Implement ResNet-50 or Vision Transformers (ViT) for better feature extraction.
Add Lightning Data: Integrate GLM (Geostationary Lightning Mapper) data as a third input channel.

