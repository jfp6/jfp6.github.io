---
layout: post
title: "Cantilever Beam: Finite Volume vs Finite Element Solutions"
author: "Joseph"
categories: blog
tags: [blog,portfolio]
image: FVFECodeAster.png

---
Both finite volume and finite element approaches can be used to solve for deflection of a cantilever beam. In a previous post, I looked at two open source finite element solvers (Code Aster and Calculix) to calculate the deflection. In this post, I will compare Code Aster to OpenFOAM (finite volume). The following mesh was used for both approaches.

![alt text](/assets/img/FVFEmesh.png)

For this comparison, I wanted to used enough cells/elements that for either approach the solution would be predominantly mesh independent. The setup of the Code Aster solution was very similar to the previous post. The results are shown below.

![alt text](/assets/img/FVFECodeAster.png)

For the OpenFOAM solution, the approach is captured in the boundary condition file D and the physicalProperties file which I show an abbreviated version.

```
D

boundaryField
{

    "(side|sidez|top|bot)"
    {
        type            tractionDisplacement;
        traction        uniform (0 0 0);
        pressure        uniform 0;
        value           uniform (0 0 0);
    }

    fix
    {
        type            fixedValue;
        value           uniform (0 0 0);
    }

    load
    {
        type            tractionDisplacement;
        traction        uniform (0 -50000 0);
        pressure        uniform 0;
        value           uniform (0 0 0);
    }

}
physicalProperties

rho
{
    type        uniform;
    value       2710;
}

E
{
    type        uniform;
    value       69e+9;
}
```

I used the solidEquilibriumDisplacementFoam solver which is a steady, linear elastic, small strain solver. The results are as follows.

![alt text](/assets/img/FVFEOpenFOAM.png)

Analytical deflection 452.90 um

Code Aster deflection is 451.03 um

OpenFOAM deflection is 450.81 um

Agreement between the two methods is excellent and both match analytical estimates extremely well. 

