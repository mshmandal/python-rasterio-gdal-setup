### Setup python for image analysis
For this tutorial I am going to use python 3.9.1 and windows 10 64-bit installations


#### Step 1. Install python 

   - Python version 3.9.1 [Download](https://www.python.org/downloads/)

   - Download and install python for all the users and check the box that saying "add python to path variables"

   - Check in command line which version is running using

```{r, eval=FALSE}
python --version
```
   - The return should give the python version. If this is does not match, then trying previous steps again.
```{r, eval=FALSE}
Python 3.9.1
```


#### Step 2. Create separate python environment

  - It is better to create an separate python environment for our image analysis setup. This is prevent any conflict with other installation and ensure reproducibility. 
  - create an folder and "cd" to the directory 
```python
mkdir c:\pygis
cd c:\pygis
```
  - Create an environment and activate it using following command

```python
python -m venv raster # replace raster with the environment name
raster\Scripts\activate # to activate the environment
```

#### Step 3. Pip install required packages
   
   - Using pip we will install required packages
   
```python
pip install -r requirements.txt
```


#### Step 4. Install GDAL and rasterio
   - We will use GDAL whell for our python setup. Go to this [website] (https://www.lfd.uci.edu/~gohlke/pythonlibs/#gdal) which provides official python binaries for many python packages developed by Christoph Gohlke, Laboratory for Fluorescence Dynamics, University of California, Irvine.
   - We will use GDAL-3.1.4-cp39-cp39-win_amd64.whl and rasterio-1.1.8-cp39-cp39-win_amd64.whl version for our GDAL and rasterio setup
   - Download the files in your root directory for python environment
   
```python
 pip install raster\GDAL-3.1.4-cp39-cp39-win_amd64.whl # install GDAL
 pip install raster\rasterio-1.1.8-cp39-cp39-win_amd64.whl #install rasterio
```
   
#### Step 5. Install other packages

   - One great way to keep track of packages is listing required packages in a text file and install them 
   
   - create a text file inside your environment, this case "raster" name it as requirements.txt
   
   - inside the file list following packages, you can add new packages in new line if you want. In this way we can install the version we want and also check the file whenever we want
   
```
numpy
scikit-learn
matplotlib
pandas
jupyterlab
```
   
#### Step 6. Run Jupyter notebook and read data

  - Run jupyter notebook 
  
```python
jupyter-lab # run jupyter-notebook
```
  - Create a notebook and name it as you prefer
  - import library to read data

```python
import rasterio
from rasterio import plot
import matplotlib.pyplot as plt
%matplotlib inline
```
   - Read image path directory and list files

```python
path='./image/' # path to image files
# list files in the folder
import os
files = os.listdir(path) #'C:/Users/ecoremo/Documents/pygis/raster/image'
for f in sorted(files):
  print(f) # doest not sort naturally
```

   - Read blue, green and red bands
```python
blue = rasterio.open(path+'1.tif')
green = rasterio.open(path+'2.tif')
red = rasterio.open(path+'3.tif')
```

   - Plot three bands 
   
```python
# plot blue, green and red 
fig, (ax1, ax2, ax3) = plt.subplots(1,3, figsize=(12,4))
plot.show(blue, ax=ax1, cmap="Blues")
plot.show(green, ax=ax2, cmap="Greens")
plot.show(red, ax=ax3, cmap="Reds")
fig.tight_layout()
```