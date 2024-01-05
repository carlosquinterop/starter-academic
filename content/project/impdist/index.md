---
title: Stochastic Implicit Neural Signed Distance Functions for Safe Motion Planning under Sensing Uncertainty
summary: Safe motion planning approach for noisy sensor measurement representation of the environment using a stochastic neural implicit representation and chance constrained optimization.
tags:
- Optimization
- Motion Planning
- Robotics
- Learning
date: "2023-09-01T00:00:00Z"
authors:
- admin

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: The environment is made of noisy points (blue spheres) to be avoided. Our method transforms a candidate path (red) into a safe path (purple) by solving a sequence of optimization problems that account for sensing uncertainty. Cutouts show parts of the path transformation, the arm is pushed away from noisy regions to attain safer behavior.
  focal_point: Smart

links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
url_code: ""
url_pdf: "https://arxiv.org/pdf/2309.16862.pdf"
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

There exists a plethora of highly efficient methods for motion planning when the environment representation is perfectly known. Typical representations include meshes and geometric primitives that resemble objects in the environment. However, when the information about the environment comes direclty from sensors the situtation changes. It is still not clear how to incorporate this information into existing motion planning algorithms in a safe and reliable way. A common approach consists of computing intermediate representations such as planes, meshes and occupancy information using sensor data. However, this naive integration may fail in guaranteeing that the computed robot motions are safe when executed by the robot. This is especially true for high-DoF manipulators where simplifying assumptions do not hold.

We propose a stochastic implicit neural signed distance representation that 1) models sensor uncertainty directly and therefores does not require exact knowledge of the environment geometry and 2) that can provide important no-collision information in the robot configuration space that we use to formulate a hierarchical chance-constrained motion planner to generate minimal risk motions that are guaranteed to respect a maximum bound on a given probability of collision and are efficiently solved using off-the-shelf solvers.

## Sensing uncertainty quantification
The figure below shows a diagram of our neural representation to quantify the uncertainy coming from the sensor. Inspired by recent trends on implicit representations we pose the problem as variational inference by learning a probability distribution over signed distances for each robot link conditioned on a point in space. This is paramount since it provides 1) uncertainty estimates of distances that can be incorporated into a safe motion planner and 2) directions in the robot's configuration space to avoid collisions from noisy points. We use this information to formulate a safe motion planner based on optimization that can be efficiently solved.

{{< figure library="true" src="method.png" title="Our stochastic implicit neural signed distance functions use a) a robot configuration q and b) one noisy point x as input. c ) Inputs go through a positional encoding layer and then through 4 fully connected layers of size 256. Finally, two separate layers of size K output the mean and standard deviation parameters of d) each link's distribution modeling the noisy signed distance conditioned on q, x." >}}

## Chance-constrained hierarchical planning
We propose a hierarchical planner that first uses the noisy information from the sensor to compute a *candidate path* that is later processed by a sequence of chance-constrained inverse kinematic optimization-based solvers using the uncertainty information from the neural representation. We propose a novel reformulation of the joint chance constraint that represents the no-collision information between the robot and the environment and show that it can be solved efficiently and to global optimality by off-the-shelf solvers for realistic motion planning problems.

## Results
We ran experiments on 50 different instances of problems from [MOTIONBENCHMAKER](https://www.kavrakilab.org/publications/chamzas2022-motion-bench-maker.pdf) where the environment was represented by small spheres that covered the actual geometry. Each problem has different start/goal configurations coming from variations in the grasped object and the robot's relative pose with respect to the table. Obstacles in the table are also randomly sampled. We compared our method with a baseline where each sphere radius is increased by certain percentage. To assess the performance of the methods we estimated the true probability of collision by running a Monte Carlo simulation with 20.000 samples for each computed path. The candidate paths were computed using RRT-Connect. The results are shown below.

{{< figure library="true" src="risk.png" title="Estimated CDF of the risk attained by each method on all 50 problems." >}}