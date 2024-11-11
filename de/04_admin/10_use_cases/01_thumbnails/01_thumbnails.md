# Thumbnails erzeugen für beschleunigte Bildanzeige

Seit einiger Zeit gibt es die Möglichkeit, in Goobi workflow Vorgangsordnern einen `thumbs/` Ordner anzulegen. In diesem Ordner können thumbnails für die Bilder in den Ordnern im `images/` Ordner hinterlegt werden. Dabei ist eine Namenskonvention zu beachten, die von Goobi workflow ausgewertet und zur effizienten Anzeige von Bildern genutzt wird.

## Der thumbs Ordner

Ein Ordner unterhalb des `thumbs/`-Ordners darf nur jpg-Bilder enthalten und muss folgendem Namensschema folgen, damit er verwendet wird:

```xml
<images-folder-name>_<size-of-longest-side-in-pixels>
```

Wenn man nun zum Beispiel folgenden Ordner im `images/`-Ordner hat:

```bash
images/myexampleprocess_master
```

Müsste man für thumbnails mit der maximalen Seitenlänge von 1000 Pixeln folgenden Ordner im `thumbs/` Ordner erstellen und mit passenden Bildern befüllen:

```bash
thumbs/myexampleprocess_master_1000
```

## Beispiel-Konfiguration

Die Ordner und Bilder darin können mithilfe eines Script-Schrittes in Goobi workflow erzeugt werden. In dem Script-Schritt können auch mehrere Aufrufe stattfinden, um Thumbnails in mehreren Größen zu erstellen. Die folgenden Scripte erstellen thumbnails für die master-images in den Größen 800, 1600 und 3200 Pixel:

```bash
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {origpath} -d {processpath}/thumbs/master_{processtitle}_media_800 -D .jpg -o "-thumbnail 800x800"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {origpath} -d {processpath}/thumbs/master_{processtitle}_media_1600 -D .jpg -o "-thumbnail 1600x1600"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {origpath} -d {processpath}/thumbs/master_{processtitle}_media_3200 -D .jpg -o "-thumbnail 3200x3200"
```

Für die Derivate erfolgen die Aufrufe analog:

```bash
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {tifpath} -d {processpath}/thumbs/{processtitle}_media_800 -D .jpg -o "-thumbnail 800x800"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {tifpath} -d {processpath}/thumbs/{processtitle}_media_1600 -D .jpg -o "-thumbnail 1600x1600"
/bin/bash /opt/digiverso/goobi/scripts/gm-convert.sh -s {tifpath} -d {processpath}/thumbs/{processtitle}_media_3200 -D .jpg -o "-thumbnail 3200x3200"
```

Das hier genutzte Script `gm-convert.sh` kann hier heruntergeladen und sollte in den Ordner `/opt/digiverso/goobi/scripts/` gelegt werden:

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