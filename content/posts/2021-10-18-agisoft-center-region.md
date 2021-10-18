---
title: Agisoft Center Region
date: 2021-10-18T08:19:55.866Z
tags:
  - agisoft
  - python
cover:
  image: /img/vector_agisoft2.png
  caption: agisoft vector
---
I've been trying to create a bounding box that fits the model similar to [pi3d](https://www.pi3dscan.com/index.php/instructions/item/automatic-scan-processing-with-agisoft).
After reading the script from [pi3d](https://www.pi3dscan.com/index.php/instructions/item/automatic-scan-processing-with-agisoft), the python script needs another marker on the wall parallel to the body model. It is redundant for my current project.
So, I tweaked it and found out that the model is not straight Z-up.


![vector in metashape](/img/vector_agisoft2.png)

The red line is a vector of the medium body, and the blue line is a vector of the middle floormat. From these two-line, We can depict that the model (black line) is not parallel with the x-axis. So, we can't shift the Z component of the floormat vector directly.

But then, I found a more straightforward solution: to average the vector centre of the existing region and the vector centre of the floormat.

```python
new_center = chunk.markers[0].position
for m in chunk.markers[1:4]:
    new_center += m.position
new_center /= 4

new_center = (new_center + chunk.region.center) / 2
newregion.center = mx
```