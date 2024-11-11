---
description: >-
  Help with displaying 3D objects in Goobi instead of images
---

# Handling of 3D Objects

Instead of two-dimensional images, 3D objects can also be saved in the `images` folder and displayed in the Goobi interface. Goobi can display the following 3D formats:

```bash
.obj
.ply
.stl
.fbx
.gltf
.glt
.x3d
```

However, full support for textures exists only for the `.obj`, `.gltf` and `.glb` formats, so use one of these formats if possible. DRACO compression is supported for `.gltf` and `.glb` formats.

## Additional resources

Often a 3D object needs additional resource files to be displayed correctly. These are usually image files for surface textures and `.mtl` files with material definitions for `.obj` files. These files should always be saved in a separate file folder next to the object file, with the same name as the object file without file extension. `.mtl` files can be given any name, whereas the naming of the image files is determined by the 3D object file or the `.mtl` file.

```bash
1234/images/myObject.obj
1234/images/myObject/materials.mtl
1234/images/myObject/textures01.jpg
1234/images/myObject/textures02.jpg
1234/images/anotherObject.glb
1234/images/andYetAnotherObject.gltf
1234/images/andYetAnotherObject/textures.jpg
```

## Known problems

* Very large 3D objects with over a million edges can often not be displayed by browsers or only very slowly. It is advisable to use only smaller files in Goobi. 
* If you use an `.mtl` file, sometimes no image is displayed. This may be due to the content of the `.mtl` file itself if it contains the following line: `Tr 1.0` or `d 0.0` This sets the transparency of the object to 100%, which means it is not displayed at all. Instead, the line must read `Tr 0.0` or `d 1.0` 
* The display of the object can also be influenced by the following line: `illum 1` or `illum 2` The `illum 1` option enhances specular reflections on the object, `illum 2` makes them possible. Mirroring reflections can make an object appear overexposed, but they can also emphasise the three-dimensional shape.