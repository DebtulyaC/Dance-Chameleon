# Dance Chameleon

Dance Chameleon is a browser-based pose-matching game that uses your webcam to track body movement in real time. The objective is simple: watch the target pose, reproduce it in front of the camera, and clear each challenge as quickly and accurately as possible.

Live application: https://dance-chameleon.onrender.com

## Overview

Dance Chameleon combines computer vision, browser APIs, and game mechanics to create an interactive webcam-based experience.

During a run, the player:

1. Enters a dancer name.
2. Selects a tracking mode.
3. Grants camera access.
4. Receives a sequence of target poses.
5. Matches each pose using their upper-body movement.
6. Maintains at least 80% similarity to clear a pose.
7. Completes five poses to finish the run.
8. Reviews total time, average accuracy, and poses cleared.
9. Saves the result to the leaderboard.

The game is designed around quick feedback and simple controls, so it can be played directly from a modern web browser without installing a separate application.

The application is deployed as a web service on Render.

## Features

- Real-time webcam-based pose tracking
- Two tracking modes:
  - Head to Hips
  - Head to Chest
- Five-pose runs
- Live pose similarity percentage
- 80% similarity threshold for clearing a pose
- Timed gameplay
- Pose library
- Instructions and guided gameplay flow
- Player name selection
- Run completion summary
- Average accuracy tracking
- Fastest-time leaderboard
- Option to change dancer name
- Option to change pose during gameplay
- Play Again functionality
- Responsive browser-based interface
- No separate desktop application required

## How to Play

### 1. Set up your dancer

Open the application and enter a dancer name.

A short name or alias can be used.

### 2. Choose a tracking mode

Select one of the available tracking modes:

- Head to Hips
- Head to Chest

### 3. Allow camera access

The game requires access to your webcam.

For the best results:

- Keep your upper body visible.
- Position the camera so you remain comfortably inside the frame.
- Make sure the room has sufficient lighting.
- Avoid having your body blend into the background.
- Keep your camera stable during gameplay.

### 4. Study the target pose

Each level presents a target pose.

Use the countdown period to understand the required arm position before the timer starts.

### 5. Match the pose

Once the level begins, reproduce the target pose in front of the camera.

The game displays a live Match percentage indicating how closely your movement matches the target.

### 6. Clear the level

A pose is cleared when the match reaches at least:

```text
80%
```

The pose must also be held steadily for a short period.

The faster you reach the required similarity, the better your final time.

### 7. Complete the run

Each run contains five poses.

After all five poses are cleared, the game displays:

- Total Time
- Average Accuracy
- Poses Cleared

You can then save the run and view the leaderboard or start another run.

## Scoring

Dance Chameleon evaluates how closely the player's movement matches the target pose.

The primary gameplay threshold is:

```text
80% similarity
```

The final results include:

### Total Time

The amount of time required to clear all poses.

### Average Accuracy

The average matching accuracy across the completed poses.

### Poses Cleared

The number of successfully completed poses out of five.

The leaderboard is ranked primarily by the fastest total time across completed runs.

## Pose Matching

The game uses pose-tracking data from the webcam to compare the player's body position with the target pose.

The matching system focuses on the upper body because the gameplay is based primarily on reproducing arm and shoulder positions.

A simplified representation of the process is:

```text
Webcam
   |
   v
Pose Detection
   |
   v
Body Landmarks
   |
   v
Pose Comparison
   |
   v
Similarity Percentage
   |
   v
80% Threshold
   |
   +---- Not reached ----> Keep adjusting
   |
   +---- Reached --------> Hold pose
                              |
                              v
                         Pose cleared
```

## Application Flow

```text
Player Setup
     |
     v
Tracking Mode
     |
     v
Main Menu
     |
     +------------------+
     |                  |
     v                  v
Instructions       Pose Library
     |                  |
     +--------+---------+
              |
              v
          Start Game
              |
              v
        Target Pose
              |
              v
       Webcam Tracking
              |
              v
       Live Match Meter
              |
              v
       Clear at 80%+
              |
              v
         Next Pose
              |
              v
       Five Poses Done
              |
              v
         Run Complete
              |
              v
       Save / Leaderboard
```

## Tech Stack

| Technology | Purpose |
|---|---|
| HTML5 | Application structure |
| CSS3 | Layout, styling, animations and responsive design |
| JavaScript | Game logic, state management and interaction |
| MediaPipe Pose | Real-time human pose estimation |
| WebRTC / getUserMedia | Webcam access |
| Canvas API | Camera and pose visualization |
| Web Audio API | Browser-based sound effects |
| SVG | Target-pose graphics |
| Render | Application deployment |

## Project Structure

The project is intentionally lightweight and can be run as a web application without a traditional backend architecture.

A typical project structure is:

```text
Dance Chameleon/
|
|-- index.html
|-- assets/
|   |-- pose and meme images
|   |-- other visual assets
|
|-- README.md
```

If your repository uses a different asset structure, keep the README synchronized with the actual repository layout.

## Running the Project Locally

Clone the repository:

```bash
git clone <repository-url>
```

Move into the project directory:

```bash
cd <repository-directory>
```

Because the application uses browser APIs such as webcam access, running it through a local HTTP server is recommended.

### Using Python

If Python is installed:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

### Using VS Code

If you use Visual Studio Code, you can also run the project through a local development server such as Live Server.

Open the project directory, start the server, and open the generated local URL in your browser.

## Deployment

The live version of Dance Chameleon is deployed on Render:

https://dance-chameleon.onrender.com

The project is suitable for deployment as a web application because the gameplay runs in the browser and does not require a desktop installation.

When deploying a webcam-based application, make sure the production site is served over HTTPS. Modern browsers generally restrict webcam access to secure contexts, with localhost being the main development exception.

## Browser Requirements

Use a modern browser with support for:

- Webcam access through `getUserMedia()`
- JavaScript ES6+
- Canvas
- Web Audio API
- Local browser storage or file-based leaderboard functionality used by the application
- Modern CSS
- WebAssembly or other browser features required by the pose-tracking dependency

Recommended browsers include current versions of:

- Google Chrome
- Microsoft Edge
- Mozilla Firefox
- Safari

Camera permissions must be granted for pose tracking to work.

## Privacy

Dance Chameleon requires webcam access because the game needs real-time visual information to determine the player's pose.

The camera is used for gameplay and pose detection. The application does not require the player to create an account before playing.

Users should review the project's implementation and hosting configuration before deploying a modified version in environments with additional privacy or security requirements.

## Leaderboard

The game includes a leaderboard that ranks completed runs by fastest total time.

Leaderboard information includes:

| Field | Description |
|---|---|
| Dancer | Player's selected name |
| Time | Total time for the completed run |
| Accuracy | Average pose accuracy |
| Poses | Number of poses cleared |

The application also provides an option to clear the leaderboard.

## Gameplay Screens

The application currently includes the following main sections:

### Player Setup

Used to enter the dancer name and select the tracking mode.

### Main Menu

Provides access to:

- Start Game
- Instructions
- Leaderboard
- Change dancer name

### Pose Library

Provides access to the available target-pose content.

### How To Play

Explains the gameplay process and the 80% matching requirement.

### Game Screen

Displays:

- Current pose number
- Target pose
- Player camera view
- Elapsed time
- Match percentage
- Number of poses cleared
- Pose controls

### Run Complete

Displays:

- Total Time
- Average Accuracy
- Poses Cleared

The player can then save the run or play again.

### Leaderboard

Displays saved rankings and provides a leaderboard-clearing option.

## Known Limitations

- Pose detection quality depends on camera quality, lighting, framing and body visibility.
- Webcam permissions are required for gameplay.
- The game is primarily designed around upper-body pose matching.
- Different camera positions and body proportions can affect matching behavior.
- Browser support and privacy restrictions can affect webcam functionality.
- The current leaderboard implementation is intended for the deployed application's supported storage workflow rather than a full account-based global ranking system.
- The pose-tracking dependency may require network access depending on how its assets are included in the deployment.

## Future Improvements

Possible improvements include:

- Global online leaderboard
- User accounts
- More target poses
- Additional difficulty levels
- Full-body pose matching
- More advanced pose similarity algorithms
- Multiplayer gameplay
- Personal performance statistics
- Achievement system
- Streaks and challenges
- Better mobile support
- Offline support
- Custom pose creation
- Improved accessibility
- Automated testing
- Performance optimizations for low-end devices

## Contributing

Contributions and suggestions are welcome.

To contribute:

```bash
git clone <repository-url>
cd <repository-directory>
```

Create a branch:

```bash
git checkout -b feature/your-feature
```

Make your changes, test the application locally, and commit them:

```bash
git add .
git commit -m "Add your feature"
git push origin feature/your-feature
```

Then open a Pull Request on GitHub.

Some areas where contributions could be useful:

- New poses
- Better pose matching
- UI improvements
- Mobile compatibility
- Accessibility
- Performance optimization
- New game modes
- Leaderboard improvements
- Documentation

## License

No license is currently specified for the project.

If you intend to make the repository open source, add a `LICENSE` file with the license you want to use.

## Author

Debtulya Chakraborty

## Links

Live Demo: https://dance-chameleon.onrender.com

---

Dance Chameleon is a small experiment in combining computer vision, browser technology and game design into an interactive webcam experience.
