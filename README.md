# TopoSSGtoMSG
The TopoSSGtoMSG package enables the computation of topological properties of arbitrary collinear magnets under both spin space groups and magnetic space groups, encompassing the vanishing spin–orbit coupling (SOC) regime, the negligible-SOC limit, and the realistic-SOC case for various magnetic-moment orientations. This unified framework provides a systematic means to elucidate how SOC, together with the orientation of magnetic moments once SOC is included, reshapes the topological characteristics of materials.

# Introduction
 - unzip the TopoSSGtoMSG-V1.zip file
   
# Installation
   - unzip the TopoSSGtoMSG-V1.zip file
   - Open a Mathematica notebook.
   - Run Import["Dir\TopoSSGtoMSG.wl"] where Dir is the path to the TopoSSGtoMSG.wl file.
   - After running, a folder selection prompt will appear. Select the folder containing TopoSSGtoMSG.wl.

# Tutorial

```mathematica
CheckSSGinfo["65.1.2.5.L"]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/ssgoperationandmmd.png" alt="Lattice" width="50%">

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
GetTopfilling["65.1.2.5.L", 0, 0, 0]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msg.png" alt="Lattice" width="80%">

```mathematica
GetTopfilling["65.1.2.5.L", 4, 0, 0]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msg.png" alt="Lattice" width="80%">

```mathematica
GetTopfilling["65.1.2.5.L", 4, 0, 1]
(* Collinear spin space group 65.1.2.5.L *)
```
<img src="https://github.com/hll726/TopoSSGtoMSG/raw/main/src/msg.png" alt="Lattice" width="80%">


# Contact

L. Huang: 602025220022@smail.nju.edu.cn


