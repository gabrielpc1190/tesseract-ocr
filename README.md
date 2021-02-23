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

``tessedit_create txt     1       Write .txt output file``

# Assign a volume to your container 
``/home/tesseract-ocr/data/:/data``

``/data`` is where you're going to locate your img.jpg file to be converted to exported.pdf on the same folder.

# Then modify your container CMD and set it like this:
``'tesseract' '--tessdata-dir' '/data/tessdata' '/data/img.jpg' '/data/exported' '-l' 'spa' '--oem' '1' '/data/tessdata/config.conf'``
