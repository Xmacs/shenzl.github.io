---
layout: default
title: 模拟中添加cation-pi相互作用
---

## 模拟中添加cation-pi相互作用
#### Blockage of Water Flow in Carbon Nanotubes by Ions Due to Interactions between Cations and Aromatic Rings

[文献链接](http://journals.aps.org/prl/abstract/10.1103/PhysRevLett.115.164502)
##### 摘要

> Combining classical molecular dynamics simulations and density functional theory calculations, we find that cations block water flow through narrow (6,6)-type carbon nanotubes (CNTs) because of interactions between cations and aromatic rings in CNTs. In wide CNTs, these interactions trap the cations in the interior of the CNT, inducing unexpected open or closed state switching of ion transfer under a strong electric field, which is consistent with experiments. These findings will help to develop new methods to facilitate water and ion transport across CNTs.
#### 总结
#### 附加代码（文献提供）

``` tcl
  set zmax 8.6
  set lambda 1.6
  set Pi 3.14159265
  proc calcforces {step unique eps} {
    global zmax lambda Pi
    while {[nextatom]} {
      if { [getmass] < 22.9 || [getmass] > 23.0} {
        dropatom
        continue
      }
      set z [lindex [getcoord] 2]
      set f [expr 1.1*$eps*$lambda/$Pi* \ (1/(($lambda*($z+$zmax))**2+1) - 1/(($lambda*($z-$zmax))**2+1))]
      addforce [list 0 0 $f]
      addenergy [expr 1.1*$eps/$Pi* \ (atan($lambda*($z-$zmax)) + atan($lambda*(-$z-$zmax)))]
    }
  }
```
