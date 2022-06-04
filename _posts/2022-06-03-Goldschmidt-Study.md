---
layout: post
title: "Comparison of MPPIC and DPM in OpenFOAM"
author: "Joseph"
categories: [portfolio,blog]
tags: [portfolio,blog]
image: Goldschmidt.png
---

### Direct Particle Modeling (DPM) 

Fluidised beds are difficult to model because both fluid-particle interactions and particle-particle interactions are important. This requires a lot of computing capacity as the interactions between thousands (or millions) of particles have to be tracked. DPM does this directly and is very computationaly expensive. For example, the OpenFOAM tutorial case Goldschmidt that models a fluidised bed with 24750 particles takes 0.51 s to complete one iteration on a single core. Shown at the link below is a simulation of 5 s of runtime.   

### DPM Video

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/fgOK8X1dh0Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>"

## Multi-Phase Particle In Cell (MPPIC)

The MPPIC approach statistically models the collisions without directly computing every individual interaction. This reduces the computational requirements substancially. For the same case on a single core, a time step takes 0.090 s. As the simulation progresses and there are more collisions, the DPM version is further slowed down. The MPPIC case ran in about 40 minutes where the DPM case took the better part of a week. The video below shows the MPPIC case. There are certainly some differences between the two cases, but the general dynamics are similar. This is a dramatic difference in the computational requirements.

### MPPIC Video

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/227j3r_NFt8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

