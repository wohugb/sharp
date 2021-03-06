## rotate

Rotate the output image by either an explicit angle
or auto-orient based on the EXIF `Orientation` tag.

If an angle is provided, it is converted to a valid 90/180/270deg rotation.
For example, `-450` will produce a 270deg rotation.

If no angle is provided, it is determined from the EXIF data.
Mirroring is supported and may infer the use of a flip operation.

The use of `rotate` implies the removal of the EXIF `Orientation` tag, if any.

Method order is important when both rotating and extracting regions,
for example `rotate(x).extract(y)` will produce a different result to `extract(y).rotate(x)`.

**参数** 

-   `angle` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** angle of rotation, must be a multiple of 90. (optional, default `auto`)

**示例** 

```javascript
const pipeline = sharp()
  .rotate()
  .resize(null, 200)
  .toBuffer(function (err, outputBuffer, info) {
    // outputBuffer contains 200px high JPEG image data,
    // auto-rotated using EXIF Orientation tag
    // info.width and info.height contain the dimensions of the resized image
  });
readableStream.pipe(pipeline);
```

-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## extract

Extract a region of the image.

-   Use `extract` before `resize` for pre-resize extraction.
-   Use `extract` after `resize` for post-resize extraction.
-   Use `extract` before and after for both.

**参数** 

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.left` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** zero-indexed offset from left edge
    -   `options.top` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** zero-indexed offset from top edge
    -   `options.width` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** dimension of extracted image
    -   `options.height` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** dimension of extracted image

**示例** 

```javascript
sharp(input)
  .extract({ left: left, top: top, width: width, height: height })
  .toFile(output, function(err) {
    // Extract a region of the input image, saving in the same format.
  });
```

```javascript
sharp(input)
  .extract({ left: leftOffsetPre, top: topOffsetPre, width: widthPre, height: heightPre })
  .resize(width, height)
  .extract({ left: leftOffsetPost, top: topOffsetPost, width: widthPost, height: heightPost })
  .toFile(output, function(err) {
    // Extract a region, resize, then extract from the resized image
  });
```

-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## flip

Flip the image about the vertical Y axis. This always occurs after rotation, if any.
The use of `flip` implies the removal of the EXIF `Orientation` tag, if any.

**参数** 

-   `flip` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## flop

Flop the image about the horizontal X axis. This always occurs after rotation, if any.
The use of `flop` implies the removal of the EXIF `Orientation` tag, if any.

**参数** 

-   `flop` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## sharpen

Sharpen the image.
When used without parameters, performs a fast, mild sharpen of the output image.
When a `sigma` is provided, performs a slower, more accurate sharpen of the L channel in the LAB colour space.
Separate control over the level of sharpening in "flat" and "jagged" areas is available.

**参数** 

-   `sigma` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** the sigma of the Gaussian mask, where `sigma = 1 + radius / 2`.
-   `flat` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** the level of sharpening to apply to "flat" areas. (optional, default `1.0`)
-   `jagged` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** the level of sharpening to apply to "jagged" areas. (optional, default `2.0`)


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## blur

Blur the image.
When used without parameters, performs a fast, mild blur of the output image.
When a `sigma` is provided, performs a slower, more accurate Gaussian blur.

**参数** 

-   `sigma` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** a value between 0.3 and 1000 representing the sigma of the Gaussian mask, where `sigma = 1 + radius / 2`.


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## extend

Extends/pads the edges of the image with the colour provided to the `background` method.
This operation will always occur after resizing and extraction, if any.

**参数** 

-   `extend` **([Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) \| [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object))** single pixel count to add to all edges or an Object with per-edge counts
    -   `extend.top` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 
    -   `extend.left` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 
    -   `extend.bottom` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 
    -   `extend.right` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 

**示例** 

```javascript
// Resize to 140 pixels wide, then add 10 transparent pixels
// to the top, left and right edges and 20 to the bottom edge
sharp(input)
  .resize(140)
  .background({r: 0, g: 0, b: 0, alpha: 0})
  .extend({top: 10, bottom: 20, left: 10, right: 10})
  ...
```

-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## flatten

Merge alpha transparency channel, if any, with `background`.

**参数** 

-   `flatten` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## trim

Trim "boring" pixels from all edges that contain values within a percentage similarity of the top-left pixel.

**参数** 

-   `tolerance` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** value between 1 and 99 representing the percentage similarity. (optional, default `10`)


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## gamma

Apply a gamma correction by reducing the encoding (darken) pre-resize at a factor of `1/gamma`
then increasing the encoding (brighten) post-resize at a factor of `gamma`.
This can improve the perceived brightness of a resized image in non-linear colour spaces.
JPEG and WebP input images will not take advantage of the shrink-on-load performance optimisation
when applying a gamma correction.

**参数** 

-   `gamma` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** value between 1.0 and 3.0. (optional, default `2.2`)


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## negate

Produce the "negative" of the image.

**参数** 

-   `negate` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## normalise

Enhance output image contrast by stretching its luminance to cover the full dynamic range.

**参数** 

-   `normalise` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## normalize

Alternative spelling of normalise.

**参数** 

-   `normalize` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## convolve

Convolve the image with the specified kernel.

**参数** 

-   `kernel` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `kernel.width` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** width of the kernel in pixels.
    -   `kernel.height` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** width of the kernel in pixels.
    -   `kernel.kernel` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)>** Array of length `width*height` containing the kernel values.
    -   `kernel.scale` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** the scale of the kernel in pixels. (optional, default `sum`)
    -   `kernel.offset` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** the offset of the kernel in pixels. (optional, default `0`)

**示例** 

```javascript
sharp(input)
  .convolve({
    width: 3,
    height: 3,
    kernel: [-1, 0, 1, -2, 0, 2, -1, 0, 1]
  })
  .raw()
  .toBuffer(function(err, data, info) {
    // data contains the raw pixel data representing the convolution
    // of the input image with the horizontal Sobel operator
  });
```

-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## threshold

Any pixel value greather than or equal to the threshold value will be set to 255, otherwise it will be set to 0.

**参数** 

-   `threshold` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** a value in the range 0-255 representing the level at which the threshold will be applied. (optional, default `128`)
-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.greyscale` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** convert to single channel greyscale. (optional, default `true`)
    -   `options.grayscale` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** alternative spelling for greyscale. (optional, default `true`)


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## boolean

Perform a bitwise boolean operation with operand image.

This operation creates an output image where each pixel is the result of
the selected bitwise boolean `operation` between the corresponding pixels of the input images.

**参数** 

-   `operand` **([Buffer](https://nodejs.org/api/buffer.html) \| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String))** Buffer containing image data or String containing the path to an image file.
-   `operator` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** one of `and`, `or` or `eor` to perform that bitwise operation, like the C logic operators `&`, `|` and `^` respectively.
-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.raw` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** describes operand when using raw pixel data.
        -   `options.raw.width` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 
        -   `options.raw.height` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 
        -   `options.raw.channels` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 
