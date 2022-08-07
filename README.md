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

While using fast.ai, wherever you could have used `ImageBlock`, just type in `RawImageBlock`.

# `class TensorRawImage` + `class RAWImage`

RAW format has a bit-depth of 16bits for every channel (R,G,B[,G]), meaning: every pixel gets values in between 0 up to... 65536!
> 2^16=65536

Therefore, a RAW image file would normally have a larger range of values for every pixel. This can help training a model become more precise, when switching from JPG to RAW.
> Note: in practice, every DSLR stores RAW files and postprocesses these files into other formats such as JPG. For instance, it crops and compresses the JPG image out of the RAW file.

#### new classes
<p align="center">
  <img src="./SVGs/TensorRawImage__.svg">
</p>
