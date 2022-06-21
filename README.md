# GenericParticleSolver

## Particle tracking to solve solute transport equation at macro-scale  (molecular diffusion + pore-scale dispersion)

Solute transport equation:

$$
\frac{\partial c_i}{\partial t}=-\mathbf{u}\cdot \nabla c_i+\nabla \cdot \left( D\nabla c_i \right) 
$$

Solve above equation in Lagrangian domain:
$$
\mathbf{x}\left( t^{n+1} \right) =\mathbf{x}\left( t^n \right) +\mathbf{u}\left( \mathbf{x}\left( t^n \right) ,t^n \right) \varDelta t+\mathbf{B}\cdot \xi \left( t \right) \sqrt{\Delta t}
$$

Given $\mathbf{B}$ is a 3x3 matrix that includes molecular diffusion and dispersion, and konws $2\mathbf{D}\left( \mathbf{x}\left( t^n \right) \right) =\mathbf{B}\left( \mathbf{x}\left( t^n \right) \right) \cdot \mathbf{B}^T\left( \mathbf{x}\left( t^n \right) \right) $

The general expression of $\mathbf{D} = \mathbf{D}=\left( \alpha _T\left| \mathbf{u} \right|+D_m \right) \mathbf{I}+\frac{\alpha _L-\alpha _T}{\left| \mathbf{u} \right|}\mathbf{uu}^T$   considering pore-scale dispersion are:
$$
\mathbf{D}=\left[ \begin{matrix}
	\left( \alpha _T\left| \mathbf{u} \right|+D_m \right) +\left( \alpha _L-\alpha _T \right) \frac{u_{1}^{2}}{\left| \mathbf{u} \right|}&		\left( \alpha _L-\alpha _T \right) \frac{u_1u_2}{\left| \mathbf{u} \right|}&		\left( \alpha _L-\alpha _T \right) \frac{u_1u_3}{\left| \mathbf{u} \right|}\\
	\left( \alpha _L-\alpha _T \right) \frac{u_1u_2}{\left| \mathbf{u} \right|}&		\left( \alpha _T\left| \mathbf{u} \right|+D_m \right) +\left( \alpha _L-\alpha _T \right) \frac{u_{2}^{2}}{\left| \mathbf{u} \right|}&		\left( \alpha _L-\alpha _T \right) \frac{u_2u_3}{\left| \mathbf{u} \right|}\\
	\left( \alpha _L-\alpha _T \right) \frac{u_1u_3}{\left| \mathbf{u} \right|}&		\left( \alpha _L-\alpha _T \right) \frac{u_2u_3}{\left| \mathbf{u} \right|}&		\left( \alpha _T\left| \mathbf{u} \right|+D_m \right) +\left( \alpha _L-\alpha _T \right) \frac{u_{3}^{2}}{\left| \mathbf{u} \right|}\\
\end{matrix} \right] 
$$

Expression of $\mathbf{B}$ from Eq.64 of `doi.org/10.1029/2000WR000100`  are given in
$$
\mathbf{B}=\left[ \begin{matrix}
	\frac{u_1}{\left| \mathbf{u} \right|}\sqrt{\alpha _L\left| \mathbf{u} \right|+D_m}&		-\frac{u_1u_3\sqrt{\alpha _T\left| \mathbf{u} \right|+D_m}}{\left| \mathbf{u} \right|\sqrt{u_{1}^{2}+u_{2}^{2}}}&		-\frac{u_2\sqrt{\alpha _T\left| \mathbf{u} \right|+D_m}}{\sqrt{u_{1}^{2}+u_{2}^{2}}}\\
	\frac{u_2}{\left| \mathbf{u} \right|}\sqrt{\alpha _L\left| \mathbf{u} \right|+D_m}&		-\frac{u_2u_3\sqrt{\alpha _T\left| \mathbf{u} \right|+D_m}}{\left| \mathbf{u} \right|\sqrt{u_{1}^{2}+u_{2}^{2}}}&		\frac{u_1\sqrt{\alpha _T\left| \mathbf{u} \right|+D_m}}{\sqrt{u_{1}^{2}+u_{2}^{2}}}\\
	\frac{u_3}{\left| \mathbf{u} \right|}\sqrt{\alpha _L\left| \mathbf{u} \right|+D_m}&		\sqrt{\frac{u_{1}^{2}+u_{2}^{2}}{\left| \mathbf{u} \right|^2}\alpha _T\left| \mathbf{u} \right|+D_m}&		0\\
\end{matrix} \right] 
$$

Expression of $\mathbf{B}$ from Eq.11 of `doi.org/10.1016/j.cpc.2019.01.0130010-4655`  are given in:
https://github.com/GerryR/par2/blob/1b7ebffa0c494339e01bd12edbfb8623da42725e/Geometry/CornerField.cuh#L413
$$
\mathbf{v}_1=\left[ u_1,u_2,u_3 \right] ^T
\\
\mathbf{v}_2=\left[ -u_2,u_1,0 \right] ^T
\\
\mathbf{v}_3=\left[ -u_3u_1,-u_3u_2,u_{1}^{2}+u_{2}^{2} \right] ^T
$$