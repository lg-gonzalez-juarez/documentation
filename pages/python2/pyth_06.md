---
title: 26. Using SciKit-image
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_06.html
folder: python2
---


## 26.1. NumPy and Scikit-Image

scikit-image is an open-source package for image processing. It has a wide range of algorithms that allow you to process your images. Documentation can be found [here](https://scikit-image.org/docs/stable/).

In this lesson, we are going to take a look at how to load an image into scikit-image and examine the NumPy array that results.

### Installation

To install scikit-image:

```powershell
python -m pip install scikit-image
```

### Loading an Image

First, we need to get the photo we are planning to use. In this case, the photo is one I took of some flowers.

```powershell
/home/cloud_user/notebooks
```

```powershell
curl -O https://raw.githubusercontent.com/linuxacademy/content-using-pythons-maths-science-and-engineering-libraries/master/flowers.jpg/home/cloud_user/notebooks/lesson1.py```
```

```powershell
# %%
import numpy as np
from skimage import io

img = io.imread('flowers.jpg')
io.imshow(img)
type(img)
img.shape
```

We should make a backup of the picture before proceeding. The file extension (.jpg, .tiff) tells Jupyter the format in which it will be saved.

Let's make a backup of the picture:

```powershell
io.imsave("img_bup.jpg", img)
io.imsave("img_bup.tiff", img)
```

## 26.2. Image Data Types

This lesson continues from our previous lesson on NumPy and Scikit-Image, and we'll review how data is stored and data types.

In case you have shut your server down, please reload the image file as we did in the previous lesson.

```powershell
# %%
import numpy as np
from skimage import io

img = io.imread('flowers.jpg')
io.imshow(img)
img.shape
img[0][0]
```

The image data is composed of arrays of 3 representing the RGB values.

Notice this data type (```dtype```) is ```uint8```. The ```u``` means unsigned, the ```int``` means integer, and the ```8``` means 8-bit. In other words, the data is a number between 0 and 255. These are the values used to represent colors in the RGB (Red, Green, Blue) color model.

## 26.3. Transforming Images

This lesson continues from the previous lesson and reviews how we can work with the image and colorspaces.

In case you have shutdown your server, re-load the image:

````powershell
# %%
import numpy as np
from skimage import io

img = io.imread('flowers.jpg')
io.imshow(img)
````

As you can see, the image is shown with axes values. These correspond to ````img[i][j]````, where ````i```` represents the vertical axis, and ````j```` represents the horizontal axis.

````powershell
img[250][1500]
````

As such, we can change the color of any pixel just by accessing it and changing the three-number array. Let's create a banner along with the top showing blue, green, and white. We can split these by x values:

````powershell
for i in range(500):
    for j in range(1000):
        img[i][j][0] = 51
        img[i][j][1] = 0
        img[i][j][2] = 255
    for k in range(1000, 2000):
        img[i][k][0] = 204
        img[i][k][1] = 255
        img[i][k][2] = 51
    for l in range(2000, 3000):
        img[i][l][0] = 255
        img[i][l][1] = 255
        img[i][l][2] = 255

io.imshow(img)
img = io.imread('flowers.jpg')
io.imshow(img)
````

Even though this picture is a rectangle, we can put a circular mask around it using the [Pythagorean theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem).

````powershell
nrows, ncols, nsize = img.shape
row, col = np.ogrid[:nrows, :ncols]
cnt_row, cnt_col = nrows / 2, ncols / 2
outer_disk_mask = ((row - cnt_row)**2 + (col - cnt_col)**2 > (nrows / 2)**2)
img[outer_disk_mask] = 0

io.imshow(img)
````

Let's examine [colorspaces](https://scikit-image.org/docs/stable/api/skimage.color.html). We will be making use of the ```convert_colorpace``` method. If you review the documentation on this method, you will find a list of colorspaces that can be used.

```powershell
from skimage import color

img = io.imread('flowers.jpg')
io.imshow(img)
hsv = color.convert_colorspace(img, 'RGB','HSV')
hsv.shape
hsv[0][0]
io.imshow(hsv)
```
