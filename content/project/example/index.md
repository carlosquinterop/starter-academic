---
title: Can Theoretical Algorithms Efficiently Escape Saddle Points in Deep Learning?
summary: Review of optimization algorithms that can escape saddle points in Deep Learning and some experimental results
tags:
- Deep Learning
- Optimization
- Gradient Descent
date: "2021-01-11T00:00:00Z"
authors:
- admin
- sean

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Gradient Descent gets stuck in saddle points
  focal_point: Smart

links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
url_code: ""
url_pdf: "pdfs/Escaping_Saddle_Points.pdf"
url_slides: "slides/EscapingSaddlePoints_CompleteFV.pdf"
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
slides: ""
---

This project provides a literature review for the most important recent works related to optimizing high-dimensional non-convex functions in the presence of saddle points mostly for machine learning applications.

The inspiration came from reviewing the paper "How to Escape Saddle Points Efficiently?". A large research effort has been devoted to proposed methods that can converge to second order stationary points efficiently. Of special interest is the set of methods that do not rely on Hessian computation, mainly driven by applications in machine learning where this may not be feasible. Although, many important theoretical results have been proposed, many of them have not be tested in real experiments, especially in the context of training a deep neural network. We have designed experiments with different network architectures and state-of-the-art datasets to observe the behavior of perturbed versions of gradient descent. Initial results show that an improvement in experimental convergence rate can be seen only for small and shallow networks. 
