# Physics

In the following we report the meaning of the main physics quantities calculated by `pySNOW`.
We suggest this review for a extensive discussion:

```bibtex
@article{baletto2019structural,
  author  = {Baletto, Francesca},
  title   = {Structural properties of sub-nanometer metallic clusters},
  journal = {Journal of Physics: Condensed Matter},
  volume  = {31},
  number  = {11},
  pages   = {113001},
  year    = {2019},
  doi     = {10.1088/1361-648X/aaf989}
}
```



## Pair Distance Distribution Function - PDDF

Given a nanoparticle, the system pair distance distribution function is defined as:

\begin{equation}
g(d) = \frac{1}{(N)(N - 1)} \sum_{i=1}^{N} \sum_{\substack{j=1 \\ j \ne i}}^{N} \delta'(r_{ij} - d)
\end{equation}

where $N$ is the number of atoms in the system, $r_{ij}$ is the distance between an atom $i$ and an atom $j$ and $d$ is the distance length probed, with $\varepsilon$ defining the width of the distance bin:

\begin{equation}
\delta' = 
\begin{cases}
1 & \text{if } d - \varepsilon \leq r_{ij} \leq d + \varepsilon, \\
0 & \text{otherwise}
\end{cases}
\end{equation}

$\varepsilon$ magnitude thus define whether two atomic distances are parsed into the same or different distance bins.

The PDDF provides rich structural information about the nanoparticle. In particular, the first minimum in $g(d)$ indicates the distance to define the first-neighbor shell, while the presence of sharp peaks reflects a high degree of structural order. It also possible to calculate the chemical PDDF.

## Radial Distance Distribution Function - RDF

The radial distribution function in a system of particles, describes how density varies as a function of distance from a reference particle. It is a measure of the probability of finding a particle at a distance of r away from a given reference particle, here the center of mass.

The density of atoms from the centre of mass of the whole nanoparticle ($\mathrm{CoM}_w$); the distribution of atoms-A from their centre of mass, $\mathrm{CoM}_A$; and similarly for B-atoms, from the $\mathrm{CoM}_B$.
The RDFs count the number of atoms falling in concentric shells from the centre of mass, of the nanoparticle:

$$ r_{\alpha}(i \in w,A,B)=\sqrt{\left(\hat{x}_\alpha(i)\right)^2+\left(\hat{y}_\alpha(i)\right)^2+\left(\hat{z}_\alpha(i)\right)^2}  $$

where the coordinates $w$ is referring to whole cluster, $\hat{x}_\alpha, \hat{y}_\alpha, \hat{z}_\alpha$ of the atom-i and chemical species $\alpha=A, B$ are re-scaled w.r.t the centre of mass chosen, $\mathrm{CoM}_w$, $\mathrm{CoM}_A$ or $\mathrm{CoM}_B$.


## Layer by Layer - LBL
During a LBL analysis, the nanoparticles is sliced into layers and binned of a certain height provided by the user.
A reasonable value to use can be the inter-layer distance of (111) planes in the bulk. 
The axis along which (perpendicular) planes are cut should be specified by the user.
Eventually, you can monitor the number of layers versus time, $m_{l}(t)$, and count the number of atoms per each chemical species $\alpha$ in each layer, $N_l^{\alpha}(t)$.  


## Shape: from gyration tensor and inertia tensor

Here we define shape descriptors obtained from the gyration tensor and inertia tensor, namely: gyration radius, asphericity, acilindricity, relative shape anisotropy, and aspect ratio. 

The gyration tensor is defined as
$$
S_{ij}=\frac{1}{N}\sum_{k=1}^Nr_{i,k}r_{j,k}
$$
where $r_{i,k}$ is the $i$-th coordinate of the $k$-th particle in a system of $N$ total particles. Given $\lambda_1<\lambda_2<\lambda_3$ the eigenvalues of the gyration tensor, we can define a series of descriptors of the geometric shape of the distribution of points (here, the atomic positions). These are:

 - the gyration radius $R_g=\lambda_1+\lambda_2+\lambda_3$, which gives information on the spatial extend of the distribution of atoms,
 - the asphericity $b=\lambda_3-(\lambda_2+\lambda_1)/2$, which is 0 for distributions that are symmetric with respect to the three coordinate axes - e.g. in spherical symmetry,
 - the acylindricity $b=\lambda_2-\lambda_1$, which is 0 for distributions that are symmetric with respect to two coordinate axes - e.g. in cylindrical symmetry,
 - the relative shape anisotropy $\kappa^2=\frac{3}{2}\frac{\lambda_1^2+\lambda_2^2+\lambda_3^2}{(\lambda_1 + \lambda_2 + \lambda_3)^2}-\frac{1}{2}$, which is 0 for spherically symmetric distributions, and 1 for linear distributions.

The inertia tensor is defined as
$$
I_{ij} = \sum_{k=1}^Nm_k(|\mathbf{r}_k|^2\delta_{ij}-r_{i,k}r_{j,k})
$$
where symbols are as above.

A further geometrical descriptor can be derived from here: the aspect ratio is defined as the ratio between the smallest and largest eigenvalues of the inertia tensor.


## Common Neighbour Analysis (CNA)

CNA is an analysis of the properties of pairs of atom. For each pair, a _signature_ in the shape $(r,s,t)$ is provided, where: 
 - $r$ is the number of nearest neighbours shared by the two atoms,
 - $s$ is the number of bonds between the shared neighbours,
 - $t$ is the longest chain which can be made from bonding $s$ atoms if they are neighbours.

We can further define, for each atom, the list of signatures corresponding to pairs that this atom is part of. This list defines the CNA pattern (CNAP) of the atom

CNA signatures and CNAPs can help us perform structure identification and recognition. Let's see how to compute and deal with these objects in atomistic systems with pySNOW.


Here the references:

- The paper introducing the CNA: 
[Honeycutt and Andersen, J. Phys. Chem. 91, 4950](https://doi.org/10.1021/j100303a014)

- A useful discussion on decriptors, and a precursor of pySNOW: 
[Structural characterisation of nanoalloys for (photo)catalytic applications with the Sapphire library](https://doi.org/10.1039/D2FD00097K)


## (Generalized) coordination numbers in pySNOW

Coordination is a general and simple property of atoms. In the most basic case, coordination is a count of the number of neighbours of an atom, as we define the coordination number of the atom $i$ as 
$$
CN(i) = \sum_{j\in\mathcal{N}(i)}1 = n_i
$$
where $j$ runs over the $n_i$ atoms in the neighbourhood of the atom $i$: $\mathcal{N}(i)=\{\mathbf{r}_j:|\mathbf{r}_j-\mathbf{r}_i|<r_{cut}\}$, where $\mathbf{r}_\alpha$ is the position vector of the atom $\alpha$.

Naturally, we need to choose a cutoff $r_{cut}$ to define which atoms are neighbours and which are not. See our tutorial on PDDF for a discussion on this.

Some more complete and insightful information can be obtained from so-called generalized coordination numbers (GCNs), which take into account the coordination of neighbours as well to define the coordination of a site. In particular, GCNs are useful as descriptors of catalytic activity [1]. GCNs can be defined for atoms (_atop_ GCN - aGCN) or for sites generally considered as adsorption sites in atomistic systems (bridge - bGCN, three-fold hollow - thGCN, four-fold hollow - fhGCN) [2].

In the atop version:
$$
aGCN(i) = \frac{1}{CN_{max}} \sum_{j=1}^{n_i} CN(j)
$$
where $j$ runs over the $n_i$ neighbours of the atom $i$, and $CN_{max}$ is the coordination of atoms of the same species in the bulk (e.g. $CN_{max}=12$ for FCC materials).

For bridge and hollow sites, the sum over coordination of neighbours is performed over all the $n_i$ unique neighbours of the pair/triplet/fourplet $i$, and the max coordination is adjusted according to the number of corresponding neighbours in the bulk (in the case of FCC materials, $CN_{max}=18$ for bridge sites, $CN_{max}=22$ for three-fold hollow sites, and $CN_{max}=26$ for four-fold hollow sites).

Strained structures have different adsorption energies and catalytic activities compared to relaxed ones. To take this into account, one can consider a strain-aware version of the GCNs we discussed [3]. Here, strained is defined as 
$$
S = \frac{d_{ij}-d_{bulk}}{d_{bulk}}
$$
where $d_{ij}$ is the distance between atoms $i$ and $j$, and $d_{bulk}$ is the corresponding nearest neighbours distance in the unstrained bulk. A system-wide measure of the strain can be obtained considering the average distance between pairs of nearest neighbours $\bar{d}_{ij}$. This way, compressive strain is negative and tensile strain is positive, while $S=0$ indicates an unstrained/relaxed structure. 

The strain-aware version of GCN is then defined as
$$
GCN^*(i) = \frac{1}{CN_{max}}\sum_{j=1}^{n_i}\sum_{k=1}^{n_j} \frac{d_{bulk}}{d_{jk}} \approx \frac{1}{1+S}GCN(i)
$$

Here the reference works from F. Calle-Vallejo and coworkers:

[1 - Introduction to generalized coordination numbers](https://doi.org/10.1002/advs.202207644)

[2 -Bridge and hollow coordination numbers](https://doi.org/10.1021/acsomega.7b01126)

[3 - Strained generalized coordination numbers](https://chemistry-europe.onlinelibrary.wiley.com/doi/full/10.1002/cssc.201800569)



## Mean Squared Displacement (MSD)

The MSD of a trajectory is defined as:
$$
MSD(t) = \sum_{i=1}^N|\mathbf{r}_i(t)-\mathbf{r}_i(0)|^2
$$
where $\mathbf{r}_i$ is the positions vector of the $i$-th particle and $i$ runs over the $N$ particles in the system. The MSD is a convenient measure of diffusion and movement in an atomistic system.



## SAXS spectra

In order to calculate Small Angle X-Ray Scattering spectra of finite systems, we employ Debye's formula - spherically averaged - for the scattered intensity at given exchanged momentum **intensity**.

$$
 I(q) = \sum_{i,j} f_i(q) f^*_j(q) ~\text{sinc}(qr_{ij}) 
$$ 
Where
 - $i,j$ run over the indices of atoms 
 - $f(q)$ are the atomic form factors
 - $r_{ij}$ is the distance from atom $i$ to atom $j$

With some manipulation, the above formula becomes:

$$ 
I(q) = \int f_i(q) f^*_j(q) ~\text{PDDF}(r)~\text{sinc}(qr) 
$$





