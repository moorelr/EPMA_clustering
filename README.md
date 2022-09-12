# EPMA_clustering

Rev. 9/12/2022 LRM

This repository is part of my ongoing effort to explore different methods for segmenting microprobe image stacks by mineralogy.  The ideal solution to this problem is a program that loads a group of images collected at the same location, determines the number of minerals present in the mapped area, and then identifies which one of these minerals is present at a given pixel.  Yes, there is already software that does this. :)

Data in this repository come from the Cameca SX-50 electron microprobe at Virginia Tech.

Here are some of the things I have tried so far:
1) K-means clustering in ImageJ
    - Load the images into ImageJ
    - Convert the images into a IJ stack
    - Use an IJ plugin to perform K-means clustering
 
2) Just Heirarchical cluster analysis (HCA) in R
    - Use the "raster" and "rgdal" packages to open the images as several "raster" objects
    - Combine these into a dataframe
    - use the "hclust" base-R function to identify clusters among the pixels

3) HCA + artificial neural network (ANN)
    - Load three of the iages into ImageJ and create a composite RGB image
    - Flag some number of "good pixels" representing diferent minerals away from cracks, pores, and grain boundaries
    - Load the images in R as in method 2), but this time use the "flagged" pixels to create the HCA model
    - Use these clusters as training data for the ANN
    - Calculate the cluster ID for all pixels in the mapped area using the ANN model

In all of the methods I have tried so far, a major problem has been that the clustering algorithms identify grain boundaries and zoning within large minerals as distinct phases.  I suspect that just manually selecting clusters from a set of three maps that produces an RGB image with a wide range of hues is probably an adequate method.

