psd2css
=======

A [forked](http://www.ps-scripts.com/bb/viewtopic.php?p=9745&sid=03d540b9a8788dee9a1f51d6539e0ee0#p9745) Photoshop script that exports all visible layers to CSS with the top, left, width, height, and background image properties using [rems](http://snook.ca/archives/html_and_css/font-size-with-rem).

This is a script that I created for myself that looks for all visible layers/groups and only exports the items at the root level. The top/left properties allow me to absolutely positiong the elements.

There currently is no support for child groups or selected layers, nor was this ever intended for scalablity. This supports my current workflow.

## Instructions

1. Place the "Export Elements to CSS.jsx" file into your Photoshop Scripts folder: `~/Applications/Adobe\ Photoshop\ CC/Presets/Scripts`

2. Restart Photoshop

3. Naigate to `File > Scripts` and run `Export Elements to CSS`

4. You can add this to your shortcuts via `Edit > Keyboard Shortcuts`



### Export Example

```css
#logo{
 top: 10rem;
 left: 11.8rem;
 width: 8.4rem;
 height: 5.5rem;
 background-image: url('#{url}images/logo@2x.png');
}
```

### REM units

I mostly work with retina assets so all of my Photoshop documents are at retina size. This script collects all of the layer measurements and divides them in half to get our base measurement. Then I round to the nearest 10th so that we have a 1:1 px ratio. For example: 11.8rem = 118px. This allows me to properly resize elements with full-width background images.

### Background Images

The background-image property references a SASS variable: **$url** which allows me to define the image URL path: `$url: 'image/path/to/files'` and then I append it with the retina prefix `@2x`:

```css
background-image: url('#{$url}images/"+layer.name+"@2x.png');
```

I am then able to declare all child elements to fill the background-image to the size of the parent element:

```css
#container * { -webkit-background-size: 100% auto }
```