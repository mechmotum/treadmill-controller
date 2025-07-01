# Treadmill Manual Controller

This Arduino program provides manual button control for a treadmill based on the original `bep_code.ino`. It replaces the automatic LIDAR-based control system with simple push-button controls.

## Features

- **Start/Stop Control**: Dedicated buttons to start and stop the treadmill
- **Speed Control**: Buttons to increase/decrease speed in 0.1 km/h increments
- **Speed Range**: 0.5 km/h to 20.0 km/h
- **Serial Communication**: Uses the same treadmill communication protocol as the original
- **Safety Features**: Button debouncing and speed limits

## Hardware Connections

Connect the following buttons to your Arduino:

- **Pin 3**: Start Button (with internal pull-up resistor)
- **Pin 4**: Stop Button (with internal pull-up resistor)  
- **Pin 5**: Speed Up Button (with internal pull-up resistor)
- **Pin 6**: Speed Down Button (with internal pull-up resistor)

### Button Wiring

Each button should be wired as follows:

```
Button Pin → Arduino Digital Pin
Button Ground → Arduino GND
```

The code uses internal pull-up resistors, so no external resistors are needed. Buttons are active LOW (pressed = LOW, released = HIGH).

## Serial Communication

- **Serial1 (19200 baud)**: Communication with treadmill
- **Serial (115200 baud)**: Debug output to serial monitor

## Usage

1. **Upload the code** to your Arduino
2. **Open Serial Monitor** (115200 baud) for debug information
3. **Press Start button** to start the treadmill (starts at 0.5 km/h)
4. **Press Speed Up/Down** buttons to adjust speed in 0.1 km/h increments
5. **Press Stop button** to stop the treadmill

## Operation Notes

- The treadmill must be started before speed can be adjusted
- Speed changes are limited to the range 0.5 - 20.0 km/h
- Button presses are debounced with a 200ms delay
- All button presses are logged to the serial monitor
- The system uses edge detection to prevent multiple commands on held buttons

## Differences from Original Code

This simplified version:

- ✅ Removes complex PID control system
- ✅ Removes LIDAR distance sensing
- ✅ Removes automatic start/stop logic
- ✅ Removes speed sensor reading
- ✅ Adds simple manual button controls
- ✅ Maintains the same treadmill communication protocol
- ✅ Preserves all speed command arrays (0.5-20.0 km/h)

## Troubleshooting

- **No response**: Check serial connections and baud rate (19200)
- **Buttons not working**: Verify pin connections and check serial monitor for debug output
- **Speed not changing**: Ensure treadmill is started before attempting speed changes
- **Multiple commands**: Button debouncing prevents this, but if issues persist, increase `BUTTON_DEBOUNCE_DELAY`

## Serial Monitor Output

The program provides helpful debug output:

```
Treadmill Controller Ready
Controls:
- Pin 3: Start
- Pin 4: Stop  
- Pin 5: Speed Up (+0.1 km/h)
- Pin 6: Speed Down (-0.1 km/h)
Speed range: 0.5 - 20.0 km/h

Treadmill STARTED
Speed: 0.5 km/h
Speed increased to: 0.6 km/h
Speed increased to: 0.7 km/h
Treadmill STOPPED
```

## Safety Considerations

- Always ensure the treadmill emergency stop is accessible
- Test all controls before use
- Monitor the serial output for any unexpected behavior
- The system maintains speed limits to prevent unsafe operation
