---
layout: post
title:  "Scaling of magnetization with temperature"
tags: magnetism chromia
math: true
---

Temperature dependencies in magnetism are always somehow tricky and involve many model assumptions. The behavior of magnetization (or sublattice magnetization for antiferromagnets) is of special interest since it gives a hint for scaling of other material parameters.

There is a seminal Bloch's 3/2 law that can be used as a good approximation for bulk ferromagnets [(Aharoni96)][Aharoni96]. It comes from the consideration of spin waves on the background of the uniform state that effectively scale the average moment per unit volume. After some math for a cubic bcc ferromagnet, the resulting scaling of the saturation magnetization \\\(M_S\\\) with temperature \\\(T\\\) is

$$
\dfrac{M_S(T)}{M_S(0)} \approx 1 - 0.0104 \dfrac{1}{S} \left( \dfrac{k_\text{B}}{\hbar^2 SJ} \right)^{3/2} T^{3/2},
$$

where \\\(k_\text{B}\\\) is the Boltzmann constant, \\\(\hbar\\\) is the Planck constant, \\\(S\\\) is the spin length, and \\\( J \\\) is the exchange integral. Other lattices may have different numerical prefactors. However, considering the real ferromagnet the saturation magnetization at 0K and the critical temperature \\\(T_C\\\) of transition to the paramagnetic state are the fitting parameters, and the Bloch formula can be improved as follows [(Kuzmin05)][Kuzmin05], [(Kuzmin20)][Kuzmin20]:

$$
\dfrac{M_S(T)}{M_S(0)} = \left[ 1 - s \left(\dfrac{T}{T_C}\right)^{3/2} - (1-s) \left(\dfrac{T}{T_C}\right)^p \right]^{1/3}
$$

where \\\(s > 0\\\) is one fitting parameter, and another fitting parameter can be taken as \\\( p = 5/2 \\\) in many cases. These dependencies can be used to estimate the exchange stiffness. Since the practically relevant case nowadays includes thin films, one should keep in mind that the spin-wave-based analytics of Bloch 3/2 law is modified there because of geometric confinement, and generally, the power 3/2 can change. 

We work a lot with antiferromagnets, with a special focus on &alpha;-Cr<sub>2</sub>O<sub>3</sub> (chromia). There, DFT and experimental estimates agree with the sublattice magnetization at 0K to be \\\( M_S \approx 530 \\\) kA/m (note that it includes two magnetically equivalent Cr ions within the four-Cr unit cell!) [(Samuelsen70)][Samuelsen70], [(Pylypovskyi24)][Pylypovskyi24]. The bulk critical temperature of transition to the paramagnetic state is 308K. And within this range, there is a nice fit of the experimental measurements given by the analytical expression [(Hoser12)][Hoser12]:

$$
\dfrac{M_S(T)}{M_S(0)} = \begin{cases}
 1 - 0.555 \left(\dfrac{T}{T_C}\right)^{3} & T < 250\text{\,K} \\
 0.893 \left[1 - \left(\dfrac{T}{T_C}\right)^{3} \right]^{0.314} & T > 250\text{\,K}
\end{cases}
$$

![](/assets/blg/figs-cr2o3/sublattice-m.png)

## References

[Samuelsen70]: Samuelsen, E., Hutchings, M. and Shirane, G. _Inelastic neutron scattering investigation of spin waves and magnetic interactions in Cr<sub>2</sub>O<sub>3</sub>_, Physica, 48, 13–42 (1970) DOI:[10.1016/0031-8914(70)90158-8](https://doi.org/10.1016/0031-8914(70)90158-8)
[Aharoni96]: Aharoni, A. _Introduction to the theory of Ferromagnetism_, Oxford University Press (1996)
[Kuzmin05]: Kuz’min, M. D. _Shape of Temperature Dependence of Spontaneous Magnetization of Ferromagnets: Quantitative Analysis_, Physical Review Letters, 94, 107204 (2005) DOI:[10.1103/physrevlett.94.107204](https://doi.org/10.1103/physrevlett.94.107204)
[Hoser12]: Hoser, A. and Köbler, U. _Renormalization Group Theory_, Springer Berlin Heidelberg (2012)
[Kuzmin20]: Kuz’min, M. D., Skokov, K. P., Diop, L. V. B., Radulov, I. A. and Gutfleisch, O. _Exchange stiffness of ferromagnets_, The European Physical Journal Plus, 135, 301 (2020) DOI:[10.1140/epjp/s13360-020-00294-y](http://dx.doi.org/10.1140/epjp/s13360-020-00294-y)
[Pylypovskyi24]: Pylypovskyi, O. V., Weber, S. F., Makushko, P., Veremchuk, I., Spaldin, N. A. and Makarov, D.
Surface-Symmetry-Driven Dzyaloshinskii-Moriya Interaction and Canted Ferrimagnetism in Collinear Magnetoelectric Antiferromagnet Cr<sub>2</sub>O<sub>3</sub>, Physical Review Letters, 132, 226702 (2024) DOI:[10.1103/physrevlett.132.226702](https://doi.org/10.1103/physrevlett.132.226702)
