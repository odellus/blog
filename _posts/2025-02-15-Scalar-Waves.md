---
layout: post
title: Scalar Waves
---

We present a simple derivation for a longitudinal wave in vacuum from the same principles as the one taught in undergraduate physics but do not neglect the current density.

Longitudinal optics is a burgeoning field of research lacking in solid theoretical foundations. This is an substandard attempt to rectify this situation.

## Equations
Curl of the curl:  
$$
\begin{align}
\nabla \times \left( \nabla \times \textbf{F} \right) &= \nabla \left( \nabla \cdot \textbf{F} \right) - \nabla^{2} \textbf{F}
\end{align}
$$

### Maxwell's Equations
Gauss' Law for Electricity:
$$
\begin{align}
\nabla \cdot \textbf{E} &= \frac{\rho}{\epsilon_0}
\end{align}
$$

Gauss' Law for Magnetism:
$$
\begin{align}
\nabla \cdot \textbf{B} &= 0
\end{align}
$$

Faraday's Law of Induction:
$$
\begin{align}
\nabla \times \textbf{E} &= - \frac{\partial \textbf{B}}{\partial t}
\end{align}
$$

Ampere's Law with Maxwell's correction:
$$
\begin{align}
\nabla \times \textbf{B} &= \mu_0 \textbf{J} + \mu_0 \epsilon_0 \frac{\partial \textbf{E}}{\partial t}
\end{align}
$$

Continuity  Equation:
$$
\begin{align}
\nabla \cdot \textbf{J} &= - \frac{\partial \rho}{\partial t}
\end{align}
$$

## Derivation
Let us first consider the RHS curl of the curl of the electric field upon applying Gauss' Law for Electricity:

  
$$
\begin{align}
\nabla \times \left( \nabla \times \textbf{E} \right) &= \nabla \left( \nabla \cdot \textbf{E} \right) - \nabla^{2} \textbf{E} \\
&= \frac{1}{\epsilon_0} \nabla \rho - \nabla^{2} \textbf{E}
\end{align}
$$
  
Successively applying first Faraday's Law of Induction then Ampere's Law with Maxwell's correction to the LHS of the curl of the curl of the electric field:  


$$
\begin{align}
\nabla \times \left( \nabla \times \textbf{E} \right) &= \nabla \times \left( - \frac{\partial \textbf{B}}{\partial t}\right) \\
&= - \frac{\partial}{\partial t} \left( \nabla \times \textbf{B} \right) \\
&= - \frac{\partial}{\partial t} \left( \mu_0 \textbf{J} + \mu_0 \epsilon_0 \frac{\partial \textbf{E}}{\partial t} \right) \\
&= - \mu_0 \frac{\partial \textbf{J}}{\partial t} - \mu_0 \epsilon_0 \frac{\partial^{2} \textbf{E}}{\partial t^{2}}
\end{align}
$$



Now equating the LHS and RHS of the curl of the curl of the electric field and collecting terms:  

$$
\begin{align}
 - \mu_0 \frac{\partial \textbf{J}}{\partial t} - \mu_0 \epsilon_0 \frac{\partial^{2} \textbf{E}}{\partial t^{2}} &= \frac{1}{\epsilon_0} \nabla \rho - \nabla^{2} \textbf{E}\\
\nabla^{2} \textbf{E} - \mu_0 \epsilon_0 \frac{\partial^{2} \textbf{E}}{\partial t^{2}}  &= \frac{1}{\epsilon_0} \nabla \rho + \mu_0 \frac{\partial \textbf{J}}{\partial t} \\ 
\left[ \nabla^2 - \frac{1}{c^2}\frac{\partial^2}{\partial t^2}\right]\textbf{E} &= \frac{1}{\epsilon_0} \nabla \rho + \mu_0 \frac{\partial \textbf{J}}{\partial t}
\end{align}
$$

The LHS of the above is the wave equation for the electric field. For homogeneous waves and non-homogeneous waves with a constant driving source $$ \vec{\lambda} = \left(\lambda_x, \lambda_y, \lambda_z \right) $$ we find the following:

$$
\begin{align}
\frac{1}{\epsilon_0} \nabla \rho + \mu_0 \frac{\partial \textbf{J}}{\partial t} &= \vec{\lambda} \\
\end{align}
$$

Taking the divergence of both sides and applying the continuity equation:  


$$
\begin{align}
\frac{1}{\epsilon_0} \nabla^{2} \rho + \mu_0 \frac{\partial}{\partial t} \left( \nabla \cdot \textbf{J} \right) &= \nabla \cdot \vec{\lambda} \\
\frac{1}{\epsilon_0} \nabla^{2} \rho + \mu_0 \frac{\partial}{\partial t} \left( - \frac{\partial \rho}{\partial t} \right) &= 0 \\
\frac{1}{\epsilon_0} 
\nabla^{2} \rho - \mu_0 \frac{\partial^{2} \rho}{\partial t^{2}} &= 0 \\
\left[ \nabla^2 - \frac{1}{c^2}\frac{\partial^2}{\partial t^2}\right]\rho &= 0
\end{align}
$$

which is the wave equation for the charge density due to the existence of non-trivial charge and therefore current density in free space due to the existence of vacuum polarization. 

We effectively model free space as a plasma with frequency zero. It matters because people have been generating needle of purely longitudinally polarized light since 2008 and it feels like the theory is lagging behind the experimental results. This is one explanation.