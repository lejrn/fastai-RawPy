# Connecting fast.ai with RawPy
Here we can make fast.ai framework support RawPy library, hence use RAW image files on fastai.

The list of all the RAW image files that can be supported by rawpy (based on LibRaw):

https://www.libraw.org/supported-cameras

Partial list of the supported RAW formats:
- *.IIQ (Phase One) 
- *.3FR (Hasselblad)
- *.DCR, *.K25, *.KDC (Kodak) 
- *.CRW *.CR2 *.CR3 (Canon) 
- *.ERF (Epson) 
- *.MEF (Mamiya) 
- *.MOS (Leaf) 
- *.NEF *.NRW (Nikon) 
- *.ORF (Olympus) 
- *.PEF (Pentax)
- *.RW2 (Panasonic)
- *.ARW, *.SRF, *.SR2 (Sony)

# How to install
Use:

```pip install fastai-rawpy```

to install this package.

# How to import fastai-rawpy

Use:

```from fastairawpy import *```

in order to import `RawImageBlock` as well as all of the necessary functions/classes/etc that adjust fast.ai so it supports RawPy.

# How to use fastai-rawpy

Upon using fast.ai, wherever you could have used `ImageBlock`, just type in `RawImageBlock`.

## examples

### Example (1)

This line creates two blocks (input and target) of an `ImageBlock`, that is a transform to be applied to create items of image type. The transform uses `PILImage` as a data-holder of the image files (such as JPG, PNG, BMP, ...).

```
dblock = DataBlock(blocks=(ImageBlock(cls=PILImage),Categorize))
```

But this line uses `RawImageBlock` transform, that is applied automatically on built-in `RAWImage` items. `RAWImage` as its data-holder of RAW image files, alike `PILImage`, but is based on `rawpy` package.

```
dblock = DataBlock(blocks=(RawImageBlock,Categorize))
```

### Example (2)

This line code snippet creates two `RawImageBlock` blocks of input and target, where the parameters being passed in define the postprocessing of each blocks' image:

```
dblock = DataBlock(blocks=(RawImageBlock(  # Input
                                         gamma=(2.222, 4.5),                 # Gamma values
                                         output_color=rawpy.ColorSpace.sRGB, # sRGB Color Space
                                         bright=0.50,                        # Brightness level
                                         output_bps=16),                     # Bits_per_pixel 
                           RawImageBlock( # Target
                                         use_camera_wb=True,                 # White blanace
                                         output_color=rawpy.ColorSpace.sRGB, # sRGB Color Space
                                         output_bps=16)                      # Bits_per_pixel 
                           )
                    )
```

The full list of parameters: https://letmaik.github.io/rawpy/api/rawpy.Params.html

# Why use fastai-rawpy

RAW format has a bit-depth of 16bits for every channel (R,G,B[,G]), meaning: every pixel gets values in between 0 up to... 65536!
> 2^16=65536

Therefore, a RAW image file would normally have a larger range of values for every pixel. This can help training a model become more precise, when switching from JPG to RAW.
> Note: in practice, every DSLR stores RAW files and postprocesses these files into other formats such as JPG. For instance, it crops and compresses the JPG image out of the RAW file.

# New objects that connect fast.ai and rawpy

### `class TensorRawImage` + `class RAWImage`

<p align="center">
  <img src="./SVGs/tensorRawImage.svg">
</p>
