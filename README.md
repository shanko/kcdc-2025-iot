# KCDC 2025 IoT Camera Project

A Python-based IoT project demonstrating camera functionality using the Raspberry Pi Camera Module with the `picamera2` library.

## Overview

This project provides a simple example of capturing images using a Raspberry Pi camera module. It's designed as a demonstration for IoT applications where image capture and processing are required.

## Features

- **High-Resolution Image Capture**: Captures images at 1920x1080 resolution
- **Live Preview**: Shows a lower-resolution preview (640x480) during operation
- **Simple Configuration**: Easy-to-understand camera setup and configuration
- **Quick Capture**: Automated image capture with minimal delay

## Hardware Requirements

- Raspberry Pi (any model with camera support)
- Raspberry Pi Camera Module (v1, v2, or HQ Camera)
- Proper camera cable connection

## Software Requirements

- Python 3.11 or higher
- `picamera2` library
- Qt libraries for preview display

## Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd kcdc-2025-iot
   ```

2. **Set up a virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Linux/Mac
   # or
   venv\Scripts\activate     # On Windows
   ```

3. **Install dependencies:**
   ```bash
   pip install picamera2
   ```

## Usage

### Basic Image Capture

Run the example script to capture a single image:

```bash
python example_picamera2.py
```

This will:
1. Initialize the camera with dual-stream configuration
2. Display a live preview window
3. Wait 2 seconds for the camera to adjust
4. Capture and save an image as `test.jpg`

### Code Explanation

The `example_picamera2.py` script demonstrates the following workflow:

```python
from picamera2 import Picamera2, Preview
import time

# Initialize camera
picam2 = Picamera2()

# Configure camera streams
camera_config = picam2.create_still_configuration(
    main={"size": (1920, 1080)},    # High-res capture stream
    lores={"size": (640, 480)},     # Low-res preview stream
    display="lores"                 # Use low-res for preview
)

# Apply configuration and start preview
picam2.configure(camera_config)
picam2.start_preview(Preview.QTGL)
picam2.start()

# Allow camera to settle
time.sleep(2)

# Capture image
picam2.capture_file("test.jpg")
```

## Configuration Details

### Camera Streams

The project uses a dual-stream configuration:

- **Main Stream**: 1920x1080 pixels for high-quality image capture
- **Low-Resolution Stream**: 640x480 pixels for efficient preview display

### Preview System

- Uses Qt Graphics Library (QTGL) for hardware-accelerated preview
- Displays the low-resolution stream to reduce system load
- Preview window appears during camera operation

## File Structure

```
kcdc-2025-iot/
├── README.md                 # This documentation file
├── example_picamera2.py      # Main camera demonstration script
├── venv/                     # Python virtual environment
└── test.jpg                  # Output image (created after running the script)
```

## Troubleshooting

### Common Issues

1. **Camera not detected:**
   - Ensure the camera module is properly connected
   - Check that the camera is enabled in `raspi-config`
   - Verify camera permissions

2. **Preview window not appearing:**
   - Install Qt libraries: `sudo apt-get install python3-pyqt5`
   - Ensure X11 forwarding is enabled if using SSH

3. **Permission errors:**
   - Add user to video group: `sudo usermod -a -G video $USER`
   - Restart the session after group changes

### Hardware Setup

1. Power off the Raspberry Pi before connecting the camera
2. Connect the camera cable with contacts facing the correct direction
3. Ensure the cable is firmly seated in both connectors
4. Enable the camera interface using `sudo raspi-config`

## Extending the Project

This basic example can be extended for various IoT applications:

- **Motion Detection**: Add motion detection algorithms
- **Time-lapse Photography**: Implement scheduled capture
- **Remote Monitoring**: Add network streaming capabilities
- **Image Processing**: Integrate OpenCV for analysis
- **Cloud Storage**: Upload images to cloud services
- **Sensor Integration**: Combine with other IoT sensors

## Development Environment

The project includes a Python virtual environment (`venv/`) to isolate dependencies. Always activate the virtual environment before development:

```bash
source venv/bin/activate
```

## Contributing

This project was created for the KCDC 2025 conference as an IoT demonstration. Feel free to fork and extend the functionality for your own projects.

## License

This project is provided as an educational example for the KCDC 2025 conference.

## Resources

- [Picamera2 Documentation](https://datasheets.raspberrypi.org/camera/picamera2-manual.pdf)
- [Raspberry Pi Camera Guide](https://www.raspberrypi.org/documentation/accessories/camera.html)
- [KCDC 2025 Conference](https://www.kcdc.info/)