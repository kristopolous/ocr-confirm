# ocr-confirm

Designed for id-confirmation, this python script tries to use a number of different ocr engines to see if a users' claimed information
is present in a photograph of their ID.

Essentially you pass in an image and some claimed information and the result is a confidence interval of whether the content is likely in
the image.

## usage

The script is really a thin wrapper around executing a number of other shell programs.  Currently the following engines are used:

  * tesseract
  * gocr
  * ocrad
  * ocrfeeder

(Although to be honest, if tesseract can't find it, you're probably out of luck.)

Anyway, so here it goes

    $ ocr-confirm test-image.jpg "assertion 1" "assertion 2" "assertion 3"
      0.889,assertion 1,< what it found >
      0.309,assertion 2,< what it found >
      0.994,assertion 3,< what it found >

So internally, the entire text output of each image is looked at and is scanned for something similar to the claimed information, reporting
the Damerau–Levenshtein distance of what *is* found.
