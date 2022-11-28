# Rancid's Blender Scripts

Hint: if you're writing your scripts in an IDE instead of inside Blender 
you can get an easy auto-complete with:
https://github.com/nutti/fake-bpy-module

I haven't currently written any Blender scripts worth their own repository,
but I did just finish a script that other's might find useful.
So I figured I'd just start a repository for miscellaneous Blender scripts I've written.

# Bulk animation converter

Currently, this script is set up to convert any amount of animations from
.bvh files to .fbx files. It could easily be changed to convert from/to any
other file format that Blender supports. There's actually a commented out
chunk that would convert to .glTF files as well, but when exporting large
amounts of animations, I noticed a the .glTF files would, while very slowly,
start to increase in size meaning that they were picking up extra data 
somewhere in the Blender scene. The script goes through and purges anywhere data should be,
and then runs tools that are also supposed to clean the scene. So,
I don't know what's not getting removed or where the data is hiding. In reality,
with the current setup of the script, the performance cost of converting
to .glTF and the file size are probably negligible so if you really want
to convert to .glTF, just uncomment the lines and run the script. It's at
the point a setting tweak might be all that's needed to fix the issue.

A quick explanation of the setup is that there are two scripts. One is the
script that Blender runs which is converting everything, and the other is a 
Python script that manages Blender. The reason for the external script is
that Blender locks when running a script. You can try your hand at threading
but Blender pretty much tells you not to do that for a few reasons. So, the
external script just runs Blender and passes it the script to run. The script
that Blender runs just does your determined number of conversions and then
closes Blender. This frees up the resources and cleans the scene. The 
external script then runs Blender again and passes it the script to run 
again. This continues until all the conversions are done.
