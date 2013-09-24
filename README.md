psd2css
=======

A [forked](http://www.ps-scripts.com/bb/viewtopic.php?p=9745&sid=03d540b9a8788dee9a1f51d6539e0ee0#p9745) Photoshop script that exports all visible layers to CSS with the top, left, width, height, and background image properties using [rems](http://snook.ca/archives/html_and_css/font-size-with-rem).

This is a script that I created for myself that looks for all visible layers/groups and only exports the items at the root level. There currently isn't any support for child groups or selected layers.

## Instructions

1. Place the "Export Elements to CSS.jsx" file into your Photoshop Scripts folder:
~/Applications/Adobe\ Photoshop\ CC/Presets/Scripts

2. Restart Photoshop

3. File > Scripts > Export Elements to CSS


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

Since we're working with retina assets, all of my Photoshop docs are at retina size. This script takes all of layer measurements and divides them in half to get our base measurement. Then I round to the nearest 10th so that we have a 1:1 px ratio. Example: 11.8rem = 118px. This allows me to properly resize elements with full-width background images.

### Background Image

The background-image property references a SASS variable called **$url** that allows me to define the image path: `$url: 'image/path/to/files'` and then I add a retina `@2x` attribute:

```css
background-image: url('#{$url}images/"+layer.name+"@2x.png');
```

I then fill the background-image to the width of the parent element:

```css
* { -webkit-background-size: 100% auto }`
```