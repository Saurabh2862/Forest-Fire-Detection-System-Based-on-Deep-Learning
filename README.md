
# Forest Fire Detection System Based on Deep Learning  

## Overview

The **Real-Time Forest Fire Detection System** utilizes deep learning techniques and drone technology to monitor forest areas for early detection of fires. The system employs an ESP32 Cam mounted on a drone to capture live video footage, which is processed using the YOLOv8 model for effective fire detection.

## Introduction

Forest fires pose a significant threat to the environment, wildlife, and human life. This project aims to address this issue by developing a system that can detect fires in real-time, allowing for prompt intervention and reducing potential damage.

## Objective

The objective of this project is to develop a real-time forest fire detection system using deep learning and the ESP32 Cam mounted on a drone. The system aims to detect forest fires early, enabling prompt intervention to minimize environmental damage and protect lives.

### Key Goals:
- **Early Detection:** Use deep learning to recognize fire in its early stages.
- **Prompt Intervention:** Enable quick alerts to authorities for rapid response.

### Methodology

We utilize the **YOLOv8 model** due to its efficiency and accuracy in object detection. The main components of the project include:
- **Dataset Preparation:** The model is trained on a dataset containing images of fire and non-fire scenarios, prepared using **Roboflow**.
- **Model Training:** **Google Colab** is used for training, employing robust computational resources.
- **Drone Implementation:** An ESP32 Cam captures live video, augmenting coverage and effectiveness in detecting forest fires.

## Conclusion

This project demonstrates the effectiveness of deep learning and drone technology in forest fire detection and shows significant potential for enhancing wildfire management.

## Installation

### Dependencies
Ensure you have the following libraries and tools installed:
- Python 3.x
- TensorFlow
- OpenCV
- Roboflow
- Arduino IDE (for ESP32 Cam firmware)

You can install the necessary Python libraries using:
```bash
pip install tensorflow opencv-python roboflow ultralytics
```

### Model Training
1. Prepare your dataset in Roboflow and export the dataset configuration.
2. Run the following code to train the YOLOv8 model:

    ```python
    # Install the required libraries
    !pip install ultralytics

    # Import necessary library
    from ultralytics import YOLO

    # Set up paths for your dataset
    train_data_path = 'path/to/your/dataset.yaml'
    model_save_path = 'yolov8_fire_detection.pt'

    # Load the YOLOv8 model (this could be a pre-trained model)
    model = YOLO('yolov8n.pt')  # Load a pre-trained YOLOv8 model

    # Train the model
    model.train(data=train_data_path, epochs=50)  # Adjust epochs as necessary

    # Save the trained model
    model.save(model_save_path)
    ```

### ESP32 Cam Setup
1. Install the **ESP32** board in Arduino IDE.
2. Load the following example code to your ESP32 to capture video:

    ```cpp
    #include "esp_camera.h"
    #include <WiFi.h>

    // Set your WiFi credentials
    const char* ssid = "YOUR_SSID";  // Replace with your WiFi SSID
    const char* password = "YOUR_PASSWORD";  // Replace with your WiFi password

    // Define the camera pins for ESP32 Cam
    #define CAMERA_MODEL_AI_THINKER
    #include "camera_pins.h"

    void setup() {
        Serial.begin(115200);
        WiFi.begin(ssid, password);
        while (WiFi.status() != WL_CONNECTED) {
            delay(1000);
            Serial.println("Connecting to WiFi...");
        }
        Serial.println("Connected to WiFi");

        // Initialize camera settings
        camera_config_t config;
        config.ledc_channel = LEDC_CHANNEL;
        config.ledc_timer = LEDC_TIMER;
        config.pin_d0 = Y2;
        config.pin_d1 = Y3;
        config.pin_d2 = Y4;
        config.pin_d3 = Y5;
        config.pin_d4 = Y6;
        config.pin_d5 = Y7;
        config.pin_d6 = Y8;
        config.pin_d7 = Y9;
        config.pin_xclk = XCLK;
        config.pin_pclk = PCLK;
        config.pin_vsync = VSYNC;
        config.pin_href = HREF;
        config.pin_sscb_sda = SIOD;
        config.pin_sscb_scl = SIOC;
        config.pin_pwdn = PWDN;
        config.pin_reset = RESET;
        config.xclk_freq_hz = 20000000;
        config.frame_size = FRAMESIZE_QVGA;
        config.jpeg_quality = 12;
        config.fb_count = 1;

        // Initialize the camera
        esp_err_t err = esp_camera_init(&config);
        if (err != ESP_OK) {
            Serial.println("Camera init failed");
            return;
        }
    }

    void loop() {
        // Capture video and run YOLO model for detection
        // Add code here for fetching frames and processing with your trained model
    }
    ```

3. Replace `YOUR_SSID` and `YOUR_PASSWORD` with your actual WiFi credentials.

## Usage
1. Deploy your trained YOLOv8 model to the ESP32 Cam.
2. Start the drone and ensure the camera is positioned correctly.
3. The system will process the live feed, and upon detecting fire, it will trigger an alarm or notification.

## Acknowledgments
- **Roboflow** for dataset preparation tools.
- **Google Colab** for providing resources for model training.
- **OpenCV and TensorFlow** for their libraries used in vision tasks.

## Authors
Saurabh Pandey
saurabhpandey5794@gmail.com

```

### Instructions for Use
1. Create a new file in your project's root directory and name it `README.md`.
2. Copy the content above into that file.
3. Replace any placeholder text (like `[Your Name]`, `[Your Contact Information]`, etc.) with your actual information.
4. Save the file.

This unified README file provides a comprehensive overview of your project while detailing instructions, objectives, and acknowledgments, suitable for guiding users or collaborators.
