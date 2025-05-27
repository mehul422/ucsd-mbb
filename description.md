# Success Prediction from Duke v. Auburn Game Film
Hello Eclipse Team,

My name is Mehul Verma, a aspiring data scientist in his 2nd year majoring in Data Science concentration in ML and minoring in cognitive science/neuro.

This project is a story in and of itself: it transforms raw basketball game footage into a complete analytics pipeline using computer vision, statistical modeling, and visual storytelling, culminating in a working model for predicting shot success based on player movement and shot context.

## 📦 Step 1: Dataset Creation with YOLOv8 and Roboflow
The foundation of this project began with extracting frames from a full game video, which was given to us in the starter repo:
DukeAuburn.mp4, a fast-paced NCAA basketball matchup between two of the hottest teams in the college scene this past season.

Firstly, we performed frame extraction, where the video was broken down into thousands of labeled images through a free program called RoboFlow, which is also machine learning friendly.

Roboflow then constructed bounding boxes, which were manually drawn around the basketball in each frame by yours truly, creating a custom-labeled YOLOv8 dataset that I can start coding with

Switching gears over to VSCodem, I built a YOLOv8 object detection model, which was trained over 30 epochs using the Roboflow-generated dataset, resulting in a specialized detector for tracking the basketball during live play.

## Step 2: YOLOv8 Inference on Full Game Footage 🧠
Using the trained model (best.pt) which was outputted by the model after the 30 epochs of training, inference was run across all 1757 frames of the game video. Each frame yielded a bounding box location of the basketball (in normalized coordinates), various detection confidence scores. This further allowed us to reconstruct the ball's trajectory across time with frame-level resolution.

## Step 3: Shot Quality Metric 📈
Taking inspiration from the machine learning ran on chess engines like Stockfish, a "Shot Quality" score was designed to evaluate how good a shot attempt likely was, based primarily on the ball’s Y-position on the court (a proxy for proximity to the hoop).

I used a custom scale to categorize shots based on the frames of the video. The scale is described as follows:

100 = Layups or dunks
80 = Midrange
60 = Wing jumpers
40 = Long 3s
20 = Heaves or backcourt attempts

This scatterplot visualizes the ball’s trajectory over the course of the game, mapped in real court dimensions (feet). Each point represents the detected position of the basketball in a specific frame of the game, and the color gradient encodes time with purple and blue representing earlier frames and green and yellow representing the end of the game film. This visualization serves as a spatial-temporal heatmap and fingerprint of the game, enabling analysts to infer possession flow, identify transition moments, and diagnose offensive efficiency. This also shows how the ball's movement evolved across time and space, without needing video playback.

## Step 4: Event Tracking Ball Movement 📊 
To better understand spatial trends, all basketball positions were converted from pixels to real court coordinates (feet).

From this, a full-court heatmap was built showing various metrics such as ball movement over time, shot attempt locations on the court, possession change zones, and fast break sequences.

This visualization created a powerful event-tagged visual of game flow, ideal for coaches and analysts, who are willing to see where and how teams need to up their defensive and offensive team ratings.

## Step 5: Random Forest Model 🌳
Finally, I decided to add my machine learning and predictive touch to it: why not predict the future when we already used real-time and live data from a pre-existing basketball game already?

With labeled shot attempts (based on proximity to hoop and bounce/stabilization heuristics), a logistic regression model was trained on features like court position (X, Y in feet), distance from baseline in the game, and the ball speed before and after the shot was attempted. Despite having only a few True (made) labels, the model achieved:

🎯 An 86% accuracy
✅ 1.00 precision on made shots
💡 A real predictive insight engine for shot efficiency that could be used by coaches and analysts down the line

## Parting Thoughts
Working on this project has been one of the most exciting and rewarding experiences, from building custom YOLOv8 models to crafting real-time court visualizations and predictive analytics. It’s been a joy bringing data to life through basketball already through the research I'm doing at Eclipse, becoming one with the sport I’ve loved since I was a kid.

I’d be thrilled to be part of the Consulting Group with the UCSD Men's Basketball Team, where I can combine my deep interest in data science with impactful problem-solving. Whether it’s optimizing strategy or exploring hidden insights, I’m all in, and I can’t wait to contribute to projects like this with even greater scale and collaboration. 😁




