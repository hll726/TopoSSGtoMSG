# TopoSSGtoMSG
The TopoSSGtoMSG package enables the computation of topological properties of arbitrary collinear magnets using high-symmetry-point wave functions obtained from VASP under both spin space groups and magnetic space groups. It encompasses the vanishing spin–orbit coupling (SOC) regime, the negligible-SOC limit, and the realistic-SOC case for various magnetic-moment orientations. This unified framework provides a systematic means to elucidate how SOC, together with the orientation of magnetic moments once SOC is included, reshapes the topological characteristics of materials.
   
# Installation
   - unzip the TopoSSGtoMSG-V1.zip file.
   - Open a Mathematica notebook.
   - Run Import["Dir\TopoSSGtoMSG.wl"] where Dir is the path to the TopoSSGtoMSG.wl file.
   - After running, a folder selection prompt will appear. Select the folder containing TopoSSGtoMSG.wl.

# Tutorial
Using the collinear altermagnetic material 0.402_Sr<sub>4</sub>Fe<sub>4</sub>O<sub>11</sub> as an example, we introduce how to use the various modules of **TopoSSGtoMSG**. The first module, **CheckSSGinfo**, provides the basic information of the spin space group *G* of the material, including the primitive lattice vectors, the nontrivial part of the collinear spin space group operations, and the classification of magnetic-moment directions in the collinear spin space group *G*. It should be noted that any spin group operation can be written in the form {R_s || R_r | τ}, where R_s denotes the operation in spin space, while R_r and τ are the rotational and translational parts of the corresponding real-space group operation, respectively. For the nontrivial part of the spin group, for convenience, we represent the real-space group operation by its action on the fractional coordinates (x, y, z) defined with respect to the primitive basis vectors **a<sub>1</sub>**, **a<sub>2</sub>**, and **a<sub>3</sub>**. That is, an arbitrary spin group operation is written as {R_s || R_r (x, y, z) + τ}. For altermagnetic 0.402_Sr<sub>4</sub>Fe<sub>4</sub>O<sub>11</sub>, the corresponding spin space group is *G* = 65.1.2.5.L, where the notation of spin space groups follows that on https://cmpdc.iphy.ac.cn/ssg/.


```mathematica
CheckSSGinfo["65.1.2.5.L"]
(*CheckSSGinfo[SSGname], SSGname denotes the name of the collinear spin space group*)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/ssgoperationandmmd.png" alt="Lattice" width="50%">

Here, *E* denotes the identity operation, and *T* denotes the time-reversal operation, which reverses the spin. The quantities *n*<sub>x</sub>, *n*<sub>y</sub>, and *n*<sub>z</sub> are the components of the unit vector of the magnetic-moment direction along the *x*-, *y*-, and *z*-axes in the Cartesian coordinate system. Next, we introduce the **CheckDegenarcy** module, which displays the labels and degeneracies of the irreducible (co-)representations at high-symmetry points, high-symmetry lines, high-symmetry planes, or generic ***k***-points *(u, v, w)* under either the collinear spin space group or the magnetic space group determined by a specific class of magnetic-moment orientations. This module is useful for understanding the degeneracies of symmetry-enforced band crossings in case III, which are identified by the core module **GetTopfilling**, introduced below. First, we present the results for the spin space group *G* = 65.1.2.5.L.

```mathematica
CheckDegenarcy["65.1.2.5.L", 0]
(*CheckDegenarcy[SSGname, momclass], SSGname denotes the name of the collinear spin space group and momclass = 0 corresponds to calculations without SOC (under spin space group)*)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/ssg.png" alt="Lattice" width="80%">

Then, we present the results for the magnetic space group 65.486 (Belov–Neronova–Smirnova notation, magnetic space group type III), which is determined by selecting class 4 (1, 0, 0) of magnetic-moment directions in the spin space group *G* = 65.1.2.5.L.

```mathematica
CheckDegenarcy["65.1.2.5.L", 4]
(*CheckDegenarcy[SSGname, momclass], SSGname denotes the name of the collinear spin space group and momclass ≠ 0 corresponds to calculations with SOC.
The specific nonzero value of momclass labels the corresponding class of magnetic-moment orientations in the given collinear spin space group*)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msg.png" alt="Lattice" width="80%">

Next, we introduce how to use **TopoSSGtoMSG** to compute the topology of collinear magnetic materials. Here, we consider three cases: without SOC (the topology is diagnosed by the spin space group), the negligible-SOC limit (the topology is diagnosed by the magnetic space group), and the realistic-SOC case (the topology is diagnosed by the magnetic space group). For the latter two cases, various magnetic-moment orientations can be considered. The computational workflow is illustrated in the flowchart below.


<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/topossgtomsg.png" alt="Lattice" width="80%">

Specifically, the workflow can be divided into three steps. The first step is a self-consistent VASP calculation. The second step is a non-self-consistent calculation to obtain the wave functions at high-symmetry points, where the content of the **KPOINTS** file is generated by the **GenKpath** module. The third step is the topological analysis, which is performed using the **GetTopfilling** module and requires the **WAVECAR** and **OUTCAR** files generated in the second step. Here, `GetTopfilling[SSGname, momclass, v, n]` computes, in parallel, the band topology at relative electronic filling *v* (electron filling minus N<sub>e</sub>, where N<sub>e</sub> is the number of valence electrons). The meaning of the parameters is as follows:
1. *momclass* = 0 and *n* = 0 correspond to calculations under the collinear spin space group in the vanishing spin–orbit coupling limit. 
2. *momclass* ≠ 0 and *n* = 0 correspond to calculations under the magnetic space group determined by a specific class of magnetic-moment orientations, with realistic spin–orbit coupling. 
3. *momclass* ≠ 0 and *n* = 1 correspond to calculations under the magnetic space group determined by a specific class of magnetic-moment orientations in the negligible spin–orbit coupling limit. 

The resulting topological classifications are divided into three cases:

- case **I**: possibly trivial.
- case **II**:all band crossings (nodal points or nodal lines) at generic ***k***-points under spin space group, or magnetic topological insulators/Weyl semimetals under magnetic space group.
- case **III**: symmetry-enforced band crossings at high-symmetry points, high-symmetry lines, high-symmetry planes, or generic ***k***-points (*u*, *v*, *w*).


Below, we illustrate the computational procedure using the altermagnetic material 0.402_Sr<sub>4</sub>Fe<sub>4</sub>O<sub>11</sub> (*U* = 0 eV) as an example. We first introduce how to compute the topology in the absence of SOC, which is diagnosed by the spin space group. First, perform the self-consistent calculation. After it is completed, use the **GenKpath** module to generate the **KPOINTS** file required for the non-self-consistent calculation. For 0.402_Sr<sub>4</sub>Fe<sub>4</sub>O<sub>11</sub> (*U* = 0 eV), the results are as follows.

```mathematica
GenKpath["65.1.2.5.L", 0]
(*GenKpath[SSGname, momclass], SSGname denotes the name of the collinear spin space group and momclass = 0 corresponds to calculations without SOC (under spin space group)*)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/kpath1.png" alt="Lattice" width="40%">

Place the **WAVECAR** and **OUTCAR** files obtained from the non-self-consistent calculation into a folder (e.g., `dir1`). Then run the following command. A folder-selection prompt will appear; select the folder `dir1` and wait for the calculation to complete.

```mathematica
GetTopfilling["65.1.2.5.L", 0, 0, 0]
```


计算的结果
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/ssgtopology.png" alt="Lattice" width="100%">

```mathematica
GetTopfilling["65.1.2.5.L", 4, 0, 1]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msgtopology3.png" alt="Lattice" width="40%">

```mathematica
GenKpath["65.1.2.5.L", 4]
(**GenKpath[SSGname, momclass], SSGname denotes the name of the collinear spin space group and momclass ≠ 0 corresponds to calculations with SOC.
The specific nonzero value of momclass labels the corresponding class of magnetic-moment orientations in the given collinear spin space group*)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/kpath2.png" alt="Lattice" width="40%">

```mathematica
GetTopfilling["65.1.2.5.L", 4, 0, 0]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msgtopology2.png" alt="Lattice" width="100%">

# References
L. Huang, X.Wan, and F. Tang, “Prediction of magnetic topological materials combining spin and magnetic space groups,” (2026), arXiv:2601.05142.

# Contact

L. Huang: 602025220022@smail.nju.edu.cn

# Note



