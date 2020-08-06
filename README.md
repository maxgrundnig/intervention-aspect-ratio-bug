# intervention-image-resize-aspect-ratio-bug

# Requirements
 - PHP 7.4.8
 - php-imagick 3.4.4
 
## Description
There are edge cases where `Image::resize()` with the aspect ratio constraint generates for the same image and nearly
identical width/height parameters different results although one would expect identical images.

For example, if you downsize (with aspect ratio constraint) a landscape image (width > height) and you pass $width/$height
parameters to `Image::resize()` where $width < $height is true, you would expect that you always get the same output image
regardless of the value of $height, because in that case the $width is the limiting dimension.

This script generates three output images for the same input image with different $width and $height input parameters.
It is expected that all three images are exactly the same size. As outlined below `assets/output3.jpg` will have an unexpected
height.

|Filename|Input parameters<br>$w x $h|Expected output dimension|Actual output Dimension|
|---|---|---|---|
|output1.jpg|100xNULL|100x67 px|100x67 px|
|output2.jpg|100x130|100x67 px|100x67 px|
|**output3.jpg**|**100x131**|**100x67 px**|**100x66 px**|

## Usage
`$ ./run`
