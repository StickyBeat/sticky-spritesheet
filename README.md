sticky-spritesheet
==================

Custom TexturePacker exporter to combine with its AutoSD feature to write a single CSS file for handling regular and retina sprite sheets.

TexturePacker and AutoSD
------------------------

TexturePacker is a great tool, and it has a great feature called AutoSD. It enabled you to set up a spritesheet that will generate two PNGs. One in full size, which will be the retina spritesheet, and one in half size, which will be the regular spritesheet. 

If you choose CSS as output format, it will also generate two css files, one for each PNG. The CSS file will have a .sprite class to slap on span elements for all sprite sheet sprites, and one class for each sprite in your spritesheet. These classes will have background-position and width/height attributes that ensures it's just the part of the PNG corresponding to your sprite that will be visible in the span element.

The problem
-----------

So far, so great! The problem is that the "retina" CSS will specify width/height values that are equal to the physical pixel size of the retina spritesheet PNG. If you've done any retina stuff, you'll know that this isn't what you typically want. What you want is the "regular" pixel dimensions, and a background-size attribute that makes the retina PNG display at half the physical size.

The solution
------------

This custom exporter writes width/height for each sprite class as the physical pixel dimensions of the regular spritesheet - as normal. 

It also writes a background-size attribute on the main .sprite class, also in regular physical pixels. 

And also also: It writes a mediaquery thing in the regular CSS file that tells the browser to use the retina spritesheet when pixel density is right for it. And that's all that changes in retina mode!

Then all you do is scrap the retina CSS generated. If anybody knows how to keep this file from being generated in an easy way, please tell me.

So: The background-size on the main .sprite class ensures that the PNG is always used as if it had the regular pixel size. This makes the background-position of the individual sprite classes work both in regular and retina mode, assuming the spritesheet layout is identical in both PNG's. Luckily, the AutoSD feature let's you do this - it's even the default setting!

Assumptions
-----------

This exporter assumes a bunch of things:

- PNG is used as the format for the image files.
- The retina PNG is exported with the same name as the regular PNG, but with a -retina suffix (before the .png extension).
- The mediaquery conditions you want is what I hardcoded into the exporter. 

Comments and suggestions
------------------------

Mail that stuff to erik@stickybeat.se, please.
