# Markov Localisation-1

---

## Introduction to localisation posterior
- We have
  - z<sub>1:t</sub> : Observation like range measurements, bearing, images
  - u<sub>1:t</sub> : Controls like yaw/pitch/roll rates, velocities
  - m : Map like grid maps, feature maps
- We want
  - x<sub>t</sub> : 2D pose (position (x,y) and orientation &theta;)

## Explanation
- Localisation is all about estimating the probability of car xt, $bel(xt = p(xt | z1:t, u1:t, m)$
- For pure localisation, we assume the map is correct and  doesn't change
- To estimate map too, $p(xt, m | z1:t, u1:t)$ -- SLAM

## Map
- Landmarks based maps are more sparse than grid based maps
- 1d case : map is a vector where these objects are : $m = [5, 9, 6, 8, ..]$

## Observation
- Car measures nearest k static objects like distance to trees
- Observation list includes distance vectors for each time step
- List : $z1:t = \{ zt, ..., z1\}$
- Vector : $zt = \{ zt1, ..., ztk\}$
- Can include 0 to k measurements

## Control
- Control vector : Includes direct move bw consecutive time stamps\
- Distance car travelled bw t and t-1
- $u1:t = [ut, ..., u1]$

## Pose range space
- Car can be anywhere in defined space
- Can be defined as a vector of 100 elements: $bel(xt) = [bel(xt=0), ..., bel(xt=99)]$
- The goal is to estimate these values
