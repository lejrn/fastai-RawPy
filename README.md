# Connecting fast.ai with RawPy
Making fast.ai framework support RawPy library (like with PIL)

# `class TensorRawImage` + `class RAWImage`
#### First off, what is the difference between JPG and RAW formats?
JPG format has a bit-depth of 8bits for every channel (R,G,B), meaning: every pixel gets values in between 0 up to 255.
> 2^8=255
  
RAW format has a bit-depth of 16bits for every channel (R,G,B[,G]), meaning: every pixel gets values in between 0 up to... 65536!
> 2^16=65536

Therefore, a RAW image file would normally have a larger range of values for every pixel. This can help training a model become more precise, when switching from JPG to RAW.
> Note: in practice, every DSLR stores RAW files and postprocesses these files into other formats such as JPG. For instance, it crops and compresses the JPG image out of the RAW file.

#### Problem: PIL doesn't support RAW files
  
In order to improve the training process, I figured out that using RAW files would yield in more details. Problem was that fastai has been based on `PIL` for handling image files, which doesn't support RAW files. Therefore, I needed to create new classes that inherit feautres from `RawPy` library, that does support RAW image files.
  
#### new classes
<p align="center">
  <img src="./SVGs/TensorRawImage__.svg">
</p>
