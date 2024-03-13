# HIT3D - Homogeneous Isotropic Turbulence in 3D

----

### When using HIT3D for your research, please cite the following papers and provide the URL: 
* SG Chumakov, A priori study of subgrid-scale flux of a passive scalar in turbulence, Phys. Rev. E, 78 15563 (2008)
* SG Chumakov, Scaling properties of subgrid-scale energy dissipation, Phys. Fluids, 19 058104 (2007)
* http://github.com/schumakov/hit3d

With any questions, contact the project owner or visit http://chumakov.info

----



HIT3D is a pseudo-spectral DNS code for simulation of homogeneous isotropic incompressible turbulence in three dimensional space. It is aspiring to be a standard code for DNS of isotropic homogeneous turbulence in triple-periodic box.
The code 
* is written in Fortran 90
* is parallelized using MPI 
* uses FFTW3 is used for Fourier transform (http://www.fftw.org)
* can employ Lagrangian particles (tracers) to gather Lagrangian statistics
* is released under the GNU Public License.


## Dependencies
The code is written in Fortran 90 and uses the two open libraries:
* Open-MPI  (www.open-mpi.org) - suggested MPI implementation.  Other MPI implementations such as MVAPICH and Intel MPI whould work as well.  The code uses standard MPI communication calls.
* FFTW3	    (www.fftw.org)

## Website
http://chumakov.info/codes-hit3d.php


## Instructions

### How to compile
* First, edit the Makefile:
  * add a section that corresponds to the name of your machine.  Ideally it should be a wrapper from your MPI implementation.
  * define the name of the F90 compiler
  * define FCFLAGS and LDFLAGS.  They should include the include directories, the flags that link FFTW3 and MPI implementation.
* Run "gmake"


### How to run
The directory `scripts` provides some examples of the batch job submission files.
* `00_example.in` 	a sample input file
* `snapshot.gp`	a Gnuplot instruction file that creates two plots that can get attached to the notification emails 


### The input file breakdown
```
  NX,NY,NZ  Number of grid points in one dimension.
            The grid will be NX x NY x NZ. The physical dimensions will be 2*pi x 2*pi x 2*pi

  ITMIN	The timestep number of the restart file.  The restart files have names
        such as "test__this.64.123456".  Here, "test__this" is the run name, 
        "64" signifies that the file is written with double precision and 
	      "123456" is the timestep number.  If the ITMIN is set to 0, the 
	      subroutine that defines	the initial conditionis for the flow is called.

ITMAX	The maximum number of timesteps in the simulation.

IPRNT1	How often to generate the statistics.

IPRNT2	How often to write restart files

IWRITE4	How often to write the real*4 files that are used for post-processing.

TMAX	The runtime of the simulation (not the wallclocok time)

TRESCALE  The time at which to rescale the velocity.  This is used in decaying
	  simulations when we want to establish some correlations first and 
	  then rescale the velocity field so it has higher kinetic energy.

TSCALAR	  When to start moving the passive scalars.

flow_type   Parameter that switches the flow type
	          0 - decaying turbulence
	          1 - forced turbulence

RE	  The local Reynolds number (1/nu, where nu is dynamic viscosity)

DT	  The timestep.
	    If DT is negative, then the timestep is fixed to be (-DT)
	    If DT is positive, the timestep is found from the stability
	    criteria for the time-stepping scheme that is used.

ISPCV1   Initial spectrum type (see init_velocity.f90)
mv1      initial infrared exponent in the spectrum
wm0v1    initial peak wavenumber in the spectrum


force_type	   The type of the forcing that is applied for the case of
		           forced turbulence.
		           1 - forcing from Michaels PRL paper (PRL #79(18) p.3411)
		           So far no other forcing has been implemented

KFMAX	  The upper bound for the forcing band in the Fourier space.

FAMP	  The magnitude of the forcing (usually set to 0.5)

det_rand 	  The parameter that switches the random generation for the
		        random seeds for the code.
	          DEFUNCTIONAL.  In the current version of the code, the seeds for the
	          random number generator are fixed and are taken from the input file.
	          The fixed seeds have the effect of producing the initial data that
	          looks similar for different resolutions (the large features of 
	          initial flow in 32^3 simulation will look similar to the large features
	          of a 1024^3 simulation if the seeds are the same).

RN1, RN2, RN3  - random number seeds


DEALIAS		The parameter that switches between the dealiasing algorithms.
	        0 - the standard 3/2-rule (or 2/3 rule).  Faster computations, but
	        fewer modes.
	        1 - the phase shift combined with truncation.  This retains much more
	        modes than the 2/3-rule, while increasing the computations 60% or so.
	        The most economical mode for DNS in terms of flops per the number of
	        Fourier modes in the resulting data.

np	      The number of Lagrangian particles

*         particle tracking mechanism:
	        0 - trilinear interpolations
	        1 - 4-point cubic interpolation
	
time_p    time in the simulation when to release the particles in the flow

particle_filter_size
          The particles can be advected by fully resolved field or by locally averaged
	        field.  The filter size determines the size of the filter that is applied
	        to the velocity field before computing the particles' velocities.
          (set to 0.0 to disable)

les_model  The LES model.  Currently not debugged and should not be used.

NUMS  The number of passive scalars to carry around

The last section contains the parameters of the passive scalars.  Each scalar
has four parameters: the type, Schmidt number, infrared exponent, peak wavenumber and 
reaction rate.

The first parameter is the scalar type.
TYPE:
0	The scalar that is forced by the mean gradient.
1-9	The initial conditions for the scalar are generated using Fourier space.
	1: Exponential spectrum
	2: von Karman spectrum
	3: double-delta PDF
>10	The initial conditions for the scalar are generated in the real space.
	11: single slab of the scalar.
	12: two slabs of the scalar
	13: 1-D sinusoidal wave of the scalar
The second and third parameters are Schmidt number and peak wavenumber.
Peak wavenumber is used when initializing scalars in Fourier space.
The fourth parameter (reaction rate) is not used in this version of the code.

```


### Copyright, Licensing and Disclaimer
Copyright (C) 2006-2024 Sergei Chumakov, Natalia Vladimirova, Misha Stepanov

The code is distributed under the terms of GNU GPLv3 license.  

You can read the full text of the license at http://www.gnu.org/licenses/gpl.html

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
