# emtools
<strong>Tools for electron microscopy data analysis</strong>

<code>transform\_particles.py</code> applies a <a href="https://en.wikipedia.org/wiki/Transformation_matrix">transformation matrix</a> to all particles in a provided RELION star file. <code>transform\_particles.py</code> is able to read and write RELION star files contaning the relevant columns (\_rlnAngleRot, \_rlnAngleTilt, \_rlnAnglePsi, \_rlnOriginXAngst and \_rlnOriginYAngst, or \_rlnOriginX and \_rlnOriginY, in older RELION versions) from versions earlier and later than 3.1.

The easiest way to manage the libraries needed to run the transform_particles.py  script is to install <a href="https://www.anaconda.com/products/individual">Anaconda</a>, and use it to generate the <code>py37</code> environment, with a version scipy that has the Rotation object.

1) Install Anaconda following the instruction in their website.

2) Clone this repository:

<code>git clone https://github.com/basantab/emtools.git</code>

<code>cd emtools</code>

3) Create <code>py37</code> using the provided .yml file:

<code>conda env create -f ./py37.yml</code>

4) Before running <code>transform\_particles.py</code>, activate the py37 environment using <code>conda activate py37</code>.

5) Run <code>transform\_particles.py</code>, like in this example:

<code>python transform\_particles.py --starfile your\_star\_file.star --transformation\_mtx [[0.98364538,-0.15451987,0.09254928,4.25534352],[0.15692689,0.48301307,-0.86143620,-5.85090884],[0.08840650,0.86187121,0.49936190,12.25449899]] --angpix 1.15</code>

In this example, all particles in your\_star\_file.star are transformed using the following transformation matrix:

<code>[[0.98364538,-0.15451987,0.09254928,4.25534352],</code>

<code>[0.15692689,0.48301307,-0.86143620,-5.85090884],</code>

<code>[0.08840650,0.86187121,0.49936190,12.25449899]]</code>

In this matrix, the fourth column is the translation in X, Y and Z, and it's in Angstroms. A matrix like this can be obtained from aligning two densities in UCSF Chimera (keep in mind manual manipulations will not be reflected in the output matrix) using the fitmap command. If using UCSF Chimera, make sure you set the Origin index (Volume viewer \> Features \> Coordinates) of your densities to "center", that way the transformation matrix will reflect the desired transformation. Also, note that the transformation is not done on the raw micrographs, the star file must be populated with assigned particle Euler angles and rotation origin shifts.
