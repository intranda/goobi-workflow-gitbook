# Create thumbnails for accelerated image display

For some time now, it has been possible to create a `thumbs/` folder in Goobi workflow process folders. In this folder, thumbnails for the images in the folders in the `images/` folder can be stored. When doing this, you must follow a naming convention that is evaluated by Goobi workflow and used to display images efficiently.

## The thumbs folder

A folder below the `thumbs/` folder may only contain jpg images and must follow the following naming scheme to be used by Goobi:

```xml
<images-folder-name>_<size-of-longest-side-in-pixels>
```

For example, if you now have the following folder in the `images/` folder:

```bash
images/myexampleprocess_master
```

For thumbnails with a maximum page length of 1000 pixels you would have to create the following folder in the `thumbs/` folder and fill it with matching images:

```bash
thumbs/myexampleprocess_master_1000
```

## Example configuration

The folders and images in them can be created using a script step in Goobi workflow. The script step may contain multiple scripts to create thumbnails in multiple sizes. The following scripts create thumbnails for the master images in 800, 1600 and 3200 pixel sizes:

```bash
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {origpath} -d {processpath}/thumbs/master_{processtitle}_media_800 -D .jpg -o "-thumbnail 800x800"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {origpath} -d {processpath}/thumbs/master_{processtitle}_media_1600 -D .jpg -o "-thumbnail 1600x1600"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {origpath} -d {processpath}/thumbs/master_{processtitle}_media_3200 -D .jpg -o "-thumbnail 3200x3200"
```

For the derivatives, the calls are made in the same way:

```bash
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {tifpath} -d {processpath}/thumbs/{processtitle}_media_800 -D .jpg -o "-thumbnail 800x800"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {tifpath} -d {processpath}/thumbs/{processtitle}_media_1600 -D .jpg -o "-thumbnail 1600x1600"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {tifpath} -d {processpath}/thumbs/{processtitle}_media_3200 -D .jpg -o "-thumbnail 3200x3200"
```

The script `gm-convert.sh` used here can be downloaded here and should be placed in the folder `/opt/digiverso/goobi/scripts/`:

{% code title="gm-convert.sh" %}
```bash
#!/bin/bash

PATH=${PATH}:/usr/local/bin

set -e
set -u

USAGE="
$0 - wrapper script for GraphicsMagick's convert command.

Mandatory options:
    -s SOURCEDIR            Source folder with images to convert
    -d DESTDIR              Output folder
    -D DEST_EXTENSION       Output file extension

Other options:
    -S SOURCE_EXTENSION     Only convert source files with these extensions
    -o GMOPTION [ -o ... ]  GM Options

    Calling from Goobi - example script command (be careful with spaces within \"\"):
    /path/to/$(basename $0) \"-s{origpath}\" \"-d{tifpath}\" \"-D.tif\" \"-o+matte -depth 8 -compress JPEG\"
"


## check if the called tools exists
type -P gm &>/dev/null || { echo "ERROR: GraphicsMagick is required but seems not to be installed." >&2; exit 1; }


## check for the given arguments
[ "$#" -ge "3" ] || { echo "$USAGE"; exit 1; }    # at least
SOURCE_EXTENSION=".*"                             # if none specified use .* as source file type
GMOPTIONS=""                                      # if none specified use none
while getopts "s:d:S:D:o:"  OPCOES; do
  case $OPCOES in
    s ) SOURCEDIR="$OPTARG";;
    d ) DESTDIR="$OPTARG";;
    S ) SOURCE_EXTENSION="$OPTARG";;
    D ) DEST_EXTENSION="$OPTARG";;
    o ) GMOPTIONS="$GMOPTIONS $OPTARG";;
    ? ) echo "$USAGE"; exit 1;;
    esac
done

# check arguments
[ -d "${SOURCEDIR}" ] || { echo "ERROR: Input folder ${SOURCEDIR} does not exist." >&2; exit 1; }
[ -d "${DESTDIR}" ]   || mkdir -p "${DESTDIR}" || { echo "ERROR: Could not create destination folder ${DESTDIR}." >&2; exit 1; }
stat -t "${SOURCEDIR}/"*${SOURCE_EXTENSION} >/dev/null || { echo "ERROR: No *${SOURCE_EXTENSION} input files found in ${SOURCEDIR}" >&2; exit 1; }


# convert
cd "${SOURCEDIR}"
CTR=0
for i in *${SOURCE_EXTENSION}; do
  CTR=$((CTR+1))
  nice gm convert "$i" ${GMOPTIONS} "${DESTDIR}/${i%${SOURCE_EXTENSION}}${DEST_EXTENSION}" || { echo "ERROR: GM command failed: gm convert $i ${GMOPTIONS} ${DESTDIR}/${i%${SOURCE_EXTENSION}}${DEST_EXTENSION}" >&2; exit 1; }
done


# Success
echo "
Done converting $CTR images to $DEST_EXTENSION with GraphicsMagick.
Options used:          $GMOPTIONS
Source directory:      $SOURCEDIR
Destination directory: $DESTDIR
"

exit 0

# Notizen
# nice gm mogrify -depth 8 +matte -compress JPEG "${i}"
# if [ "$(tiffinfo ${i} 2>&1 | grep Bits | awk {'print $2'})" != "1" ]; then
# prepare !
```
{% endcode %}