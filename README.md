
# Head Tracker Unit

A 3-axis head tracking system using Arduino, MPU6050 gyroscope/accelerometer, servo motors, and OLED display for real-time head movement tracking and mechanical replication.

## Features

- **Real-time head tracking** using MPU6050 6-axis motion sensor
- **3-axis servo control** for pitch, yaw, and roll movements
- **OLED display** showing current angles in real-time
- **Automatic calibration** on startup
- **Smooth servo mapping** from gyroscope angles to servo positions

## Hardware Requirements

### Components
- Arduino Nano (or compatible)
- MPU6050 gyroscope/accelerometer module
- 3x SG90 Servo motors (for up/down, left/right, and roll movements)
- SSD1306 OLED display (128x64)
- Jumper wires and breadboard

### Wiring Diagram

#### MPU6050 Connections
- VCC → 5V
- GND → GND
- SCL → A5 (or SCL pin)
- SDA → A4 (or SDA pin)

#### OLED Display (SSD1306)
- VCC → 5V
- GND → GND
- SCL → A5 (or SCL pin)
- SDA → A4 (or SDA pin)

#### Servo Motors
- **Up/Down Servo (Pitch)** → Pin 2
- **Left/Right Servo (Yaw)** → Pin 3
- **Roll Servo** → Pin 4

All servos:
- Red wire → 5V
- Brown/Black wire → GND
- Orange/Yellow wire → Signal pin

## Software Dependencies

Install the following libraries in Arduino IDE:

```
Wire (built-in)
MPU6050_light
Servo (built-in)
Adafruit_GFX
Adafruit_SSD1306
```

### Installation Instructions

1. Open Arduino IDE
2. Go to **Sketch** → **Include Library** → **Manage Libraries**
3. Search for and install:
   - `MPU6050_light` by rfetick
   - `Adafruit GFX Library`
   - `Adafruit SSD1306`

## Setup and Usage

1. **Hardware Setup**
   - Connect all components according to the wiring diagram
   - Ensure stable power supply for servos
   - Mount MPU6050 securely to the object you want to track

2. **Upload Code**
   - Open `CODE 1.0.cpp` in Arduino IDE
   - Select your board and port
   - Upload the code

3. **Calibration**
   - Keep the MPU6050 steady during startup
   - Wait for "Calibration done!" message in Serial Monitor
   - The system will automatically calibrate offsets

4. **Operation**
   - Move the MPU6050 to see servo motors respond
   - OLED display shows current X, Y, Z angles
   - Servo positions update in real-time

## Code Structure

### Main Functions

- **`setup()`**: Initializes all components and performs calibration
- **`loop()`**: Main execution loop that:
  - Reads MPU6050 data
  - Maps angles to servo positions
  - Updates servo positions
  - Refreshes OLED display

### Angle Mapping

The code maps gyroscope angles to servo positions:

- **X-axis (Pitch)**: -90° to 90° → 0° to 180° servo
- **Z-axis (Yaw)**: -180° to 90° → 0° to 180° servo
- **Y-axis (Roll)**: -90° to 90° → 0° to 180° servo (with safety limits 60°-190°)

### Safety Features

- Roll servo movement is limited to prevent mechanical damage (60°-190° range)
- MPU6050 initialization check with error handling
- Automatic offset calibration for accurate readings

## Customization

### Adjusting Servo Ranges
Modify the `map()` function parameters to change servo movement ranges:

```cpp
int servo_up_down_angle = map(a, -90, 90, 0, 180);
```

### Changing Update Rate
Adjust the delay in the main loop:

```cpp
delay(1); // 1ms delay = ~1000Hz update rate
```

### Display Customization
Modify OLED display parameters in the display section of the loop.

## Troubleshooting

### Common Issues

1. **Servos not moving**
   - Check power supply (servos need adequate current)
   - Verify pin connections
   - Ensure servo library is properly installed

2. **OLED display not working**
   - Check I2C connections (SDA/SCL)
   - Verify OLED address (0x3C is default)
   - Test with I2C scanner sketch

3. **Erratic readings**
   - Recalibrate by restarting the system
   - Keep MPU6050 steady during calibration
   - Check for loose connections

4. **Serial Monitor shows MPU6050 error**
   - Verify MPU6050 connections
   - Check if MPU6050 is properly powered
   - Try different I2C address if needed

## Applications

- **Camera gimbals** for smooth video recording
- **VR/AR head tracking** systems
- **Robotic head** that mimics human movement
- **Motion capture** for animation
- **Educational projects** for learning sensor integration

## License

This project is open source. Feel free to modify and distribute according to your needs.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for improvements.

---

**Note**: This project requires basic knowledge of Arduino programming and electronics. Always double-check connections before powering on to avoid component damage.
