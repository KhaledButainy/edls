# Edge-Data Center Latency Streams (EDLS)  

## Overview  
<img width="1080" alt="image" src="https://github.com/user-attachments/assets/3993403b-ac4f-4ce5-86ac-1f8452dab3ad" />


This is the official repository of the EDLS dataset to study rendering inonsistency in edge-supported cloud gaming systems. Rendering inconsistency occurs when the edge server renders new scenes locally before receiving the updated global game state from the data center due to latency. As a result, rendered scenes may appear different and/or deformed from the intended (ground truth) scenes of the game, as illustrated in the figure above. Ultimately, this impacts the player's experience.

 The dataset is used to study the impact of latency on rendering accuracy. The dataset contains synchronized gameplay recordings of client view and ground truth videos. The videos were originally recorded at 2K resolution with a frame rate of 60fps and later downsampled to 720p for analysis.

## Dataset Summary  
- **Original Quality**: 2K (2560x1440) - 60 FPS
- **Downsampled Quality**: 720p (1280x720) - 60 FPS
- **# Frames**: 90k (18k per Session)
- **Latencies (ms)**: 20, 100, 200, 300, and 400
- **Temporal Complexity Method**: [EVCA](https://github.com/cd-athena/EVCA)
- **Perceptual Similarity Method**: [LPIPS (AlexNet)](https://github.com/richzhang/PerceptualSimilarity) 

## Contents  
- **Client View Videos**: Captures the perspective of the client at different latencies during the gameplay.  
- **Ground Truth Videos**: Represents the reference 0 ms videos.  
- **Combined Videos**: Represent the center-cropped GT and Client view frames, put side by side in a single frame for comparison and analysis.

## Download Links
- 2k-60fps (Under processing)
- 720p-60fps ([Here](https://data.mendeley.com/preview/kwp3ntc3pz?a=eadee1af-aec6-45d4-949b-e37455482d34))

## Structure
The following is the general structure for the dataset repository: 
```
├── <Game Title>
│   ├── 720p-60fps-<synchronization_tool>
│   │   ├── client_metadata.csv
│   │   ├── gt_metadata.csv
│   │   ├── client
│   │   │   ├── sync-<latency(ms)>-client.mp4 
│   │   │   └── ... 
│   │   ├── GT
│   │   │   ├── sync-<latency(ms)>-host.mp4 
│   │   │   └── ...
│   │   └── combined
│   │       ├── sync-<latency(ms)>-combined.mp4 
│   │       └── ...
│   └── ...
└── ...

```
where currently we used [Lightworks](https://lwks.com/) for `<synchronization_tool>`. For the future, timestamps could be extracted from Lightworks or any other tool, and then streams could be synchronized using [FFmpeg](https://ffmpeg.org/) for more flexibility. The `.csv` files contains the metadata such as perceptual similarity and temporal complexity associated with each frame. 
