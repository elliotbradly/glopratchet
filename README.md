![GitHub go.mod Node.js version](https://img.shields.io/node/v-lts/carbon)

# glopratchet

Glopratchet is an automated digital art program designed to recreate the captivating – and delightfully unpredictable – visual experience of watching a janky, real-time application apply paint within a JavaScript-powered Electron browser. Each run births a unique image, a fleeting moment captured in code.

The program’s heart lies within a single JSON file, a compendium of parameters that dictate its artistic values: canvas size, brush type, the delicate spacing of each mark, color range, saturation, and a host of other specifications. This repository contains the essential elements needed to bring Glopratchet to life, but it’s also an invitation – a canvas awaiting the artist’s touch, ready to be extended with custom brushes and boundless creativity."

1. [Quick Start](#quick-start)
1. [Design](#design)
1. [Painting](#painting)
1. [Configuration](#configuration)
1. [Upgrading](#upgrading)
1. [Configuration Reference](#configuration-reference)

## Quick Start

Unzipped the file labeled `glp` into the root directory.
Click the batch file labeled `glopratchet.bat`.
(Alternatively) open your command line terminal and run
`cd glp`
`node go`

An Electron browser window should open, followed by the creation of a cow image from scratch

Requires at least 8GB of RAM.

## Example Artwork

<div align="center">

![Royal Tenenbaum](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/00.png)

</div>

<div align="center"> Royal Tenenbaum </div>

<div align="center">

![Abstraction](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/01.png)

</div>

<div align="center"> Abstraction </div>

<div align="center">

![Child with Gigi](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/02.png)

</div>

<div align="center"> Child with Gigi </div>

<div align="center">

![Alligator Earth](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/03.png)

</div>

<div align="center"> Alligator Earth </div>

<div align="center">

![Our Earth](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/04.png)

</div>

<div align="center"> Our Earth </div>

## Design

This program works by sampling from the source image random x and y values between a distance in pixels. The points are then used and replaced with a png file from the mrk directory and overlayed on top of the final work untill all the sample points have been process with small variation in color to the final pixel values used. A palette file restricts the colors used with a small sample.

## Example Marks

![Mark One](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/000.png)

![Mark Two](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/001.png)

![Mark Three](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/003.png)

![Mark Four](https://raw.githubusercontent.com/elliotbradly/glop00/main/examples/004.png)

### File System Structure

The operation of the program is reliant upon the structure of the file system. The list of directories which may require manipulation are as follows

```
/art - location of finalized work
/frm - container to hold the reference image
/mrk - directories of brushes
/pal - text files representing color pallettes
```

#### /art

Use this folder to access the final images as they are processed.

#### /frm

Use this folder to place the reference images you want to manipulated.

#### /mrk

Use this folder to see the difference types of marks which can be used to process your image

#### /pal

This directory contains the text file which result in limiting the colors to a specfic range

## Painting Tips

to do

## Configuration

All configuration is done through a single config file in the json format. The configuration file is found in the root directory of the program.

```
./00-fate.json
```

This file can be manipulated manually or through scripting.

### Sample `00-fate.json`

A full example of the Glopratchet configuration file is as below.

```json
{
  "time": 30,
  "pass": 0,
  "size": 0,
  "over": 1,
  "sizeList": [
    { "id": 0, "width": 1080, "height": 1080 },
    { "id": 1, "width": 1920, "height": 1920 }
  ],
  "fate": true,
  "reset": false,
  "done": 0,
  "brushes": 133,
  "label": "mass art \r",
  "color": ["#829ba0"],
  "layout": {
    "compIMG": 11,
    "compTXT": 0,
    "showIMG": true,
    "showTXT": false,
    "colrIMG": "0xFF00FF",
    "colrTXT": "0xFF00FF",
    "image": { "x": 108, "y": 0, "width": 108, "height": 972 },
    "text": { "x": 648, "y": 0, "width": 216, "height": 1080 },
    "x": 712,
    "y": -695,
    "scaleX": 0.2,
    "scaleY": 0.2
  },
  "style": [
    {
      "id": "000",
      "mark": 13,
      "sample": 1,
      "range": [0.012360040306176734, 0.99941],
      "scale": [1, 1, 1, 1],
      "value": [1, 1, 1, 1],
      "size": [1, 1, 1, 1],
      "amount": 31,
      "palette": "24-turrel",
      "blur": { "x": 0, "y": 0 },
      "hue": 99,
      "sat": 88,
      "lit": 99,
      "fde": 0
    }
  ]
}
```

Refer to the [configuration reference](#configuration-reference) for full details of each
configuration key.

## Upgrading

Upgrading to handle new marks is accomplished by creating a numbered folder in the root level mrk directory and placing a series of png images here

## Configuration Reference

Below is a reference of all keys available in the `00-fate.json`

### `time`

A value in second to run the program before automatically shutting down.

Example

```json
time:0
```

### `size`

The index of the dimension to be used from the sizeList array

Example

```json
size:0
```

### `sizeList`

An array of dimension that can be used by the program

Example

```json
"sizeList": [
    { "id": 0, "width": 1080, "height": 1080 },
    { "id": 1, "width": 1920, "height": 1920 }
  ]
```

### `brushes`

The number of brushes to be used to the run. Each brush will have randomness applied to it to make it slightly different than all the others

Example

```json
"brushes": 133
```

### `mark`

Example

The index of the brush collection used from the mrk folder.

```json
"mark": 13
```

### `range`

A floating point number which represents a percentage value between light and dark colors found within the reference image. 0 represents lights while 1 represents darks.

Example

```json
"range": [0.012360040306176734, 0.99941],
```

### `scale`

An array of values which represent the a size modifier to applied to the brush marks. These modifiers are randomly selected from the list. An amount of 2 represents twice the size while an amount of 10 would represent ten times the scale of the brush.

```json
  "scale": [2, .9, 1.6, 1.3],
```

### `palette`

The name of palette file from which to restrict colors used

Example

```json
 "palette": "24-turrel"
```

### `blur`

an object which determines the blurring of the brush mark based percentage of x and y values

Example

```json
"blur": { "x": 0, "y": 0 },
```

### `hue`

a value to adjust the pure pigment of the color

Example:

```json
 "hue": 99,
```

### `sat`

a value to adjust the saturation of the color

Example

```json
"sat": 88,
```

### `lit`

a value to adjust the light and darkness of the brush mark color. Higher values indicate lightness while darker colors indicate darker tones

Example

```json
"lit": 99,
```

### `fde`

a value to affect the transparency of the brush mark

0. no tranparency
1. 10 percent tranparency
2. 20 percent tranparency
3. 50 percent tranparency

Example

```json
 "fde": 0
```

## License

MIT License

Copyright (c) 2024 [Brad Henderson](http://fictiq.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
