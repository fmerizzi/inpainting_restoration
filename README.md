# inpainting_restoration
Affreschi restoration with inpainting

As a part of an intership at I3S lab, I approach the task of affreschi digital restoration.
the general goal of the project is as follows: 

1) select high resolution pictures of the damaged affreschi 
2) produce a proper mask for inpainting
3) test traditional algorithms 
4) test deep image prior technique 

### file list 

- [inpainting_basicsComparison.ipynb](https://github.com/fmerizzi/inpainting_restoration/blob/main/inpainting_basicsComparison.ipynb), testing "traditional" methods for image inpainting, using opencv library. Fast Marching Method and algorithm proposed by Sapiro in 2001.
- [inpainting_deepImagePrior.ipynb](https://github.com/fmerizzi/inpainting_restoration/blob/main/inpainting_deepImagePrior.ipynb), testing the deep image prior technique for image inpainting, with different architectures and parameter settings

### considerations on the making the of the mask 
I considered several approaches on the creation of the mask selecting damaged areas, reported below:

1) __color based selection__, in this first attempt I selected a range of colors related to the damaged parts of the painting, however this selection proved to be too general, and its almost impossible to select only the damaged parts, producing masks that perform poorly.
2) __"magic wand" method__, in this supervised method we select both a color sample and a coordinate, and we expand the selection from the coordinate to the adjacent pixels that match our color sample to a certain degree. The quality of this selection is much greater than the simple color based selection, and the results are convincing. However, upon testing, the quality of the inpainting was poor. We consider this problem to arise because this method leave "exposed" the edges of the patch, the in-between areas where the color changes; this areas are then used by the network to recreate the patch. This results suggest that the best method to create masks is to __completely cover the damaged area__
3) __manual selection__, the final method used in our experiments is to simply create the masks manually, usually a paint tool, and making sure to completely cover the damage. The mask being slightly bigger than the damaged area proved not to be a problem for neural inpainting. 



### preparing the mask 
![preparing](https://github.com/fmerizzi/inpainting_restoration/blob/main/prepare.png)

### producing the result 
![result](https://github.com/fmerizzi/inpainting_restoration/blob/main/detail2_full256.jpeg)

