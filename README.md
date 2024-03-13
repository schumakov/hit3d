# General

This code is a pseudo-spectral DNS code for simulation of homogeneous isotropic incompressible turbulence in three dimensional space. It is aspiring to be a standard code for DNS of isotropic homogeneous turbulence in triple-periodic box.

The features include: 
* MPI framework
* * currently has been tested for OpenMPI and MVAPICH on variety of NSF and DOE clusters * FFTW3 is used for Fourier transforms. See http://www.fftw.org for details. * Lagrangian particles (tracers) to gather Lagrangian statistics. * Ability to perform Large-Eddy Simulation (LES), several models are implemented.

The code is released under the GNU Public License.

With any questions, contact the project owner or visit http://schumakov.info

When using HIT3D for your research, please cite the following papers and provide the URL: * SG Chumakov, A priori study of subgrid-scale flux of a passive scalar in turbulence, Phys. Rev. E, 78 15563 (2008) * SG Chumakov, Scaling properties of subgrid-scale energy dissipation, Phys. Fluids, 19 058104 (2007) * http://hit3d.googlecode.com


# Dependencies

The code is written in Fortran 90 and uses the two open libraries:

* Open-MPI  (www.open-mpi.org) - MPI implementation.  Does not have to be Open MPI, but recommended.
* FFTW3	    (www.fftw.org)


# Website
http://chumakov.info/codes-hit3d.php

# Copyright, Licensing and Disclaimer
Copyright (C) 2006-2017 Sergei Chumakov, Natalia Vladimirova, Misha Stepanov

The code is distributed under the terms of GNU GPLv3 license.  

You can read the full text of the license at http://www.gnu.org/licenses/gpl.html

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
