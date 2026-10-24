
# Mood-Link Plus — Facial Expression Recognition & Eye Activity Analysis

**Mood-Link Plus** is a webcam-based AI application designed to recognize facial expressions, display emotion-related suggestions, and visualize facial and eye landmarks in real time. The project explores how computer vision can support emotional awareness through a simple, interactive web interface.

The application uses face detection and facial-expression analysis to identify the most likely expression from a webcam frame. It also includes a one-time detection option and a temporary, in-memory database for viewing recent emotion-detection records.

> **Project type:** AI / Computer Vision / Web Application  
> **Status:** Educational prototype  
> **Repository:** [Mood-Link-off](https://github.com/hima-prog/Mood-Link-off)

## 1. Problem Statement

Understanding facial expressions and non-verbal cues can be useful when exploring human-computer interaction. However, interpreting these cues manually can be subjective and may require continuous attention.

This project explores a computer-vision-based approach to detecting facial expressions through a webcam and presenting the output in an understandable format. It aims to demonstrate how facial-expression analysis can be combined with contextual suggestions and a lightweight interface.

The project also explores visualizing eye landmarks as a starting point for further development in eye-activity and fatigue-awareness applications.

## 2. Proposed Solution

Mood-Link Plus provides a browser-based interface that accesses a user's webcam with permission and analyzes the video feed using a pre-trained facial-analysis model.

The application includes:

- **Facial-expression recognition:** Identifies the most likely expression from the detected face.
- **Face landmark visualization:** Uses facial landmarks to support visual analysis.
- **Eye mode:** Highlights the detected eye regions and displays the current expression.
- **Emotion-related suggestions:** Presents suggestions associated with the detected expression.
- **One-time detection:** Allows the user to capture and freeze a detection result.
- **Detection history:** Displays recent emotion records with timestamps and confidence values using an in-memory SQL.js database.
- **Camera controls:** Includes a camera restart control and camera-permission handling.

## 3. Methodology / Workflow

The application follows this workflow:

1. **Initialize the application:** Load the facial-analysis models and initialize the SQL.js database.
2. **Request camera access:** Use the browser's webcam API after the user grants permission.
3. **Detect the face:** Apply the Tiny Face Detector model to the video stream.
4. **Identify facial landmarks:** Detect facial landmark points, including those around the eyes.
5. **Analyze facial expressions:** Use the face-expression model to estimate probabilities for supported expression categories.
6. **Select the leading expression:** Choose the expression with the highest estimated probability, subject to the code's confidence threshold.
7. **Display the result:** Show the predicted expression, confidence percentage, and related suggestions.
8. **Record detection history:** In continuous mode, log eligible results to the in-memory database and display recent records.

### Workflow Overview

`Webcam → Face Detection → Facial Landmarks → Expression Analysis → Result & Suggestions → Temporary History`

## 4. Technologies Used

| Technology | Purpose |
|---|---|
| HTML5 | Structures the web application |
| CSS3 | Styles the interface and visual elements |
| JavaScript | Implements detection logic, controls, and UI updates |
| face-api.js | Performs face detection, facial landmark detection, and expression analysis |
| Tiny Face Detector | Detects faces in video frames |
| Face Landmark 68 Net | Identifies facial landmark points |
| Face Expression Net | Estimates facial-expression categories |
| Web Media API (`getUserMedia`) | Requests webcam access |
| SQL.js | Provides SQLite-compatible, in-memory data storage |
| CDN-hosted resources | Loads the required libraries and model files |

## 5. Implemented Features

### 5.1 Facial Expression Recognition

The application uses face-api.js to estimate seven expression categories:

- Happy
- Sad
- Angry
- Fearful
- Surprised
- Disgusted
- Neutral

The interface displays the leading predicted expression and its confidence percentage.

**Important:** The output represents a model prediction based on visible facial patterns. It does not establish a person's actual emotional state.

### 5.2 Face and Eye Modes

The interface provides two modes:

- **Face Mode:** Focuses on face detection and expression analysis.
- **Eye Mode:** Visualizes the detected eye regions using facial landmarks and displays the leading expression.

Eye-region visualization is not the same as validated eye-closure measurement or fatigue detection.

### 5.3 Emotion-Related Suggestions

The application maps predicted expression categories to predefined suggestions. For example, it may display a breathing exercise, a short break, or another general well-being suggestion.

These messages are rule-based suggestions associated with the model output; they are not personalized medical or psychological recommendations.

### 5.4 One-Time Detection

The One-time Detect control allows the user to freeze the video at the next eligible detection result for closer inspection.

### 5.5 Detection History

The application uses SQL.js to create a `mood_logs` table containing:

- Record ID
- Predicted expression
- Confidence value
- Timestamp

The interface displays the five most recent records.

The database is initialized in memory, so the history is temporary and is not automatically persisted across page reloads.

### 5.6 Camera Controls

The application includes camera status indicators, a restart control, and a message when camera access is denied.

## 6. Project Structure

```text
Mood-Link-off/
│
├── index.html    # Web application source
├── code.txt      # Copy of the application code
└── README.md     # Project documentation
```

The `index.html` file contains the web application's HTML structure, CSS styling, and JavaScript implementation. The `code.txt` file contains the corresponding source code for reference.

## 7. How to Run the Project

### Prerequisites

- A modern web browser, such as Google Chrome.
- A working webcam.
- An active internet connection to load the CDN-hosted libraries and facial-analysis model files.
- Permission to access the webcam.

### Steps

1. Open the [Mood-Link-off repository](https://github.com/hima-prog/Mood-Link-off).
2. Download the repository using **Code → Download ZIP**, or clone it:

   ```bash
   git clone https://github.com/hima-prog/Mood-Link-off.git
   ```

3. Open the project folder in Visual Studio Code.
4. Open `index.html` using a local development server, such as the **Live Server** extension in VS Code.
5. Open the local application URL in your browser.
6. Allow camera access when prompted.
7. Wait for the models and database to initialize.
8. Position your face in front of the webcam and observe the predicted expression.
9. Switch between Face Mode and Eye Mode, try One-time Detect, and inspect the detection-history table.

**Note:** If the webcam does not start when opening the HTML file directly, use a local development server. Browser camera APIs generally require a secure context, such as `localhost`, or HTTPS. The application also requires internet access to load its external dependencies.

## 8. Expected Output

When the required resources load successfully and a face is visible, the interface is designed to display:

- The live webcam feed.
- Face or eye-region visualizations, depending on the selected mode.
- The leading predicted expression and its confidence percentage.
- Suggestions associated with the predicted expression.
- Recent detection records in the history table.

Actual output and detection quality depend on lighting, camera quality, face position, model behavior, and successful loading of external resources.

## 9. Limitations

- Facial-expression predictions may be incorrect or inconsistent.
- Lighting, camera angle, occlusion, and individual differences can affect detection.
- Facial expressions alone cannot reliably establish a person's internal emotional state.
- Eye landmark visualization does not by itself establish fatigue, drowsiness, or sleepiness.
- The current database is in-memory; records are lost when the page is reloaded.
- External libraries and model files require network access.
- The project has not been documented with a formal accuracy evaluation or validated clinical testing.

## 10. Future Improvements

Potential improvements include:

- Evaluate expression predictions on a representative test dataset and report appropriate metrics.
- Improve error handling and provide clearer model-loading and camera-status messages.
- Add persistent storage if users need detection history across sessions.
- Improve accessibility, responsive design, and user controls.
- Develop and validate eye-closure or blink-duration measurements before making fatigue-related claims.
- Add explicit privacy controls and clearer information about how camera frames and detection records are handled.
- Evaluate model performance across different lighting conditions, camera positions, and user groups.

## 11. Learning Outcomes

This project provides practical experience with:

- Integrating a pre-trained computer-vision model into a web application.
- Accessing webcam streams through browser APIs.
- Understanding face detection, facial landmarks, and expression estimation.
- Updating a user interface dynamically with JavaScript.
- Using a lightweight SQLite-compatible database in the browser.
- Handling asynchronous resource loading and camera permissions.
- Considering privacy, responsible AI, and the limitations of model predictions.

## 12. Privacy and Responsible Use

Mood-Link Plus is an educational prototype, not a medical diagnostic system or a reliable measure of a person's mental state.

Use the camera only with the user's informed permission. Avoid using expression predictions to make consequential decisions about a person. The current implementation initializes its detection-history database in memory; this does not, by itself, guarantee that all camera data or processing remains local, particularly because external libraries and model files are loaded from CDNs.

## 13. Project Status

Mood-Link Plus is maintained as a learning and demonstration project. The repository documents a browser-based implementation of facial-expression estimation, eye-landmark visualization, expression-associated suggestions, and temporary detection logging.

Further testing, validation, and improvements are needed before treating it as a production-ready application.

---

**Developed as an AI and computer-vision learning project.**
