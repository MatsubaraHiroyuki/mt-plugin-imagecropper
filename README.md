# Image Cropper Plugin for Movable Type #

The Image Cropper Plugin for Movable Type provides a simple
user interface for managing and generating custom thumbnails
from any image asset managed by Movable Type. 

The plugin was specifically designed to addressed the case
where publishers want the ability to produce different thumbnails
designed specifically for certain different locations on a web site. 
Furthermore, for each of these locations it is not sufficient
simply to scale the asset in question; rather the publisher
would rather crop the asset in a custom manner for each thumbnail
generated.

Finally, in order to properly annotate thumbnails to credit the 
photographer and preserve any required copyright notices, this 
plugin allows you place some text on the image accordingly.

This utility facilitates that process.

## Features ##

* Define a set of "prototypes" which in essence are a prescribed
  set of allowable thumbnail sizes.

* Manage all related thumbnails from a single dashboard.

* Create alternate thumbnails using a simple drag-and-drop cropping
  interface - without ever leaving Movable Type.

* Annotate thumbnails with a custom message.

* Place annotations using the orientation and location you specify 
  on the generated thumbnail.

* Hooks for designers to define thumbnail prototypes for their
  themes and template sets so that their users don't have to.

## Installation ##

To install this plugin follow the instructions found here:

http://tinyurl.com/easy-plugin-install

## Usage ##

**Managing "Prototypes"**

To manage the list of allowable cropped thumbnails for your web
site, select "Thumbnail Prototypes" from the Preferences menu from
within Movable Type.

Then simply add and edit thumbnail prototypes by defining the following
properties for each:

* Max Width
* Max Height
* Label (used later for selecting and placing cropped images on your web site)

**Managing Thumbnails**

Once you have defined a list of prototypes you can begin creating
thumbnails. To do that, navigate to the Edit Asset screen associated
with the asset in question. In the sidebar you will see a link called
"Generate Thumbnails." Clicking that link will take you to the cropping
dashboard.

**Adding Cropped Images to your Website**

Once you have created a cropped thumbnail, you can display it on your
web site using the following template code:

    <mt:Asset id="136">
      <mt:CroppedAsset label="Square">
        <img src="<$mt:AssetURL$>" />
      </mt:CroppedAsset>
    </mt:Asset>

It is quite possible however that you need to display the cropped
version of an asset only if it is available and fall back to a simple
scaled version of the thumbnail if a cropped version cannot be found.
The following template code shows how you can use `<mt:else>` to do
just that:

    <mt:Asset id="136">
      <mt:CroppedAsset label="Square">
        <img src="<$mt:AssetURL$>" width="<$mt:AssetProperty property="image_width"$>" height="<$mt:AssetProperty property="image_height"$>" />
      <mt:Else>
        <mt:PrototypeVar label="Square" property="max_width" setvar="width" />
        <mt:PrototypeVar label="Square" property="max_height" setvar="height" />
        <img src="<$mt:CropThumbnailURL width="$width" height="$height"$>" width="<$mt:Var name="width"$>" height="<$mt:Var name="height"$>" />
      </mt:CroppedAsset>
    </mt:Asset>

## Config Directives ##

* **`DefaultCroppedImageText`** - Determines the default text to be
  used when annotating images.

## Template Tags ##

* `<mt:CroppedAsset>` - Places the desired cropped image asset
  into context. This tag must be called with an existing asset
  (the parent asset) already in context. See example above. Allowable
  arguments:

  * `label` - The label to filter by.

* `<$mt:ScaleThumbnailURL$>` - URL of scale image asset to max size. Allowable
  arguments:

  * `width` - maximum of image width.
  * `height` - maximum of image height.

* `<$mt:FillThumbnailURL$>` - URL of fill image asset to min size. Allowable
  arguments:

  * `width` - minimum of image width.
  * `height` - minimum of image height.

* `<$mt:CropThumbnailURL$>` - URL of crop image asset to size. Allowable
  arguments:

  * `width` - image width.
  * `height` - image height.
  * `align_x` - cutoff block (optional) as`left``center``right`.
  * `align_y` - cutoff block (optional) as `top``center``bottom`.

* `<$mt:PrototypeVar$>` - Return prototype value in custom prototypes. Allowable
  arguments:

  * `label` - label of prototype.
  * `property` - property of prototype as `max_width``max_height`.

## Designer Guide ##

The Image Cropper plugin exposes a simple set of hooks that can be
embedded in a theme's `config.yaml` file so that designers can specify 
the exact dimensions of their fixed image prototypes. When prototypes
are defined in this way, they will appear automatically on the 
**Preferences > Thumbnail Prototypes** screen for blogs using the corresponding
theme. 

To define thumbnail prototypes via `config.yaml`, consult this super 
simple example:

    generic_blog_theme:
      label: 'Generic Blog Theme'
      thumbnail_prototypes:
        feature_thumb:
          label: 'Featured Thumbnail'
          max_width: 100
          max_height: 90
        feature_lrg:
          label: 'Homepage Feature'
          max_width: 350
          max_height: 300
      templates:
        index:
          etc...

example of define prototypes for MT5 theme via `config.yaml`.
**Design > Crop Prototypes** screen for blogs using the corresponding
theme MT5 or later.


    themes:
      mtVicunaSimple:
        id: mtVicunaSimple
        label: mt.Vicuna Simple Theme
        thumbnail_prototypes:
          feature_thumb:
            label: Featured Thumbnail
            max_width: 300
            max_height: 90

As you can see you can define one or more prototypes easily for a theme.
Designers can specify the label for the prototype as well as its 
dimensions.

## This modified version of ImageCropper

This modified version of Image Cropper for MT5 or later maintain by [naoaki.onozaki](https://github.com/naoaki011).

Original version of Image Cropper created by Endevver, LLC.

# Help, Bugs and Feature Requests ##

If you are having problems installing or using the plugin, please check out our general knowledge base and help ticket system at [help.endevver.com](http://help.endevver.com).

If you know that you've encountered a bug in the plugin or you have a request for a feature you'd like to see, you can file a ticket in the [Image Cropper project](https://endevver.lighthouseapp.com/projects/34923-image-cropper) in our issue tracking system and we'll get to it as soon as possible.

## Copyright ##

This plugin was created from the kind support of 
Talking Points Memo (http://www.talkingpointsmemo.com/), who
supports and appreciates open source. We <3 TPM.

Copyright 2009, Endevver, LLC. All rights reserved.

## License ##

This plugin is licensed under the GPL v2.

# About Endevver #

We design and develop web sites, products and services with a focus on 
simplicity, sound design, ease of use and community. We specialize in 
Movable Type and offer numerous services and packages to help customers 
make the most of this powerful publishing platform.

http://www.endevver.com/

