# WebXR AR Heart Rate Panel Demo

This project demonstrates a **WebXR AR experience** where a floating **heart rate panel** is placed on real-world surfaces using **hit-test AR**. The panel includes a normalized heart rate curve and a last-point indicator, and it is fully visible from all sides. The line is always in front of the panel, and the entire widget floats slightly above the surface.

---

## Features

- Markerless AR using **WebXR hit-test**.
- Panel with **double-sided background**.
- Normalized heart rate curve with **last-point indicator**.
- Curve always in front of the panel (prevents clipping).
- Widget floats slightly above the detected surface.
- Fully self-contained using **CDN imports** (`three.js` and `ARButton`).
- Compatible with **Chrome on Android** and **WebXR simulators** on desktop.

---

## How it works

1. **Hit-Test AR:**  
   The app uses the WebXR `hit-test` feature to detect a flat surface in the environment.

2. **Panel and Chart:**  
   - A `PlaneGeometry` panel is created as a semi-transparent background (`DoubleSide`) and serves as the widget.
   - Heart rate data is simulated and normalized to the panel’s height so it always fits within the widget.

3. **Curve Placement:**  
   - The heart rate line and last-point indicator are grouped together as a child of the panel.
   - This group is offset slightly along the panel’s normal (local z-axis) so it **always appears in front of the panel**.
   - The entire widget group is slightly raised above the detected surface (`yOffset`) to float over the ground.

4. **Interactivity:**  
   - Users tap the screen on a detected surface to place the widget.
   - The reticle shows where the widget will appear.

---

## Running Locally

WebXR requires either **HTTPS** or `localhost` for camera access. You **cannot open the HTML file via `file://`**.

### Option 1: Using Python

```bash
# Navigate to your project folder
cd path/to/project

# Python 3.x
python3 -m http.server 8000


## Option 1: Using Chrome
1. Open Chrome and visit: [http://localhost:8000](http://localhost:8000)

## Option 2: Using Node.js
1. Install `http-server` globally:
  ```bash
  npm install -g http-serverNavigate to your project directory:cd path/to/project```

Start the server on port 8080:http-server -p 8080

Open Chrome and visit: http://localhost:8080Option 3: Using VS Code Live ServerInstall the Live Server extension in VS Code.Right-click index.html and select Open with Live Server.
It will serve the project at something like: http://127.0.0.1:5500/index.html

Using WebXR Simulator (Desktop Chrome)If you don’t have a mobile device, you can use the WebXR Emulator extension for Chrome:Install the WebXR Emulator Extension.Start the local server.Enable the emulator and simulate an AR device.Use your mouse to “tap” and place the AR widget.Deploying to GitHub / GitLab PagesGitHubCreate a new repository and push your project files (index.html, README.md, etc.).Go to Settings → Pages.Under Build and deployment, select Deploy from a branch.Choose:
Branch: main (or your default)
Folder: / (root)

Save and wait a few minutes.
Your AR demo will be available at:https://<username>.github.io/<repository-name>/

GitLabCreate a new repository and push your project files.Go to Settings → Pages.Configure a .gitlab-ci.yml (optional if using the root folder). A minimal example:pages:
 stage: deploy
 script:
   - mkdir public
   - cp -r * public
 artifacts:
   paths:
     - public

Commit and push.After the pipeline runs, GitLab Pages will provide a URL like:https://<username>.gitlab.io/<project-name>/NotesWorks best on Android Chrome or devices with WebXR support.On iOS, you may need WebXR bridge apps (like iQ3Connect) since Safari does not natively support WebXR.All assets are loaded via CDN, so you don’t need any build step.
