# cell-identifier
Mathematica files used to identify cells in flourescence videos.
------------------------------------------------------------------------------
This file is used to detect beta-pancreatic cells. It reads in .tif stacks obtained from a fluorescence microscope. Individual cell signals for the experiment can be obtained.
------------------------------------------------------------------------------
Reads in a .tif file.

The steps taken to identify the cells and segment the image are as follows:

  1- Two images are created from the stack. Max pixel value image and high-percentile pixel value image. These two images are averaged to obtain a sample image of the stack.
  
  2- Two new images are created from the sample image, k and 2k. Image k is the sample image blurred with a gaussian filter with kernel size k. Image 2k is the sample image blurred with a kernel size of 2k.
  
  3- A bandpass image is created by subtracting image 2k from k. bandpassImage = k - 2k.
  
  4- Distance transform is applied to the bandpass image and the centers of each cell is identified.
  
  5- Using Mathematica's watershed algorithm with a minimum saliency of 0.8, seeds as the peaks from the distance trnsform, and the background as the morphological binarized version of the distance transform.

After segmentation, individual cell signals can be exported as the mean signal and sum signal as well as the cell position (centroid) and cell index in the list of watershed components.
