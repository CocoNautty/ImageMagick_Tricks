# ImageMagick_Tricks_Collection
Some ImageMagick tricks that I collect.

## Picture Stencil Maker

From https://blog.jiayu.co/2019/05/edge-detection-with-imagemagick/.

<img src="./src/tomjerry.jpg" alt="original" width="400"/>

### Preprocessing

We first grayscale this picture and remove the alpha's.

```bash
convert tomjerry.jpg -colorspace gray -alpha remove tomjerry-preprocessed.jpg
```

<img src="./src/tomjerry-preprocessed.jpg" alt="preprocessed" width="400" />

### Convolution

#### Roberts Cross algorithm

```bash
convert tomjerry-preprocessed.jpg \
	-define morphology:compose=Lighten \
	-morphology Convolve 'Roberts:@' \
	-negate \
	-gaussian-blur 1x1 \
	-auto-threshold OTSU \
	tomjerry_roberts_maximum_threshold.jpg
```

<img src="./src/tomjerry_roberts_maximum_threshold.jpg" alt="roberts" width="400" />

