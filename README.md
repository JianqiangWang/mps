*mps* - 3D incompressible fluid dynamics solver by using moving particle semi-implicit(MPS) method with Fortran.  
        the code is parallelized by OpenMP.
======
moving particle semi-implicit(MPS) method: http://li.mit.edu/Stuff/CNSE/Paper/Koshizuka96Oka.pdf  
currently intel compiler is required to build it.  
  
how to run:  
~~~~
$ vi mps.F90 # adjust the parameters  
$ make  
$ ./mps  
$ ./create_anime.sh  
~~~~
  
TODO:  
---
- implement ICCG method and replace CG method with it
- create a function to find neighbor particles in the effective radius(using hash table is better?)
- continue the verification
- parallelize the code by MPI
- still some particles are running away from the box, so modify the code not to calculate the escaped particles

performance comparison:
---
parameter setting for the performance comparison:  
~~~~
nparticles_fluid = (/8, 16,16/)  
nparticles_box   = (/32,16,16/)  
dist_particles   = 7.5d-2  
tol = 1.0d-30  
dt  = 3.0d-3  
tstep_max  = 200  
~~~~
Intel(R) Xeon(R) CPU E5-2650 v3 @ 2.30GHz, 20 cores, with AVX2  
wtih 1 core  : 4243.89s  
with 20 cores:  434.99s  
---
a calculation result(water collapse in a box) is below.  
in this case, size of the box is 2.4x1.2x1.2(m), size of the water in the initial state is 0.6x1.2x1.2(m), time is 0.0~6.0(s)(2000 steps).  
it took about 1h30m with 20 cores to calculate the process.  
![Alt text](./water_collapse.gif?raw=true "water collapse")
