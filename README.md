# sp3d5s_star

An c++ software package aimed at quantum mechanics based atomistic simulation of semiconductor nanostructures using empiracal tight binding model. 

## Main features of NanoTB are: 

Slater-Koster type sp3d5s* atomic basis semi-empirical parameters for main semiconductor materials; 

1D, 2D and 3D periodic structures of nanostructures up to millions of atoms; 

Electronic band structures, density of states projected to local atom orbitals.

Generate new  tight binding parameters from simulated-annealing algorithm.

# 1. Input files
## 1.1. control.inp 
Calculation setup, parameters 

## 1.2. kpt.inp

k-points，support openmpi parrallel calculation of k-points.

## 1.3. pos.inp 
Unit cell and atomic positions, similar to POSCAR.

## 1.4. mat.inp 
TB parameters。

## 1.5 ref-eigen.dat 
Referential eigenvalues, only appllicable in fitting mode(ISA=true). Usuallly get from DFT calculations, keep the same k-points mesh.

#2. Control.inp settings
```
# NanoTB control tags  '#' for
SYSTEM=TB  #(optional)the name of the system。
LPRD = 1 1 1    # periodic boundary conditions 1 1 1 for the three dimensions
EAVE = 0.3      # (optional)Eigenvalue middle point 
NCBAND = 40       # number of bands in eigenvalue calculation
SURFOFFSET = 5*0.18 # (optional) surface states
LBASIS = 1 1 1 1 5*1 1	# (optional)switch s p3 d5 s*  default for 1
LSOI = 1     	# spin-orbital interaction

#LHYDROGEN = 1 # pseudo-hydrogen(optional)。
VERBOSITY= High

NMATE = 1  # species of materials
BONDLENGTH = 3.2800000 #bond length in Angstrom. Should consistent with pos.inp to set the hopping between neighbor atoms
MATFNAM=mat.inp # the filename of TB-parameters



ISA=false #whether fitting the TB parameters using simulated annealing algorithm (SA).
ITBOUT=true # whether to update output when doing SA. set to false when ISA=true.

#SA parameters (optional, only appllicable when ISA=true)，See gsl manual (The GNU Scientific Library, http://www.gnu.org/software/gsl/)
N_TRIES=20 #
ITERS_FIXED_T=100
STEP_SIZE=1e-2
T_INITIAL=1e-3
T_MIN=1.0e-4
MU_T=1.108

# Add the weight of specific eigenvalues to the fitting object function. Can help to converge better to the desired eigenvalues.
FITK=6 0  # Add the weights of the sixth and the 0-th k-point, use with FITBAND
FITBAND=8 10 # Add the weights of the eighth and the tenth band of the sixth and the 0-th k-point. 
FITGAP=0.19 4.128574 # help to fit the band gap at the kpoints.
FITEIG=6 8 0.0 #help to fit the valence band maximum to 0.
```
