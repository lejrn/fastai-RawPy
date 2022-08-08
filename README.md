# Connecting fast.ai with RawPy
Here we can make fast.ai framework support RawPy library, hence use RAW image files on fastai

# How to install
Use:

```pip install fastai-rawpy```

to install this package that lets you use fast.ai and RAW image files as well.

# How to import fastai-rawpy

Use:

```from fastairawpy import *```

in order to import `RawImageBlock` as well as all of the necessary functions/classes/etc that adjust fast.ai so it supports RawPy.

# How to use fastai-rawpy

Upon using fast.ai, wherever you could have used `ImageBlock`, just type in `RawImageBlock`.

## examples

### 1

This line uses `PILImage` as a data-holder of PIL supporting image files (such as JPG, PNG, BMP, ...), which will be peaked by the `ImageBlock` classifier.

```
dblock = DataBlock(blocks=(ImageBlock(cls=PILImage),ImageBlock(cls=PILImage)))
```

But this line uses `RawImageBlock` classifier, which would automatically use `RAWImage` as its data-holder of RAW image files.

```
dblock = DataBlock(blocks=(RawImageBlock(),RawImageBlock()))
```

### 2

This code:

```
dblock = DataBlock(blocks=(RawImageBlock(gamma=(2.222, 4.5), # Input  
                                         output_color=rawpy.ColorSpace.sRGB, 
                                         bright=0.50, 
                                         output_bps=16),
                           RawImageBlock(use_camera_wb=True, # Target
                                         output_color=rawpy.ColorSpace.sRGB,
                                         output_bps=16)
                           )
                    )
```

is changed into this code:

```
dblock = DataBlock(blocks=(RawImageBlock(gamma=(2.222, 4.5), # Input  
                                         output_color=rawpy.ColorSpace.sRGB, 
                                         bright=0.50, 
                                         output_bps=16),
                           RawImageBlock(use_camera_wb=True, # Target
                                         output_color=rawpy.ColorSpace.sRGB,
                                         output_bps=16)
                           )
                    )
```

# Why use fastai-rawpy

RAW format has a bit-depth of 16bits for every channel (R,G,B[,G]), meaning: every pixel gets values in between 0 up to... 65536!
> 2^16=65536

Therefore, a RAW image file would normally have a larger range of values for every pixel. This can help training a model become more precise, when switching from JPG to RAW.
> Note: in practice, every DSLR stores RAW files and postprocesses these files into other formats such as JPG. For instance, it crops and compresses the JPG image out of the RAW file.

### `class TensorRawImage` + `class RAWImage`

#### new classes
<p align="center">
  <img src="./SVGs/TensorRawImage__.svg">
</p>
