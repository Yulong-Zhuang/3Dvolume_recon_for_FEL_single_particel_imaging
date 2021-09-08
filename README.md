# 3Dvolume_recon_for_FEL_single_particel_imaging
Using VAE to reconstruct 3D volumes of heterogeneous objects from their 2D tomography images in single particle imaging

Figure below shows the architecture of the VAE neural network, consisting of a 2D CNN pattern-encoder to encode 2D patterns along with their orientation estimates into distributions of latent parameters, and a 3D transposed convolution network as volume-decoder to generate 3D intensity volumes from latent numbers. This setting allows the neural networks to learn the 3D-heterogeneity-structure-encoded latent numbers from the diffraction patterns.
![plot](https://github.com/Yulong-Zhuang/3Dvolume_recon_for_FEL_single_particel_imaging/blob/main/appendix/VAE_structure.png)
The model works in the following manner: For each input average $X$, its orientation, $\Omega$ and gain, $\mathcal{G}$, the encoder network generates a Gaussian distribution of its latent variable values $N(\mu, \sigma)$. The fact that this is not just a single latent vector $z$, but a distribution makes the auto-encoder variational and enforces the smoothness of the latent space. It also enables the network to use information from neighbouring regions in the space to update regions with limited data. A latent vector $z$ is sampled using this distribution and used by the decoder to generate a 3D intensity volume $V_{3d}$, which is then symmetrized by the octahedral point group. The known orientation is then used to slice the generated 3D volume to get a reconstructed 2D pattern $X'$. The goal of training is to minimize the difference between $X$ and $X'$ (further details in Appendix~\ref{app:vae_details}). 3D information is obtained since the same latent space region is sampled by averages in a variety of orientations. Note, that although the $\mathcal{G}$ is not strictly necessary for the VAE network to reconstruction 3D volumes, it helps to regularize the latent space of $z$.

There are 3 different reconstructing volume sizes options: low volume ($81^3$), intermediate volume ($161^3$) and high volume ($243^3$).



