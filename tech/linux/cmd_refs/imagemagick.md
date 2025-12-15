# ImageMagick convert

## See also
- [ffmpeg](./ffmpeg.md)
- [v4l](./v4l.md)

###### Install ImageMagick (includes `convert`)
```bash
sudo apt install imagemagick
```

###### Create an animated gif from a directory of numbered JPEG images
```bash
convert -delay 20 -loop 0 *.jpg myimage.gif
```

##### Create a PDF from a directory of numbered JPEG images
```bash
convert *.jpg -auto-orient -units pixelsperinch -density 72 -page letter -gravity center pictures.pdf
```

##### Create PDF by embedding SVG file

```bash
inkscape --export-filename=output.pdf input.svg
pdfjam --papersize '{8.5in,11in}' output.pdf --outfile output-letter.pdf
```

##### Convert pages of a PDF to PNG images
```bash
convert -density 150 input.pdf[0] output.png
```

Or this to do a batch, but it may run out of memory:
```bash
mogrify -density 150 -format png input.pdf
```

So I wrote a script:

```bash
#!/bin/bash

FILENAME1=original.pdf
FILENAME2=original_no_bg.pdf
PAGES=8
DPI=300
BG_COLOR="#cba787"

#remove background
if [ ! -f "$FILENAME2" ]; then
    echo "Removing background..."
    convert $FILENAME1 -fuzz 20% -channel rgba -fill none -opaque "$BG_COLOR" $FILENAME2
fi

#convert to png
for (( i=0; i<$PAGES; i++ ))
do
    page_filename="page_${i}.png"
    if [ ! -f "$page_filename" ]; then 
        echo "Converting page $i..."
        convert -density $DPI "${FILENAME2}[$i]" $page_filename
        sleep 1
    else
        echo "page ${page_filename} already exists"
    fi
done

```


This command will generate output_prefix-0.png, output_prefix-1.png, etc., for each page of input.pdf at 300 DPI. Adjust the -density value for different resolutions.

##### Remove solid color background from PDF

```bash
convert input.pdf -fuzz 10% -channel rgba -fill none -opaque "#RRGGBB" output.pdf
```

Replace `#RRGGBB` with hex code of background color you want to remove e.g. `#cba787` and adjust `-fuzz` for color tolerance.

```bash
convert input.pdf -fuzz 10% -channel rgba -fill none -opaque "#cba787" output.pdf
```

###### Fix for error convert-im6.q16: attempt to perform an operation not allowed by the security policy `PDF' @ error/constitute.c/IsCoderAuthorized/426.

```bash
sudo vim /etc/ImageMagick-6/policy.xml
```

Change this line:

```xml
<policy domain="coder" rights="none" pattern="PDF" />
```

To this:

```xml
<policy domain="coder" rights="read | write" pattern="PDF" />
```


## imagemagick man page
```
ImageMagick-im6.q16(1)                                                                      General Commands Manual                                                                      ImageMagick-im6.q16(1)

NAME
       ImageMagick - is a free software suite for the creation, modification and display of bitmap images.

SYNOPSIS
       convert-im6.q16 input-file [options] output-file

OVERVIEW
       Use  ImageMagick®  to create, edit, compose, or convert bitmap images. It can read and write images in a variety of formats (over 200) including PNG, JPEG, GIF, HEIC, TIFF, DPX, EXR, WebP, Postscript,
       PDF, and SVG. Use ImageMagick to resize, flip, mirror, rotate, distort, shear and transform images, adjust image colors, apply various special effects, or draw  text,  lines,  polygons,  ellipses  and
       B\['e]zier curves.

       The  functionality of ImageMagick is typically utilized from the command-line or you can use the features from programs written in your favorite language. Choose from these interfaces: G2F (Ada), Mag‐
       ickCore (C), MagickWand (C), ChMagick (Ch), ImageMagickObject (COM+), Magick++ (C++), JMagick (Java), JuliaIO (Julia), L-Magick (Lisp), Lua (LuaJIT), NMagick (Neko/haXe), Magick.NET (.NET), PascalMag‐
       ick (Pascal), PerlMagick (Perl), MagickWand for PHP (PHP), IMagick (PHP), PythonMagick (Python), magick (R), RMagick (Ruby), or TclMagick (Tcl/TK). With a language interface, use ImageMagick to modify
       or create images dynamically and automagically.

       ImageMagick utilizes multiple computational threads to increase performance and can read, process, or write mega-, giga-, or tera-pixel image sizes.

       ImageMagick is free software delivered as a ready-to-run binary distribution or as source code that you may use, copy, modify, and distribute in both open and proprietary applications. It is  distrib‐
       uted under a derived Apache 2.0 license.

       The  ImageMagick  development  process ensures a stable API and ABI. Before each ImageMagick release, we perform a comprehensive security assessment that includes memory error, thread data race detec‐
       tion, and continuous fuzzing to help prevent security vulnerabilities.

       The current release is ImageMagick 6.9.10-11. It runs on Linux, Windows, Mac Os X, iOS, Android OS, and others.

       The authoritative ImageMagick version 6 web site is https://legacy.imagemagick.org. The authoritative source code repository is https://github.com/ImageMagick/ImageMagick6. We maintain a  source  code
       mirror at https://gitlab.com/ImageMagick/ImageMagick6.

       The  design of ImageMagick is an evolutionary process, with the design and implementation efforts serving to influence and guide further progress in the other. With ImageMagick version 7 we aim to im‐
       prove the design based on lessons learned from the version 6 implementation.

       In the paragraphs below, find a short description for each command-line tool.Cl ick on the program name to get details on the program usage and a list of comman d-line options that alters how the pro‐
       gram performs. If you are just getting acq uainted with ImageMagick, start at the top of the list, the convert program, and
        work your way down. Also be sure to peruse Anthony Thyssen's tutorial on how to
        use ImageMagick utilities to convert, compose, or edit images from the command- line.

       convert

              convert between image formats as well as resize an image, blur, crop, despeckle, dither, draw on, flip, join, re-sample, and much more.

       identify

              describes the format and characteristics of one or more image files.

       mogrify

              resize an image, blur, crop, despeckle, dither, draw on, flip, join, re-sample, and much more. Mogrify overwrites the original image file, whereas, convert writes to a different image file.

       composite

              overlaps one image over another.

       montage

              create a composite image by combining several separate images. The images are tiled on the composite image optionally adorned with a border, frame, image name, and more.

       compare

              mathematically and visually annotate the difference between an image and its reconstruction..

       stream

              is a lightweight tool to stream one or more pixel components of the image or portion of the image to your choice of storage formats. It writes the pixel components as they are read from the in‐
              put image a row at a time making stream desirable when working with large images or when you require raw pixel components.

       display

              displays an image or image sequence on any X server.

       animate

              animates an image sequence on any X server.

       import

              saves any visible window on an X server and outputs it as an image file. You can capture a single window, the entire screen, or any rectangular portion of the screen.

       conjure

              interprets and executes scripts written in the Magick Scripting Language (MSL).

       For more information about the ImageMagick, point your browser  to  file:///usr/share/doc/imagemagick-6-common/html/index.html  (on  debian  system  you  may  install  the  imagemagick-6  package)  or
       http://imagemagick.org/.

SEE ALSO
       convert-im6.q16(1),  identify-im6.q16(1),  composite-im6.q16(1),  montage-im6.q16(1),  compare-im6.q16(1),  display-im6.q16(1),  animate-im6.q16(1), import-im6.q16(1), conjure-im6.q16(1), quantize(5),
       miff(4)

COPYRIGHT
       Copyright (C) 1999-2020 ImageMagick Studio LLC. Additional copyrights and licenses apply to this software, see file:///usr/share/doc/imagemagick-6-common/html/www/license.html (on  debian  system  you
       may install the imagemagick-6 package) or http://imagemagick.org/script/license.php

ImageMagick                                                                                Date: 2009/01/10 01:00:00                                                                     ImageMagick-im6.q16(1)

```