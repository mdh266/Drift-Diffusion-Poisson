# Introduction 

Solves the coupled drift-diffusion-Poisson that describe used to model 
a photoelectrochemical solar cell in 1D.  We use a mixed finite element
method for the Poisson equation and local discontinuous Galerkin method
along with implicit-explicit time stepping method for the drift-diffusion
equations. For more information see the documentation for this code.  Documenation
for the two vesion, http://michael-harmon.com/PECS/, gives further background on the
methods and model.


# Dependencies:
0. CMAKE 2.8   (Required)
1. GSL 1.16	(Required)
2. EIGEN 3.0   (Required)
4. BOOST       (Required)
3. OpenMP 	(Optional)


# Installing

cd into the downloaded directory with a terminal then:
1. mkdir build
2. cd build 
3. cmake  -DCMAKE_BUILD_TYPE=RELEASE ..
4. make solar_cell_app
5. mv solar_cell_app ../run



# Using
0. cd in run director.  If you want to use multi-threading use
		
		export OMP_NUM_THREADS=num_threads

1. Enter data in ddp-input.ini
2. command to run, in current directory type:
			
		./solar_cell_app

3. If you want to change the doping/concentration
	profiles change the file the ConcentrationProfile
	directory.  All units (densities and space are 
	in non-dimensional form).  You will need to
	recompile if you change this filel: aka.
	"cd build" and then type "make"

4.  DATA OUTPUT FILES
		 
		StateXXXX.dat:
	
	 when (xvalues < 0)
		 xvalues, electron density, hole density, electric field, potential, current, time

	 when	(xvalues > 0)
		 xvalues, reductant density, oxidante density, electric field, potential, current, time

5. plotter.py in directory run uses matplotlib and numpy to invoke:
		
		python plotter.py

6. To get rid of .dats, .png .mp4 invoke:
		
		./clean.sh

7. Edit and use Runner_IV.py if you want to run this over multiple 
    bias values.


# Testing

same as INSTALL steps 1-3
	 make test_System
	 ./test_System



# Documentation

A documentation is provided into the /doc/ directory.  You must have
doxygen and latex installe in order to build it.  Once in the
directory type 

	doxygen dox

and a html file website we be built in the directory /html/.  This
can be viewed from any webbrowser.


# Trouble Shooting
* If oscillations appear in semiconductor domain(usually on the electron densities) 
use a smaller the timeStepFactor. 

**NOTE: will slow down run time.**

* Negative values/spikes/stability issues (NANs), increase the numBoundaryElements (make sure to 
increase numElements so that numBoundaryElementsremains less than numElements). 
Also if this issue area is outside of the boundaryLayerWidth, incrase boundaryLayerWidth 
so that it covers these issue areas.  

**NOTE: will slow down run time**