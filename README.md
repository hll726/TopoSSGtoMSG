# TopoSSGtoMSG
The TopoSSGtoMSG package enables the computation of topological properties of arbitrary collinear magnets under both spin space groups and magnetic space groups, encompassing the vanishing spin–orbit coupling (SOC) regime, the negligible-SOC limit, and the realistic-SOC case for various magnetic-moment orientations. This unified framework provides a systematic means to elucidate how SOC, together with the orientation of magnetic moments once SOC is included, reshapes the topological characteristics of materials.
   
# Installation
   - unzip the TopoSSGtoMSG-V1.zip file
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

Here, *E* denotes the identity operation, and *T* denotes the time-reversal operation, which reverses the spin. Next, we introduce the **CheckDegenarcy** module, which displays the names and degeneracies of the irreducible (co-)representations at high-symmetry points, high-symmetry lines, high-symmetry planes, or generic **k** points *(u, v, w)* under either the collinear spin space group or the magnetic space group determined by a specific class of magnetic-moment orientations. This module is useful for understanding the degeneracies of symmetry-enforced band crossings in case III, which are identified by the core module **GetTopfilling**, introduced below.

```mathematica
CheckDegenarcy["65.1.2.5.L", 0]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/ssg.png" alt="Lattice" width="80%">

```mathematica
CheckDegenarcy["65.1.2.5.L", 4]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msg.png" alt="Lattice" width="80%">

unzip the TopoSSGtoMSG-V1.zip file

<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/topossgtomsg.png" alt="Lattice" width="80%">

```mathematica
GenKpath["65.1.2.5.L", 0]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/kpath1.png" alt="Lattice" width="40%">

```mathematica
GetTopfilling["65.1.2.5.L", 0, 0, 0]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/ssgtopology.png" alt="Lattice" width="100%">

```mathematica
GetTopfilling["65.1.2.5.L", 4, 0, 1]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msgtopology3.png" alt="Lattice" width="40%">

```mathematica
GenKpath["65.1.2.5.L", 4]
(* Collinear spin space group 65.1.2.5.L *)
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



