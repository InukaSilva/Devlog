---
title: SO101 Arm - Set up and Imitation learning
draft: false
tags:
---
```
Environment:
- SO101 Leader and Follower Arm
- Lenovo Legion 5 (Ryzen 7, RTX 4060)
- WSL Ubuntu 24.04
- Windows 11
- Lerobot 0.6.1
```

First thing that I worked on was getting everything set up, teleoperation, and running an imitation learning model. I was able to get calibration and teleoperation working smoothly pretty quickly.

The first and biggest issue I ran into was with getting cameras to work nicely within WSL. Due to how USB ports work, I needed to share the USB into the virtual machine. Once that was done, I ran into issue with the lerobot commands for finding cameras. This is because in code it seemed to automatically choose an FFMPEG backend even though it should be picking V4L2. Additionally, it would avoid picking MJPEG and pick YEYV as the image format. I was able to get around this issue by specifying the camera backend and format. Additionally, I found that openCV 4.13 uses a different backend than the newest version, which helped rather than hardcoding it inside of the commands.

Then came recording a dataset, training the model, and testing. For my environment and task, I wanted the arm to pick up a rubber duck within a specified area and place it into a hole in the environment. I start with a 50 episode dataset. I found that my two camera set up was not recording at the correct fps, meaning frames were missing. From what I can tell, this came from the Logitech 270 and how it interacts with WSL. I ended up buying the USB camera that was typically sold with the kit, but that also seemed to not work as well it should.

In total, I recorded and trained 3 imitation learning models, with 50 episodes each. While I was able to get some successful runs, the accuracy was still low, which could be due to a slightly changing environment, lack of episodes, etc.

![[Lerobot_Arm_Imitation_Learning_Demo.mp4]]

**What's next?**
I've been told that recently lerobot works pretty well on a windows system, so I am setting everything up on windows rather than having to deal with USB pass through for WSL. Additionally, I am going to set up Issac sim and see if I can work on a simulation model, and then sim to real life using a reinforcement learning model. Finally, I want to put everything together to make an overall system rather than just manually running a command to start the model.