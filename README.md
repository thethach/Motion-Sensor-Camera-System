# Motion Detection & Cloud-Based Image Alert System

## Overview

This project is a **motion detection and notification system** that captures images when motion is detected and delivers alerts through a cloud-based infrastructure. It integrates **embedded hardware**, **Bluetooth Low Energy (BLE)** communication, and **AWS cloud services** to provide real-time monitoring and email notifications.

The system is designed to detect motion using a PIR sensor, trigger image capture via a Raspberry Pi camera, store images in the cloud, and send email alerts containing the captured images.

---

## System Architecture

1. **Motion Detection**

   * PIR sensor detects motion
   * Rising-edge detection prevents false positives at startup

2. **BLE Communication**

   * ESP32 hosts a BLE server
   * Motion state (0 or 1) is sent to Raspberry Pi via BLE characteristics

3. **Image Capture**

   * Raspberry Pi captures an image when motion is confirmed
   * LED and buzzer provide visual and audio feedback during capture

4. **Cloud Integration**

   * Image uploaded to AWS S3
   * Flask server hosted on AWS EC2 sends SMTP email alerts
   * Images embedded in emails and displayed on a web interface

---

## Hardware Components

* **ESP32 TTGO OLED Board**

  * Hosts BLE server
  * Interfaces with sensors, LED, and buzzer
* **PIR Motion Sensor**

  * Detects infrared-based motion
  * Outputs `0` (no motion) or `1` (motion)
* **Raspberry Pi Camera**

  * Captures images upon motion detection
* **LED**

  * Indicates when an image is being captured
* **Buzzer**

  * Audible alert during image capture
* **10Ω Resistor**

  * Used to limit LED brightness

---

## Software & Technologies

* **AWS EC2**

  * Hosts Flask server
  * Handles SMTP email notifications
* **AWS S3**

  * Stores captured images
  * Serves images for emails and web display
* **Flask (Python)**

  * Backend web server
  * Handles image links and email delivery
* **Bluetooth Low Energy (BLE)**

  * Communication between ESP32 and Raspberry Pi
* **Python**

  * Image capture, BLE client, cloud upload, and email logic

---

## Key Features

* Real-time motion detection
* Wireless BLE communication between devices
* Cloud-based image storage
* Automated email notifications with embedded images
* Visual and audio feedback during capture
* Web-accessible image display

---

## Challenges & Solutions

### Camera Integration

* **Issue:** OV7670 camera could not reliably transmit image data through the ESP32
* **Solution:** Switched to a Raspberry Pi camera, enabling stable image capture and processing

### False Motion Triggers

* **Issue:** PIR sensor produced high signals during startup
* **Solution:** Implemented **rising-edge detection** to ignore startup noise and minor disturbances

---

## Future Improvements

* Add video capture instead of still images
* Improve motion classification to reduce false alerts
* Implement user authentication for web interface
* Add mobile push notifications
* Optimize power consumption for battery operation

---

## License

This project was developed for educational purposes. A license can be added if open-sourcing is desired.
