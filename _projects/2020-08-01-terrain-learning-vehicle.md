---
layout: project
title: Terrain Learning Vehicle
description: Description for Seo
summary: Self-supervised robot that learns from experience
category: Master's Project
---

<img src="/assets/terrain-learning-vehicle/f1-robots.png" alt='Offroad Robots' style="width: 20%; float: right; margin: 5px;"/>

This project proposes a self-supervised machine learning architecture which samples and learns a vehicle and terrain relationship from experience for an off road vehicle. The findings from this research are currently being written up for publication, and the original thesis can be downloaded 
[here](/assets/terrain-learning-vehicle/Learning_Vehicle_Dynamics_Models_by_Self_Supervised_Learning.pdf){:target="_blank"}

The motivation for this project is that mobile robots are no longer confined to just factory floors anymore and are increasingly being used in unstructured and unknown environments, such as urban, farmland and even other planets! (see figure 1) As such there is a requirement for accurate and robust vehicle-terrain prediction mechanisms.

---

### Learning Architecture
The vehicle (real or virtual) makes some pass over the terrain, which is used to calculate a traversability label. This score is mapped back onto images of the terrain and used as labels to train a CNN to predict terrain traversal for new images (Figure 2).

<img src="/assets/terrain-learning-vehicle/f2-Learning-Architecture.png" width='100%' alt='Learning Architecture'>

---

### Traversal Data from Simulation
The data used to train this model was collected using a computer simulation, but the same process could be applied to data from a real robot.

<img src="/assets/terrain-learning-vehicle/f3-pioneer.png" alt='Pioneer Robot' style="width: 25%; float: right;"/>
**Simulation Setup -** Simulated using Gazebo and ROS (Robot Operating System). The Pioneer 3-AT skid-steer robot was modelled (Figure 3) as it can later be used in real life.<br clear="all" />

<img src="/assets/terrain-learning-vehicle/f4-deepscene.png" alt='DeepScene dataset' style="width: 50%; float: right;"/>
**DeepScene Forest Dataset -** Contains 350 real RGB, depth and ground truth images (Figure 4).<br clear="all" />

<img src="/assets/terrain-learning-vehicle/f5-mesh.png" alt='Terrain mesh' style="width: 50%; float: right;"/>
**Terrain Generation -** Depth images converted into 3D meshes (Figure 5) and loaded into simulation.<br clear="all" />

<img src="/assets/terrain-learning-vehicle/f6-traversal.png" alt='Terrain Traversal' style="width: 50%; float: right;"/>
**Traversal Training -** Robot drives over terrain mesh, and the traversal labels are mapped back onto terrain image (Figure 6). This traversal data is required to train the CNN (see section 4).<br clear="all" />

---

### Convolutional Neural Network

**Architecture -**The CNN architecture is based upon a height map which uses a Keras front end and TensorFlow backend. This is a standard CNN structure which is well suited for image feature recognition (see the exact architecture on Figure 7).
<img src="/assets/terrain-learning-vehicle/f7-CNN.png" width='100%' alt='CNN' >

**Training -** 
The CNN was trained for 9 hours with 52,000 samples (around 13km of driving simulations), and eventually achieved an accuracy of around 70% (see Figure 8).
<img src="/assets/terrain-learning-vehicle/f8-CNN-Training.png" width='100%' alt='Training' >

---

### Results

<img src="/assets/terrain-learning-vehicle/t1-friction.png" alt='Friction' style="width: 55%; float: right;"/>
The CNN was trained for both uniform (𝜇 = 1.0) and variable terrain friction coefficients (see Table 1)<br clear="all" />

<img src="/assets/terrain-learning-vehicle/f9-results.png" width='100%' alt='Results' >

**Path Planning -**
A simple Dijkstra algorithm is demonstrated with traversability weightings applied:

<img src="/assets/terrain-learning-vehicle/f10-pathplanning.png" width='100%' alt='Path Planning' >