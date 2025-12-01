# 🗑️ AR Trash Sorting Game

An immersive Augmented Reality educational game that teaches proper waste segregation through interactive gameplay. Point your camera at a marker, select trash types, and sort them into the correct bins to score points!

![AR Trash Sorting Game](https://img.shields.io/badge/AR-WebXR-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![Status](https://img.shields.io/badge/status-active-success)

## 📋 Overview

**AR Trash Sorting Game** is a web-based augmented reality application designed to educate users about waste management in an engaging, gamified format. Using marker-based AR technology, the game projects 3D trash bins into the real world, allowing players to practice sorting different types of waste correctly.

The game combines entertainment with environmental education, making learning about recycling and waste segregation fun and memorable. It's perfect for schools, environmental awareness campaigns, and anyone interested in sustainability.

## ✨ Key Features

- **🌍 World-Anchored AR**: Trash bins persist in physical space even when the marker is lost from view
- **📱 Marker-Based Tracking**: Uses image recognition to accurately place AR objects in the real world
- **🎮 Interactive Gameplay**: Click buttons to select trash, then tap bins to sort them
- **🎯 Real-Time Scoring**: Earn +10 points for correct sorting, -5 points for mistakes
- **🔄 Recenter Functionality**: Reposition bins by rescanning the marker
- **📊 Visual Feedback**: Animated trash throwing with rotation effects and color-coded feedback messages
- **🎨 Three Waste Categories**: Paper, Organic, and Inorganic waste types
- **📲 Mobile & Desktop Compatible**: Works on smartphones, tablets, and desktop browsers with webcam

## 🛠️ Technology Stack

### Core Technologies

| Technology | Version | Purpose |
|------------|---------|---------|
| **A-Frame** | 1.4.2 | WebXR framework for building VR/AR experiences |
| **MindAR** | 1.2.2 | Computer vision library for image tracking |
| **Three.js** | (bundled) | 3D graphics rendering engine |
| **HTML5** | - | Structure and DOM manipulation |
| **CSS3** | - | Styling and animations |
| **JavaScript (ES6)** | - | Game logic and interactivity |

### AR & 3D Technologies

- **WebXR Device API**: Browser API for AR/VR experiences
- **GLB/GLTF Models**: 3D models for trash items and bins
- **Image Tracking**: Compiled `.mind` files for efficient marker detection
- **World Anchoring System**: Custom implementation using Three.js matrix decomposition

### Libraries & Frameworks

```html
<script src="https://aframe.io/releases/1.4.2/aframe.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/mind-ar@1.2.2/dist/mindar-image-aframe.prod.js"></script>
```

## 🎮 Gameplay Mechanics

### How to Play

1. **📸 Scan the Marker**
   - Open the game in a web browser
   - Allow camera permissions when prompted
   - Point your camera at the printed `targets.png` marker
   - Wait for the AR scene to load

2. **🗑️ Select Trash Type**
   - Three buttons appear at the bottom: Paper Waste, Organic Waste, Inorganic Waste
   - Click one button to spawn that trash type
   - The trash appears floating in front of your camera view

3. **👆 Sort Into Bins**
   - Three 3D bins appear anchored to the marker:
     - **Blue Bin** (Left): Paper Waste
     - **Green Bin** (Center): Organic Waste
     - **Red Bin** (Right): Inorganic Waste
   - Tap/click the correct bin to throw the trash

4. **🎯 Score Points**
   - **Correct match**: +10 points, green "CORRECT! +10" message
   - **Wrong match**: -5 points, red "WRONG! -5" message
   - Try to maximize your score!

5. **🔄 Recenter (Optional)**
   - If bins drift from their position, click the "📍 RECENTER" button
   - Rescan the marker to reposition bins

### Waste Categories

| Waste Type | Examples | Bin Color |
|------------|----------|-----------|
| **Paper** | Cardboard, newspapers, documents, magazines | 🔵 Blue |
| **Organic** | Food scraps, fruit peels, vegetable waste, leaves | 🟢 Green |
| **Inorganic** | Plastic bottles, cans, glass, metal, packaging | 🔴 Red |

## 🔬 AR Technology Explained

### Marker-Based AR

The game uses **marker-based augmented reality**, where a specific image (the marker) serves as an anchor point for virtual objects. Here's how it works:

1. **Marker Detection**
   - The camera feed is analyzed frame-by-frame
   - MindAR's computer vision algorithms search for the marker pattern
   - When found, the marker's position and orientation are calculated

2. **3D Object Placement**
   - Virtual bins are positioned relative to the marker
   - Three.js handles 3D rendering and transformations
   - A-Frame provides the WebXR interface layer

3. **World Anchoring**
   - On first detection, the system captures the marker's world-space position
   - Objects are "locked" to this position using matrix decomposition
   - Bins persist even when the marker leaves the camera view
   - This creates a more stable, realistic AR experience

### Technical Implementation

```javascript
// World anchor system captures marker position in 3D space
marker.object3D.matrixWorld.decompose(
  markerWorldPosition,
  markerWorldQuaternion,
  markerWorldScale
);

// Objects are cloned to a persistent group
persistentGroup.object3D.position.copy(markerWorldPosition);
persistentGroup.object3D.quaternion.copy(markerWorldQuaternion);
```

## 📁 Project Structure

```
FP-XR-NEW-main/
├── index.html              # Main application file (all-in-one)
├── README.md               # This file
├── assets/
│   ├── targets.mind        # Compiled marker data for MindAR
│   ├── targets.png         # Printable AR marker image
│   └── models/
│       ├── bin-kertas.glb      # Paper waste bin 3D model
│       ├── bin-organik.glb     # Organic waste bin 3D model
│       ├── bin-anorganik.glb   # Inorganic waste bin 3D model
│       ├── trash-kertas.glb    # Paper trash 3D model
│       ├── trash-organik.glb   # Organic trash 3D model
│       └── trash-anorganik.glb # Inorganic trash 3D model
└── .git/                   # Git repository
```

### File Descriptions

- **index.html**: Complete standalone application with embedded CSS and JavaScript
- **targets.mind**: Pre-compiled marker file for fast image tracking
- **targets.png**: Source marker image that users scan with their camera
- **GLB models**: Optimized 3D models in GL Transmission Format

## 🚀 Getting Started

### Prerequisites

- Modern web browser with WebXR support (Chrome, Edge, Firefox, Safari)
- Webcam or smartphone camera
- Local web server (required for camera access)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Winskiii/Bin.git
   cd Bin
   ```

2. **Print the AR marker**
   - Open `assets/targets.png`
   - Print it on A4 paper or display it on another screen

3. **Start a local server**
   
   **Option A: Python**
   ```bash
   python -m http.server 8080
   ```
   
   **Option B: Node.js (http-server)**
   ```bash
   npx http-server -p 8080
   ```
   
   **Option C: VS Code Live Server**
   - Install Live Server extension
   - Right-click `index.html` → "Open with Live Server"

4. **Open in browser**
   ```
   http://localhost:8080
   ```

5. **Grant camera permissions** when prompted

6. **Point camera at marker** and start playing!

## 🎯 Usage Guide

### For Desktop/Laptop

1. Open the game URL in Chrome or Edge
2. Allow webcam access
3. Hold the printed marker in front of your webcam
4. Use mouse clicks to select trash and bins
5. View the score in the top-left corner

### For Mobile Devices

1. Open the game URL in mobile browser (Chrome/Safari)
2. Allow camera access
3. Point phone camera at the marker
4. Tap buttons to select trash
5. Tap bins to throw trash
6. Bins stay anchored in space as you move around

### Troubleshooting

**Camera not working?**
- Ensure you're using HTTPS or localhost (camera access requires secure context)
- Check browser permissions for camera access
- Try a different browser

**Marker not detecting?**
- Ensure good lighting conditions
- Keep marker flat and fully visible
- Avoid shadows or glare on the marker
- Try moving camera closer or further away

**Models not loading?**
- Check browser console for errors
- Ensure all GLB files are in `assets/models/` folder
- Verify local server is running

## 🎨 Customization

### Adding New Trash Types

1. Add GLB model to `assets/models/`
2. Update the assets section in `index.html`:
   ```html
   <a-asset-item id="trash-newtype-asset" src="./assets/models/trash-newtype.glb"></a-asset-item>
   ```
3. Add to `trashConfig`:
   ```javascript
   const trashConfig = {
     newtype: { model: '#trash-newtype-asset', scale: '0.5 0.5 0.5' }
   };
   ```
4. Add button in UI container

### Changing Scoring System

Edit the score values in `handleSuccess()` and `handleFail()` functions:

```javascript
function handleSuccess() {
  currentScore += 10;  // Change this value
  // ...
}

function handleFail() {
  currentScore -= 5;   // Change this value
  // ...
}
```

### Styling Modifications

All CSS is embedded in `<style>` tags in `index.html`. Modify colors, sizes, and animations directly:

```css
.btn-kertas { 
  background-color: #3b82f6; /* Change button color */
}
```

## 🌐 Browser Compatibility

| Browser | Desktop | Mobile | Notes |
|---------|---------|--------|-------|
| Chrome | ✅ | ✅ | Best performance |
| Edge | ✅ | ✅ | Recommended |
| Firefox | ✅ | ⚠️ | Some AR features limited |
| Safari | ⚠️ | ✅ | iOS Safari works well |
| Opera | ✅ | ✅ | Chromium-based |

**Legend**: ✅ Full support | ⚠️ Partial support | ❌ Not supported

## 📊 Performance Optimization

- **GLB Models**: Compressed 3D models for faster loading
- **Asset Preloading**: A-Frame asset management system
- **Efficient Tracking**: MindAR's optimized computer vision
- **Minimal Dependencies**: All-in-one file structure
- **Lazy Loading**: Event-driven initialization
