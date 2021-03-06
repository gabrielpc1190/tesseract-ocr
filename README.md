# tesseract-ocr
How to use tesseract-ocr on a container to convert jpg to searchable pdf

## Run a container tesseract-ocr, like this one from clearlinux:
clearlinux/tesseract-ocr:latest

## Download the TESSDATA files from this repo:
https://github.com/tesseract-ocr

Make sure you download your interested language files, in my case I downloaded
https://github.com/tesseract-ocr/tessdata_best/raw/master/eng.traineddata

https://github.com/tesseract-ocr/tessdata_best/raw/master/spa.traineddata

Also download the pdf.tff to be able to convert to pdf
https://github.com/tesseract-ocr/tessconfigs/raw/master/pdf.ttf

to your host and store them on the path you're going to use for tesseract-ocr:
For example: ``mkdir /home/tesseract-ocr/data/tessdata``

# Create a config file containing the instructions to export:
``nano /home/tesseract-ocr/data/tessdata/config.conf``

Add this lines to it:

``tessedit_create_pdf     1       Write .pdf output file``

Other examples are:

``tessedit_write_unlv 1    .unlv output file``

``tessedit_create_txt 1    .txt output file (default)``

``tessedit_create_hocr  1  .html hOCR output file``

``tessedit_create_tsv 1    .tsv output file``

``tessedit_create_pdf 1    .pdf output file``

``textonly_pdf 1 creates PDF with only one invisible text layer``
Really usefull for storing only the text, if you don't need the shape and other forms of the document. Small file


# Assign a volume to your container 
``/home/tesseract-ocr/data/:/data``

``/data`` is where you're going to locate your img.jpg file to be converted to exported.pdf on the same folder.

# Then modify your container CMD and set it like this:
``'tesseract' '--tessdata-dir' '/data/tessdata' '/data/img.jpg' '/data/exported' '-l' 'spa' '--oem' '1' '/data/tessdata/config.conf'``
# Now put a jpg file on your run your data folder and run your container
You will get a searchable pdf called exported.pdf
# That's it!
