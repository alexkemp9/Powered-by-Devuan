# *Powered-by-Devuan*
A Series of Logos + the IM6 Scripts to Create Them

This is a series of *“Powered by Devuan”* logos for use in websites, or whatever you wish. There's not a lot, but an ImageMagick (IM6) script is provided for each option, and that means that you can spend the next 3 months customising the heck out of them if you want. Both Scripts & logos are within the [Logo](Logo/) directory. The tar.gz is a collection of all scripts + logos.

See also https://dev1galaxy.org/viewtopic.php?id=5885.

## *The Logos*

Here is a set of six ( {LHS | Centre | RHS} top + bottom ) each in *“NimbusSans-Regular”* font:–     

| Left-Hand-Side                   | Centre                               | Right-Hand-Side                  |
|:---------------------------------|:------------------------------------:|---------------------------------:|
![lhs logo](Logo/devuan-powered-by-lhs.png) | ![centre logo](Logo/devuan-powered-by-centred.png) | ![rhs logo](Logo/devuan-powered-by-rhs.png)
![lhs-bottom logo](Logo/devuan-powered-by-lhs-bottom.png) | ![centre-bottom logo](Logo/devuan-powered-by-centred-bottom.png) | ![rhs-bottom logo](Logo/devuan-powered-by-rhs-bottom.png)

…and then, just because we can, here is the same set of 6 but with a *narrow* version of the same font:–     

| Left-Hand-Side                   | Centre                               | Right-Hand-Side                  |
|:---------------------------------|:------------------------------------:|---------------------------------:|
![lhs logo](Logo/devuan-powered-by-lhs-narrow.png) | ![centre logo](Logo/devuan-powered-by-centred-narrow.png) | ![rhs logo](Logo/devuan-powered-by-rhs-narrow.png)
![lhs-bottom logo](Logo/devuan-powered-by-lhs-bottom-narrow.png) | ![centre-bottom logo](Logo/devuan-powered-by-centred-bottom-narrow.png) | ![rhs-bottom logo](Logo/devuan-powered-by-rhs-bottom-narrow.png)

## *The Scripts*

This is the combo of IM6 Script + the PNG that that script will produce (in the same order as above):

| Left-Hand-Side                   | Centre                               | Right-Hand-Side                  |
|:---------------------------------|:------------------------------------:|---------------------------------:|
| **Top:**                                                                                                   |
| convert-lhs ＝＞ devuan-powered-by-lhs.png  | convert-centred ＝＞ devuan-powered-by-centred.png    | convert-rhs ＝＞ devuan-powered-by-rhs.png   |
| **Bottom:**                                                                                                |
| convert-lhs-bottom ＝＞ devuan-powered-by-lhs-bottom.png  | convert-centred-bottom ＝＞ devuan-powered-by-centred-bottom.png         | convert-rhs-bottom ＝＞ devuan-powered-by-rhs-bottom.png   |
| **Top Narrow:**                                                                                            |
| convert-lhs-narrow ＝＞ devuan-powered-by-lhs-narrow.png  | convert-centred-narrow ＝＞ devuan-powered-by-centred-narrow.png     | convert-rhs-narrow ＝＞ devuan-powered-by-rhs-narrow.png   |
| **Bottom Narrow:**                                                                                            |
| convert-lhs-bottom-narrow ＝＞devuan-powered-by-lhs-bottom-narrow.png | convert-centred-bottom-narrow ＝＞ devuan-powered-by-centred-bottom-narrow.png  | convert-rhs-bottom-narrow ＝＞ devuan-powered-by-rhs-bottom-narrow.png  |

## *Editing the Scripts*
A little bit of help to get you going should you wish to edit one or more of the IM6 scripts.

[ImageMagick CLI](https://imagemagick.org/script/command-line-options.php)     
[ImageMagick Usage](https://legacy.imagemagick.org/Usage/)     
[ImageMagick Fonts](https://imagemagick.org/script/command-line-options.php#font)

These scripts were written for IM6 (current version is IM7; there are some differences):
```
$ convert --version
Version: ImageMagick 6.9.11-60 Q16 x86_64 2021-01-25 https://imagemagick.org
Copyright: (C) 1999-2021 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC Modules OpenMP(4.5) 
Delegates (built-in): bzlib djvu fftw fontconfig freetype heic jbig jng jp2 jpeg lcms lqr ltdl lzma openexr pangocairo png tiff webp wmf x xml zlib
```
The very first thing that you may wish to do is to grab the current Devuan logo (one is already within [Logo](Logo/), but this is me being super careful):
```
$ wget https://git.devuan.org/devuan/documentation/raw/branch/master/art/graphics/logo/devuan-logo.png
--2023-08-19 14:30:48--  https://git.devuan.org/devuan/documentation/raw/branch/master/art/graphics/logo/devuan-logo.png
Resolving git.devuan.org (git.devuan.org)... 116.202.138.212, 2a01:4f8:a0:3284::74ca:8ad4
Connecting to git.devuan.org (git.devuan.org)|116.202.138.212|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3316 (3.2K) [image/png]
Saving to: ‘devuan-logo.png’

devuan-logo.png   100%[===================>]   3.24K  --.-KB/s    in 0s      

2023-08-19 14:30:48 (47.2 MB/s) - ‘devuan-logo.png’ saved [3316/3316]
$ file devuan-logo.png
devuan-logo.png: PNG image data, 230 x 48, 8-bit gray+alpha, non-interlaced
```
Please note that the logo-background is *transparent* (set as alpha-transparency). Note also that all scripts are set to render their PNG file in the exact same mode.

The item that most folks may wish to change is the font for the text *“Powered by”*. Fonts are perhaps one of the most iffy aspects of IM6, so let's try to explain what to explore & what you may need to do.

The following code will show fonts currently registered in IM6 on your system & also IM6-specific local setup:
```
$ convert -list font | head

Path: /etc/ImageMagick-6/type-urw-base35.xml
  Font: AvantGarde-Book
    family: AvantGarde
    style: Normal
    stretch: Normal
    weight: 400
    glyphs: /usr/share/fonts/type1/urw-base35/URWGothic-Book.t1
$ convert -list font | fgrep Font: | wc -l
2919
$ fgrep -c '<type name=' /etc/ImageMagick-6/type-urw-base35.xml
34
```
So, I have a terrifying 2,919 fonts available to IM6 in my Desktop machine, whilst IM6 has just 34 fonts registered within it's local XML file. The non-narrow font used within the scripts is *NimbusSans-Regular* & that appears to come from amongst those 2,919 fonts (as does the narrow version):
```
$ convert -list font | fgrep 'Font: NimbusSans-Regular' -A 5
  Font: NimbusSans-Regular
    family: Nimbus Sans
    style: Normal
    stretch: Normal
    weight: 400
    glyphs: /usr/share/fonts/opentype/urw-base35/NimbusSans-Regular.otf
```
If you do not have any fonts already registered in IM then look at [Mark Setchell's answer](https://stackoverflow.com/questions/24696433/why-font-list-is-empty-for-imagemagick#24701602) but otherwise maybe just precede the fontname with an “@” (see the CLI font help).
