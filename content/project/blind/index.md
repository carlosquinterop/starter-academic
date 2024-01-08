---
title: Human-Guided Motion Planning in Partially Observable Environments
summary: Human-in-the-loop algorithm to compute joint-space trajectories for high-DoF robots under partial observability
tags:
- Optimization
- Motion Planning
- Robotics
- Learning
date: "2021-09-01T00:00:00Z"
authors:
- admin

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: (Left) The Fetch robot planning a motion to pick up an object inside the box where only part of the box (colored voxels) is visible. (Right) Fetch robot planning its motion to move the hand from the oven to the counter top while avoiding the (not observable) heat coming from the stove.
  focal_point: Smart

links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
url_code: ""
url_pdf: "https://www.kavrakilab.org/publications/quintero-chamzas2022-blind.pdf"
url_slides: ""
url_video: "https://www.youtube.com/watch?v=RbDDiApQhNo"

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
slides: ""
---
This project is concerned with the problem of motion planning for high-DOF robots under partial observability using guidance from humans.
We have proposed Bayesian Learning in the Dark (BLIND), an algorithm that leverages the human senses to compute high-DOF robot trajectories that are safe despite partial observability of the environment.
The main components that made up BLIND are shown next

{{< figure library="true" src="BLIND-pipeline.png" title="BLIND algorithm" >}}

The construction of a low-dimensional discrete state space and the guided motion planner are the two main novelties within BLIND.
The former leverages projections and sampling-based motion planners to create a space where reward learning can be performed. The latter uses optimization-based motion planning to incorporate the knowledge learned from the human as motion constraints.  
These two together enable reward learning techniques to be used using critiques to learn and compute high-dimensional safe trajectories despite the incomplete environmental information.

The results show that BLIND outperforms state-of-the-art methods in teaching effort, success rate and path length.

{{< figure library="true" src="results.png" title="Results of simulated experiments in the Box and Stove environments" >}}

Check out our video of a robot implementation of BLIND, where a human user is asked to critique trajectories that are potentially unsafe. BLIND is executed in real-time and it converges to a safe solution.

{{< youtube RbDDiApQhNo >}}