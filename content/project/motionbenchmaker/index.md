---
title: MotionBenchMaker A Tool to Generate and Benchmark Motion Planning Datasets
summary: Open source tool to generate benchmarking datasets for robot manipulation problems.
tags:
- Motion Planning
- Robotics
- Learning
date: "2021-11-01T00:00:00Z"
authors:
- admin

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Examples of environments and robots in our pre-generated dataset of motion planning problems. The black arrows show the direction of perturbation that can be made to the nominal scenes to create new problems by for example sampling the relative orientation of the robot.
  focal_point: Smart

links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
url_code: "https://github.com/KavrakiLab/motion_bench_maker"
url_pdf: "https://www.kavrakilab.org/publications/chamzas2022-motion-bench-maker.pdf"
url_slides: ""
url_video: "https://www.youtube.com/watch?v=t96Py0QX0NI"

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
slides: ""
---

Evaluating motion planning algorithms for high degree-of-freedom robots (i.e., manipulators) can be challenging and time consuming, prone to bias and hard to compare against state-of-the-art planners. Additionally, with the advent of learning methods in planning for robotics, it is paramount to have the ability to generate datasets of meaningful problems to train and evaluate new models. In this paper we introduce [MotionBenchMaker](https://github.com/KavrakiLab/motion_bench_maker), an open source tool to generate datasets for bechmarking and training for realistic robot manipulation problems. Our tool is designed to be easy to extend to support new problems and robots and comes with tools to easily perform motion planning benchmarking.

## Features of MotionBenchMaker
These are some of the features that MotionBenchMaker offers:
- It is written on C++
- It supports ROS and MoveIt making it easy to integrate into existing robotics implementations
- Configuration of new environments and robots is done through standard formats such as yaml, urdf, srd files.
- It comes with sampling-based planners from OMPL such as RRT-Connect, PRM, KPIECE, etc.
- It provides tools to easily specify environment transformations to automatically generate interesting motion planning problems, such as problem generator and scene sampler.
- It comes with prefrabicated datasets that comprise 5 commonly used robots and 8 environments that are actively being used by the community to assess the performance of new motion planning algorithms.

## Scene Sampler and Problem Generator
The main functionality of MotionBenchMaker is its ability to create new problems by 1) easily specifying (random) transformations to objects from a nominal scene to generate distinct problems from a similar domain and 2) automating the way to specify motion planning problems (start/goal configurations) for manipulation problems by describing relationships between robot end-effectors and objects in the scene. The first component is achieved by a scene sampler which can perform SE(3) sampling to objects in the scene as well as URDF sampling as shown in the figure below:

{{< figure library="true" src="scene_sampler.png" title="Given a nominal scene (left), the scene sampler generates variations by performing (right) SE(3) sampling as well as URDF sampling of kinematic structures of a scene (such as the doors of a cabinet). Sampling parameters are specified using descriptor files." >}}

The Problem Generator takes as inputs a robot description (URDF), a geometric scene and object-centric end-effector poses and create a motion planning problem (start and goal configurations in the form of a MoveIt! request). Additional transformations to specify the robot base pose can be specified. The figure below shows examples.

{{< figure library="true" src="problem_generator.png" title="Given the information on the left, the problem generator performs inverse kinematics and all the appropriate transformations to compute a fully defined motion planning problem, i.e., start and goal configurations, providing an abstract interface that is robot-agnostic and ready to use." >}}

## Prefabricated dataset
MotionBenchMaker comes with a set of prefabricated problems that are interesting motion planning queries with commonly used robots.

{{< figure library="true" src="problems.png" title="Prefabricated problems that come with MotionBenchMaker" >}}