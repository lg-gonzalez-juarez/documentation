---
title: 15. Hands-on Lab Editing Images with scikit-image
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_15.html
folder: handson
---

## Introduction

In this lab, we work with image data using scikit-image. We will go through the process of reading in an existing image and make modifications to it programmatically.

## Solution

To get started, we need to log in to the VS Code server using the browser. To do so, use the provided public IP and the 9090 port. For example: <PUBLIC_IP>:9090

## Install scikit-image

Before we can edit images we'll need to install scikit-image:

1. Check the python version and make sure it is above 3.8:
```
 python -V
```

2. Install scikit_image:
```
 python -m pip install scikit-image
```

## Load the highrise.jpg Image into Memory

Now that we have `scikit-image` installed, we're ready to start using it in our `image_editing.py` script. To test the image changes that we'd like to automate, we're going to work with a local image called highrise.jpg. This can be found at `/home/cloud_user/highrise.jpg`:

1. Using the Open File or Folder command provided by the VS Code server, open our `image_editing.py` file.

2. Under the # 1) `Load highrise.jpg` into memory section, enter the following code:

```
 from skimage import io

 highrise = io.imread("/home/cloud_user/highrise.jpg")
 ```

3. Select the Run Cell selection above the first section.

4. After the first section runs, click on Run Cell for the section we just updated.

## Create a Black and White Version of highrise.jpg

The first modification we'd like to automate is the conversion of an image from being a colored/RGB image to being a black and white or grayscale image. This is a common task, and we can leverage code from within the skimage.colors module to do nearly all of the work.

1. Under the # 2) Create a black and white version of `highrise.jpg` section, enter the following:

```
 from skimage.color import rgb2gray

 grayscale = rgb2gray(highrise)

 fig, ax = plt.subplots(1, 2, figsize=(6, 4))
 ax[0].imshow(highrise, cmap=plt.cm.gray)
 ax[0].axis("off")
 ax[1].imshow(grayscale, cmap=plt.cm.gray)
 ax[1].axis("off")

 fig.tight_layout()
 plt.show()
```

2. Select Run Cell for this section, and we will see a comparison of our old color image and our new black and white one.

## Create a Copy of highrise.jpg with a Circular Mask

Adding a mask to our image is a much more complicated task that requires us to index and slice the array that is backing our image's data:

1. Under the `# 3) Create a version of highrise.job` with a circular mask, enter the following:

```
 import numpy as np

 masked = highrise.copy()

 nrows, ncols, nsize = masked.shape
 row, col = np.ogrid[:nrows, :ncols]
 cnt_row, cnt_col = nrows / 2, ncols / 2
 outer_disk_mask = (row - cnt_row) ** 2 + (col - cnt_col) ** 2 > (nrows / 2) ** 2
 print(outer_disk_mask)
 masked[outer_disk_mask] = 0
```

2. Click on Run Cell to check the mask. It will show True for all fields when it is correct.

3. Remove the `print (outer_disk_mask)` section, as we no longer need it.

4. Enter the following under what we have already created:

```
 fig2, ax2 = plt.subplots(1, 2, figsize=(6, 4))
 ax2[0].imshow(highrise, cmap=plt.cm.gray)
 ax2[0].axis("off")
 ax2[1].imshow(masked, cmap=plt.cm.gray)
 ax2[1].axis("off")

 fig2.tight_layout()
 plt.show()
```
5. Click on Run Cell and note that the image now has blacked out corners.
