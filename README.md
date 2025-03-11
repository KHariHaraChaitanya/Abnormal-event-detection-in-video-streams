# Anomaly Detection in Video Surveillance Using Spatio-Temporal Autoencoder

This project introduces a method for detecting unusual activities in video surveillance using a spatio-temporal autoencoder. The goal is to create a deep learning model that can identify anomalies in video streams, which is a key part of modern surveillance systems. The model combines Convolutional Neural Networks (CNNs) and Long Short-Term Memory (LSTM) networks to analyze both the visual and time-based patterns in video data.

## Key Features

- **Spatio-Temporal Analysis**: The model uses CNNs to process visual information and LSTMs to understand how this information changes over time.
- **Anomaly Detection**: By learning to reconstruct normal video sequences, the model can detect anomalies by identifying significant differences between the original and reconstructed frames.
- **Testing**: The model has been tested on well-known datasets like the **Chinese University of Hong Kong (CUHK) Avenue dataset** and the **University of California San Diego (UCSD) Ped1 dataset**, which include a variety of normal and abnormal events.
- **Embedded Device Deployment**: The model has been successfully deployed on a **Raspberry Pi 4 Model B**, demonstrating its potential for real-world surveillance applications.

## How It Works

1. **Training**: The autoencoder is trained on normal video sequences. It learns to reconstruct these sequences accurately.
2. **Anomaly Detection**: During testing, the model tries to reconstruct new video sequences. If the reconstruction error is high, it indicates the presence of an anomaly.
3. **Evaluation**: The model's performance is measured using standard metrics on datasets that include both normal and abnormal events.

## Deployment on Raspberry Pi 4 Model B

The model was successfully deployed on a Raspberry Pi 4 Model B, demonstrating its feasibility for real-world surveillance applications. Here’s how the deployment was achieved:

1. **Model Conversion to TensorFlow Lite (TFLite)**:
   - The trained TensorFlow model was converted to TFLite format using post-training quantization techniques. This reduced the model size and made it suitable for deployment on resource-constrained devices like the Raspberry Pi.

2. **Setting Up the Raspberry Pi**:
   - The Raspberry Pi 4 Model B was configured with the necessary libraries, including TensorFlow Lite, OpenCV, and other dependencies like `libatlas` and `libjasper`.
   - A Python script was used to load the TFLite model and perform inference on video streams captured by the Raspberry Pi camera module.

3. **Running the Model**:
   - The Python script was executed on the Raspberry Pi, initiating the anomaly detection process.
   - The script monitored the video stream in real-time, and if anomalies were detected, it provided relevant information on the terminal or any connected display.

4. **Performance on Raspberry Pi**:
   - The model ran efficiently on the Raspberry Pi, demonstrating its capability to handle real-time video analysis.
   - Despite the hardware limitations, the model maintained a good balance between accuracy and inference speed, making it suitable for practical surveillance applications.

## Setting Up the Raspberry Pi for TFLite Model Deployment

This section provides a step-by-step guide to set up the Raspberry Pi 4 Model B for deploying the TFLite model.

### Prerequisites
- **Raspberry Pi 4 Model B**
- **MicroSD card** with Raspbian OS installed
- **Raspberry Pi camera module** (optional, for real-time video capture)
- **Stable internet connection**

### Step 1: Install Required Libraries
1. **Update the Raspberry Pi**:
   ```bash
   sudo apt update
   sudo apt upgrade
   ```

2. **Install Python and Pip**:
   ```bash
   sudo apt install python3 python3-pip
   ```

3. **Install TensorFlow Lite Runtime**:
   ```bash
   pip3 install tflite-runtime
   ```

4. **Install OpenCV and Other Dependencies**:
   ```bash
   sudo apt install libopencv-dev python3-opencv
   sudo apt install libatlas-base-dev libjasper-dev
   ```

### Step 2: Set Up the Camera Module (Optional)
1. **Enable the Camera Interface**:
   - Run `sudo raspi-config` and navigate to `Interfacing Options` > `Camera` to enable the camera module.

2. **Test the Camera**:
   ```bash
   raspistill -o test.jpg
   ```
   For detailed information, you can check this link from [medium.com](https://fulldataalchemist.medium.com/camera-setup-on-raspberry-pi-4-912e7d415cdf).

### Step 3: Deploy the TFLite Model
1. **Copy the TFLite Model to the Raspberry Pi**:
   - Transfer the `.tflite` model file to the Raspberry Pi using SCP or a USB drive.

2. **Create a Python Script for Inference**:
   - Write a Python script to load the TFLite model and perform inference on video streams.

3. **Run the Script**:
   ```bash
   python3 anomaly_detection.py
   ```

### Step 4: Monitor and Optimize
- Monitor the script’s output on the terminal or a connected display.
- Optimize the script for better performance by adjusting the frame rate, resolution, or model parameters.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
