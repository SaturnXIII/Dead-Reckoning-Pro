# Dead Reckoning Pro

*A GPS-free navigation app for Android (BETA) that uses pedestrian dead reckoning (PDR) to track your position when GPS is unavailable. Built with Android, OSMDroid, and sensor fusion algorithms.*

*Created with AI assistance*

---

## 📷 Screenshots

<p align="center">
  <img src="https://github.com/user-attachments/assets/c7cc0cca-6442-4a0f-8756-489710d3d809" width="250" />
  <img src="https://github.com/user-attachments/assets/820db7ab-47c6-4e31-b60d-fb4459e32c40" width="250" />
  <img src="https://github.com/user-attachments/assets/4151b176-e890-4369-a4de-6925e7cf746d" width="250" />

</p>

## ✨ New Features (v2.0)

### 🗺️ Map Markers
- **Add custom markers** with emoji icons and labels
- **18 emoji options**: 📍 📌 🏠 🏢 🍔 🍕 ☕ 🛒 🛑 ⛽ 🏨 🏞 🚗 ✈️ ⭐ ❤️ 🔴 🟢
- **Persistent storage**: Markers are saved and restored between sessions
- **Drag to move**: Long-press and drag markers to reposition

### 🔄 360° Map Rotation
- **Two-finger rotation**: Rotate the map like Google Maps
- **Intuitive gesture**: Place two fingers and rotate
- **Better navigation**: Align map with your direction of travel

### 🗑️ Smart Clear Options
- Clear tracks only
- Clear markers only  
- Clear everything
- Confirmation dialog to prevent accidents

---

## Features

### Core Navigation
- **GPS Tracking**: Accurate GPS positioning when available
- **Dead Reckoning**: Continue tracking when GPS signal is lost
- **Step Counting**: Automatic step detection using accelerometer
- **Heading Estimation**: Sensor fusion of gyroscope + magnetometer for accurate direction
- **Manual Mode**: Manual direction control (turn left/right/around)
- **360° Dial**: Visual compass dial for selecting direction in manual mode

### Data Management
- **Trip History**: Save and view past trips
- **GPX Export**: Export trips in GPX format for use in other apps
- **CSV Export**: Export trip data including all path points
- **Custom Export Location**: Choose where to save exported files

### Background Tracking
- **Foreground Service**: Tracking continues when app is in background
- **Screen Off Support**: Sensors continue collecting data when screen is off
- **Wake Lock**: Prevents device from sleeping during active tracking
- **Switch Apps**: Continue tracking while using other apps

### Calibration
- **GPS Calibration**: Automatic calibration using GPS data to correct drift
- **Magnetometer Calibration**: Built-in compass calibration
- **Step Calibration**: Calibrate step length for accurate distance

---

## How It Works

### Dead Reckoning Algorithm

The app uses **Pedestrian Dead Reckoning (PDR)** to estimate position:

1. **Step Detection**: Uses accelerometer to detect pedestrian steps via peak detection
2. **Heading Estimation**: Combines gyroscope (short-term accuracy) + magnetometer (long-term stability) using a complementary filter
3. **Position Update**: `New Position = Previous Position + Step Length × Heading Vector`

```
x_new = x_old + step_length × sin(heading)
y_new = y_old + step_length × cos(heading)
```

### GPS Calibration

When GPS is available, the app continuously calibrates:
- **Scale Factor**: Ratio of GPS distance to estimated distance
- **Heading Bias**: Difference between compass heading and actual GPS bearing

This correction is applied when GPS is unavailable, significantly improving accuracy.

---

## Installation

### Prerequisites
- Android Studio (Arctic Fox or later recommended)
- Java JDK 11 or later
- Android SDK with API 22+ (minimum), API 34 (target)

### Build Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/SaturnXIII/Dead-Reckoning-Pro
   cd DeadReckoning
   ```

2. **Open in Android Studio**
   - File → Open → Select the project folder
   - Wait for Gradle sync to complete

3. **Configure SDK**
   - Go to File → Project Structure → SDK Location
   - Ensure Android SDK is configured

4. **Build Debug APK**
   - Build → Build Bundle(s) / APK(s) → Build APK(s)
   - Or press `Ctrl+F9` (Windows/Linux) / `Cmd+F9` (Mac)

5. **Install on Device**
   - Enable USB debugging on your Android device
   - Connect device and run from Android Studio
   - Or manually install: `adb install app/build/outputs/apk/debug/app-debug.apk`

### Permissions Required

The app requests these permissions:
- `ACCESS_FINE_LOCATION` - GPS tracking
- `ACCESS_COARSE_LOCATION` - Network-based location
- `ACCESS_BACKGROUND_LOCATION` - Background location
- `FOREGROUND_SERVICE` - Background tracking
- `FOREGROUND_SERVICE_LOCATION` - Location in background
- `WAKE_LOCK` - Prevent device sleep
- `HIGH_SAMPLING_RATE_SENSORS` - High-frequency sensor data
- `ACTIVITY_RECOGNITION` - Step counting
- `POST_NOTIFICATIONS` - Android 13+ notification permission
- `INTERNET` - Map tiles download
- `ACCESS_NETWORK_STATE` - Network status check

---

## Usage Guide

### Starting a Trip

1. Open the app and grant all requested permissions
2. Wait for GPS to lock (status shows "GPS: OK")
3. Tap the **Start** button to begin tracking
4. Walk while the app records your path

### Adding Markers

1. Tap the **+** button (orange) to enter marker mode
2. Tap on the map where you want to place the marker
3. Select an emoji icon from the list
4. Optionally enter a label for the marker
5. Tap **Confirm** to save

### Rotating the Map

1. Place **two fingers** on the map
2. Rotate in a circular motion
3. The map will rotate 360°
4. Double-tap to reset to North-up

### Using Manual Mode

1. Tap **Mode: Auto** to switch to Manual mode
2. Use arrow buttons to turn left/right (90°) or U-turn
3. Or tap the **compass icon** to open the 360° dial
4. Drag the dial to select your exact heading, then confirm

### When GPS is Unavailable

1. Tap **No GPS** button to switch to dead reckoning mode
2. The app will continue tracking using steps + heading
3. Use manual controls to indicate turns
4. When GPS returns, tap **No GPS** again to re-enable GPS tracking

### Viewing Past Trips

1. Navigate to **History** from the main menu
2. Tap a trip to view details
3. Tap **View on Map** to see the trip path
4. Use export options to save as GPX or CSV

### Exporting Data

From History screen:
- **Export CSV (choose folder)** - Select custom save location
- **Export GPX (choose folder)** - Select custom save location  
- **Export to Downloads** - Save directly to Downloads folder

### Clearing Data

1. Tap the **trash icon** (red) in the bottom right
2. Choose an option:
   - **Tracks only**: Clear current path
   - **Markers only**: Delete all saved markers
   - **Everything**: Clear both tracks and markers
3. Confirm your choice

---

## Screenshots Description

<!-- Add descriptions of your screenshots here -->

| Screen | Description |
|--------|-------------|
| Map View | Main tracking screen with GPS status, steps, distance, heading |
| Markers | Custom emoji markers on the map with labels |
| History | List of saved trips with export options |
| Calibration | Step length calibration tools |

---

## Project Structure

```
app/src/main/java/nisargpatel/deadreckoning/
├── activity/           # UI Activities and Fragments
│   ├── MapFragment.java       # Main map view with tracking + markers
│   ├── MainNavigationActivity.java  # Activity wrapper
│   ├── HistoryActivity.java  # Trip history list
│   ├── GuideActivity.java    # Help & guide
│   └── ...
├── sensor/             # Core sensor processing
│   ├── DeadReckoningEngine.java    # Position calculation
│   ├── PreciseHeadingEstimator.java # Sensor fusion
│   └── GPSCalibrator.java         # GPS correction
├── stepcounting/       # Step detection algorithms
├── orientation/        # Orientation estimation
├── model/              # Data models (Trip, Marker, TurnEvent)
├── storage/            # Trip & Marker persistence
│   ├── TripStorage.java     # Trip data storage
│   └── MarkerStorage.java   # Marker data storage
├── service/            # Background tracking service
└── view/              # Custom views (DegreeDialView)

app/src/main/res/
├── layout/             # XML layouts
├── drawable/           # Icons and graphics
├── values/             # Strings, colors, styles
└── ...
```

---

## Key Classes

| Class | Description |
|-------|-------------|
| `DeadReckoningEngine` | Core PDR algorithm, combines steps + heading |
| `PreciseHeadingEstimator` | Sensor fusion (gyro + magnetometer + Kalman filter) |
| `GPSCalibrator` | Calculates scale/heading correction from GPS |
| `EnhancedStepCounter` | Peak detection step counting |
| `TrackingService` | Foreground service for background tracking |
| `DegreeDialView` | Custom 360° compass dial view |
| `Trip` | Trip data model with GPX/CSV export |
| `Marker` | Custom marker model with emoji + label |
| `MarkerStorage` | JSON persistence for markers |

---

## Sensors Used

| Sensor | Purpose |
|--------|---------|
| `TYPE_GRAVITY` | Stable gravity vector for orientation |
| `TYPE_MAGNETIC_FIELD` | Compass heading |
| `TYPE_GYROSCOPE` | Rate of turn for short-term heading |
| `TYPE_LINEAR_ACCELERATION` | Step detection |
| `FusedLocationProvider` | GPS positioning |

---

## Technical Details

- **Map Provider**: OSMDroid (OpenStreetMap)
- **Location**: Google Play Services FusedLocationProvider
- **Matrix Library**: EJML for calculations
- **Min SDK**: 22 (Android 5.1)
- **Target SDK**: 34 (Android 14)

---

## Credits & License

**Original Project**: [nisargnp/DeadReckoning](https://github.com/nisargnp/DeadReckoning)

**Fork & Modifications**: https://github.com/SaturnXIII/Dead-Reckoning-Pro

**Libraries Used**:
- OSMDroid (OpenStreetMap)
- Google Play Services Location
- Material Components for Android
- EJML (Efficient Java Matrix Library)
- AChartEngine

**License**: Open Source - Feel free to contribute and modify!

---

## Troubleshooting

### Steps not being counted
- Ensure the app has activity recognition permission
- Keep phone in pocket or hand while walking
- Try calibrating step length in Settings

### Heading drifts
- Calibrate magnetometer (go to Calibration in menu)
- Keep phone away from metal objects
- Use manual mode for better control

### GPS not working
- Ensure location permission is granted
- Check GPS is enabled in phone settings
- Wait for initial lock (may take 30-60 seconds)

### App crashes on export
- Check storage permission
- Try "Export to Downloads" option
- Ensure enough free storage space

### Marker not appearing
- Make sure you've selected an emoji and confirmed
- Try zooming in on the map

---

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

**Note**: This app is for educational and research purposes. GPS should be used as the primary navigation source when available. Dead reckoning provides estimates that may drift over time, especially without regular GPS calibration.
