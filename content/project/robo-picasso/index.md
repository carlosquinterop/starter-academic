---
title: Inverse Kinematics Robo Picasso
summary: Solving the inverse kinematics problem for a FANUC S-500 robot and using it to draw a Mickey Mouse
tags:
- Robotics
date: "2021-01-11T00:00:00Z"
authors:
- admin

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: FANUC industrial robot
  focal_point: Smart

links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
slides: ""
---

This project was a lab assignment in the course **MECH 498: Introduction to Robotics** that I took during the Spring of 2020 offered by [Dr. Marcia O'Malley](https://omalleym.web.rice.edu/). I thought this project was a lot of fun and so I decided to share the main results here.
The assignment was about computing the inverse kinematics (IK) problem for a 6-DOF FANUC S-500 robot shown above.

The project was coded using MATLAB where we were given a model of the FANUC robot and were asked to implement both its forward kinematics and inverse kinematics.
The robot is provided with a drawing tool attached to its end-effector with 4 different brushes and the objective is to give the robot a 3D discretized path that contains the points that make the drawing (a Mickey Mouse face in our case!), so that the robot can draw it. By solving an IK problem for each point in the trajectory and plot them all we can see how the robot model draws the given trajectory. Notice that there are additional challenges to avoid the robot to change between 'elbow up' and 'elbow down' configurations in consecutive points of the trajectory.

To make it slightly more interesting we decided to make the robot plot in two different planes for the same drawing, similar to paintings that are drawn in the corner of a room. Checkout the video to see our robot painting the Mickey Mouse face between two walls and notice how the orientation of the tool is changed when the second half of the face is being painted.

{{< youtube ibtgLo-S1uE >}}