## Distributed IoT Vision System
### ESP32-S3 Edge Streaming with Server-Side Facial Recognition

###Abstract

This project implements a distributed real-time IoT vision system using an ESP32-S3 with an OV2640 for edge-based image acquisition and MJPEG streaming over WiFi.
Captured frames are transmitted to a host processing server where facial detection and recognition are performed using OpenCV. The system demonstrates embedded camera interfacing, hardware-accelerated compression, memory-aware buffering strategies, and distributed AI processing.
The architecture intentionally separates image acquisition from computationally intensive inference to reflect production IoT design principles.

+------------------------+
|  ESP32-S3 Edge Device  |
|------------------------|
| - Camera Capture       |
| - Hardware JPEG Encode |
| - PSRAM Buffering      |
| - HTTP MJPEG Stream    |
+-----------+------------+
            |
            | MJPEG over HTTP
            v
+------------------------+
|  Processing Server     |
|------------------------|
| - Frame Decode         |
| - Face Detection       |
| - Face Recognition     |
| - Logging & Display    |
+------------------------+


## Architectural Rationale

Microcontrollers are optimized for deterministic I/O operations.
Facial recognition requires memory-intensive matrix computation.

Separating acquisition and inference:
Improves frame rate stability
Reduces embedded memory pressure
Enables scalable processing
Mirrors real-world IoT deployments

### Hardware Platform

ESP32-S3 N16R8
-Dual-core 240 MHz
-16MB Flash
-8MB PSRAM
OV2640

Why ESP32-S3
-Dedicated camera interface with DMA
-Hardware JPEG encoder
-External PSRAM support
-Integrated WiFi stack
-Vector instruction support (future TinyML expansion)

### Memory Strategy

QVGA frame (320×240):
320 × 240 ≈ 76 KB (grayscale equivalent)

PSRAM enables:
-Double frame buffering
-Stable MJPEG streaming
-Reduced frame drops under WiFi jitter
-Future on-device inference experimentation

### Embedded Firmware Design
Core Components
-Espressif Camera Driver
-PSRAM-backed frame buffers
-HTTP streaming server
-Snapshot REST endpoint
-Configurable WiFi credentials

Data Flow
-Camera DMA transfers frame to PSRAM
-Hardware JPEG compression applied
-Frame served via HTTP MJPEG boundary stream
-Client decodes JPEG frames
-This design prevents network latency from interfering with frame acquisition.

### Processing Pipeline

Host-side implementation (Python + OpenCV):
1. Connect to MJPEG stream
2. Decode JPEG frames
3. Convert to grayscale
4. Detect faces
5. Perform identity recognition
6. Annotate and display
7. Log detection timestamps

Inference remains off-device to preserve real-time throughput.

### File Structure

/firmware
    camera_stream.ino
/server
    server.py
    recognition.py
    requirements.txt
/docs
    architecture_diagram.png
README.md
