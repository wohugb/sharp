## background

Set the background for the `embed`, `flatten` and `extend` operations.
The default background is `{r: 0, g: 0, b: 0, alpha: 1}`, black without transparency.

Delegates to the _color_ module, which can throw an Error
but is liberal in what it accepts, clipping values to sensible min/max.
The alpha value is a float between `0` (transparent) and `1` (opaque).

**参数** 

-   `rgba` **([String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object))** parsed by the [color](https://www.npmjs.org/package/color) module to extract values for red, green, blue and alpha.


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameter

**返回** **Sharp** 

## greyscale

Convert to 8-bit greyscale; 256 shades of grey.
This is a linear operation. If the input image is in a non-linear colour space such as sRGB, use `gamma()` with `greyscale()` for the best results.
By default the output image will be web-friendly sRGB and contain three (identical) color channels.
This may be overridden by other sharp operations such as `toColourspace('b-w')`,
which will produce an output image containing one color channel.
An alpha channel may be present, and will be unchanged by the operation.

**参数** 

-   `greyscale` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## grayscale

Alternative spelling of `greyscale`.

**参数** 

-   `grayscale` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `true`)

**返回** **Sharp** 

## toColourspace

Set the output colourspace.
By default output image will be web-friendly sRGB, with additional channels interpreted as alpha channels.

**参数** 

-   `colourspace` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** output colourspace e.g. `srgb`, `rgb`, `cmyk`, `lab`, `b-w` [...](https://github.com/jcupitt/libvips/blob/master/libvips/iofuncs/enumtypes.c#L568)


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 

## toColorspace

Alternative spelling of `toColourspace`.

**参数** 

-   `colorspace` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** output colorspace.


-   Throws **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** Invalid parameters

**返回** **Sharp** 
