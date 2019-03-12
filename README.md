# computador pessoal TK2000-color: CARTÃO DE REFERÊNCIA

![Capa](/capa.jpg "computador pessoal TK2000-color: CARTÃO DE REFERÊNCIA")

This repository contains all files used in the digitization of the `computador pessoal TK2000-color: CARTÃO DE REFERÊNCIA` reference card, which was part of the contents included by the former brazilian militar dictatorship-era "MICRODIGITAL" company in their TK2000 home computer.

All reference card pages were scanned with XSane and a multi-function home device (`Canon MX725`) on a Linux System running Fedora 29. TIFF Raw images with the photographic reproduction of the referecence card pages were processed with `Scan Tailer` and converted to JPEG2000 using the following `Image Magick` command: 

> $ for i in 'scan tailor output/*.tif' ; do convert -define jp2:rate=20 "$i" "scan tailor output.j2k/i\`basename -s .tif "$i"\`.j2k" ; done 

`Image Magick` was used to create one .PDF file from the JPEG2000 images as well:

> $ convert -adjoin "scan tailor output.j2k/*.j2k" cartão_referência_TK2000-color_original_pages.pdf 

`cartão_referência_TK2000-color_original_pages.pdf` was created with the documentation of the original publication in mind. A second, searchable PDF file was generated in order to let enthusiasts access the contents of the document easilier. For this purpose, a second `scan tailor` project to output black and white versions of the scanned pages was created. The B&W pages were then used as input in `tesseract`, an utility for OCR capable of creating searchable PDF files from scanned pages of text:

> $ for i in "scan tailor contents only output/*.tif" ; do tesseract "$i" "tesseract.out/\`basename -s .tif "$i"\`" -l por pdf ; done

The searchable PDF files with single pages of the reference card were joined in one single, searchable PDF file:

> $ pdfjoin --outfile cartão_referência_TK2000-color.pdf tesseract.out/*.pdf

That's all Folks! 
