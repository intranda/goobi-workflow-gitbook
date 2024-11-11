# config_contentServer.xml

In the file `config_contentServer.xml`, technical details about the content server used in Goobi are provided. The configuration file can be used for Goobi Workflow and Goobi Viewer in the same way.

The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/config_contentServer.xml
```

For example, this configuration file looks as follows:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<config>
	<localConfigPath value="/opt/digiverso/config/config_contentServer.xml" />
	<defaultResolution
		value="600" />
	<connectionTimeout>2000</connectionTimeout>
	<openJpeg>
		<binaries>/opt/digiverso/OpenJpeg</binaries>
	</openJpeg>
	<imageToPdfSizeFactor tiff="0.35" jpg="1.0" />
	<maxFileLength
		file=""
		value="0" />
	<scaling
		quality="QUALITY"
		thumbnailQuality="SPEED"
		maxStepSize="50" />
	<defaultFileNames>
		<image
			value="image_$datetime"
			sendAsAttachment="false" />
		<pdf
			value="ContentServer_$datetime"
			sendAsAttachment="true" />
	</defaultFileNames>
	<defaultRepositoryPathImages
		value="file:///opt/digiverso/viewer/media/" />
	<defaultRepositoryPathPdf
		usage="true"
		value="file:///opt/digiverso/viewer/pdf/" />
	<defaultRepositoryPathAlto
		usage="false"
		value="file:///opt/digiverso/viewer/alto/"
		fontFile="font.ttf" />
	<defaultRepositoryPathMets
		value="file:///opt/digiverso/viewer/mets/" />
	<defaultImageConfig defaultFormat="jpeg" />
	<defaultPdfConfig
		pagesize="A4"
		imageDpi="0"
		imageScale="1.0"
		imageScaleToBox=""
		imageCompression="0"
		convertToGrayscale="false"
		writeAsPdfA="false"
		metsFileGroup="PRESENTATION" 
		metsFileUrlRemove="file:\/\/\/opt\/digiverso\/viewer\/media\/" writeAsPdfA="false" />
	<defaultHighlightColor
		valueRed="255"
		valueGreen="255"
		valueBlue="0"
		valueAlpha="255" />
	<imageTypeSettings>
		<type format="png">
			<settings scaleWithScalr="false"></settings>
		</type>
		<type compression="jpeg" colorType="grayscale">
			<settings forceConvertToBuffered="true"></settings>
		</type>
		<type format="jpeg">
			<settings scaleWithScalr="true"></settings>
		</type>
		<type format="tiff" embeddedColorProfile="true">
			<settings scaleWithScalr="false"></settings>
		</type>
		<type format="jpg2000">
			<settings scaleWithScalr="false" allowSubSampling="true"></settings>
		</type>
		<type
			format="default"
			colorType="default"
			compression="default"
			embeddedColorProfile="both"
			minSize="0"
			maxSize="0">
			<settings
				allowRenderWithJAI="false"
				scaleWithScalr="true"
				mergeWithJAI="false"
				forceConvertToBuffered="false"
				forceConvertToRGB="false"
				forwardDirectlyIfPossible="true"
				preferredImageReader="com.github.jaiimageio"
				preferredImageWriter="com.github.jaiimageio">
			</settings>
		</type>
	</imageTypeSettings>
	<watermark
		use="false"
		scale="true"
		convertColorSpace="false"
		scaleToPercent="6"
		configFile="file:///opt/digiverso/viewer/config/config_imageFooter.xml" />
	<errorWaterMark
		title="Error"
		titleFontSize="20" 
		messageFontSize="14"
		messageMaxLineLength="60" />
	<pdfTitlePage
		use="true"
		templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
		defaultTemplate="default"
		configFile=""
		fontFile="" />
	<pdfChapterTitlePages
		use="true"
		templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
		defaultTemplate="default" />
	<singlePdfTitlePage
		use="false"
		templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
		defaultTemplate="default" />
	<restapi use="false">
		<iiif>
			<attribution></attribution>
			<logo></logo>
			<license></license>
		</iiif>
		<discloseContentLocation>true</discloseContentLocation>
	</restapi>
	<contentCache
		useCache="false"
		size="100"
		useShortFileNames="false"
		path=""
		cachePartialImages="false" />
	<thumbnailCache
		useCache="false"
		size="100"
		useShortFileNames="false"
		path="" />
	<pdfCache
		useCache="true"
		size="100"
		useShortFileNames="false" />
	<memoryUsage
		maximalParallelImageRequests="0"
		maximalParallelPdfRequests="0"
		lowMemoryShreshold="1000000000"
		memoryUnit="MB"
		timeoutUnit="s"
		triggerGCAfterAction="true">
		<image>
			<maxParallelRequests>20</maxParallelRequests>		
			<lowMemoryThreshold>200</lowMemoryThreshold>
			<lowMemoryTimeout>8</lowMemoryTimeout>
		</image>
		<pdf>
			<maxParallelRequests>8</maxParallelRequests>		
			<lowMemoryThreshold>500</lowMemoryThreshold>
			<lowMemoryTimeout>10</lowMemoryTimeout>
		</pdf>
		<metsPdf>
			<maxParallelRequests>4</maxParallelRequests>		
			<lowMemoryThreshold>1000</lowMemoryThreshold>
			<lowMemoryTimeout>20</lowMemoryTimeout>
		</metsPdf>
	</memoryUsage>
	<S3>
		<useCustom>true</useCustom>
		<Endpoint>http://192.168.178.124:9000</Endpoint>
		<AccessKeyID>24JW1VB99T8MAU94TBIC</AccessKeyID>
		<SecretAccessKey>OTrwBXGVBacVdXNSI7SKKrX8b+CqwANa5ngLZ4lB</SecretAccessKey>
	</S3>
</config>
```

## Data types

In this configuration file settings are made with different data types. For overview all used types are explained briefly in the following table:

| Data type | Examples | Meaning |
| --------- | -------- | ------- |
| `boolean` | `false`, `true` | Boolean value: can be true or false |
| `string` | `TEXT`, `MB` | Text: can contain any characters |
| `integer` | `0`, `1000` | Integer: can contain all positive or negative numbers (or 0) |
| `long` | `0`, `1000000000` | Large integer: like `integer`, can contain significantly larger numbers, mostly used for milliseconds and timestamps |
| `float` | `0`, `1.0` | Floating point number: decimal number with few digits precision |
| `double` | `0`, `99.999` | Floating point number: decimal number with many digits precision |

## General settings and default values

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `value` | string | /opt/digiverso/config/config_contentServer.xml` | This parameter can be used in the `localConfigPath` element and specifies the location of this configuration file. |
| `value` | integer | `72` | This parameter can be used in the `defaultResolution` element and specifies the default resolution of a file. The resolution is DPI (Dots Per Inch), i.e. pixels per inch. |
| `connectionTimeout` | integer | `2000` | This value specifies a timeout that must not be exceeded when sending image files. |
| `binaries` | string | `/opt/digiverso/OpenJpeg` | This element specifies the path to a library to process image files with. |

In addition, the `imageToPdfSizeFactor` element can be used to set arbitrary parameters for file types for which a special factor should be used to scale from that file type to a PDF file (see example). In that case the image file extensions are used as parameter names and the scaling factors as values. A scaling of 1.0 means that the image size remains the same. Values below 1.0 or above 1.0 reduce or enlarge the image. The value 0 should not be used.

The size of image files can be limited on the content server. The following parameters can be used in the `maxFileLength` element:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `value` | integer | `0` | This parameter specifies the maximum file size in megabytes. 0 can be specified to deactivate the size limit. |
| `file` | string | | This parameter specifies a file which can be used as a substitute in case of an error (if the file is too large). |

For different application purposes it may be useful to scale images differently. The following parameters can be used in the `scaling` element:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `quality` | string | `QUALITY` | This parameter specifies the scaling quality. The values `SPEED`, `QUALITY` and `ULTRAQUALITY` can be used. |
| `thumbnailQuality` | string | `SPEED` | This parameter specifies the scaling quality for thumbnails. The values `SPEED`, `QUALITY` and `ULTRAQUALITY` can be used. |
| `maxStepSize` | integer | `50` | This parameter additionally specifies a quality factor for scaling image files with the "Java Advanced Imaging" library (JAI). It can be between 0 and 99. Image files have a higher quality the higher this value is. A lower value, on the other hand, speeds up the loading process. Recommended values are between 10 and 50. |

For downloading images generated in the content server, a default file name can be specified here. The following parameters can be used in the `image` and `pdf` elements within the `defaultFileNames` element:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `value` | string | `image_$timestamp` for image and `ContentServer_$timestamp` for pdf | This parameter specifies how a file name should be formed. Here `$timestamp` can be used as a placeholder for the current time. |
| `sendAsAttachment` | boolean | `false` for image and `true` for pdf | This parameter specifies whether an `attachment` header field should be set in the server response. |

Default paths for locations of different file types can be specified for non-complete requests to the content server. The following parameters can be used in the `defaultRepositoryPathImages`, `defaultRepositoryPathPdf`, `defaultRepositoryPathAlto`, and `defaultRepositoryPathMets` elements:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `usage` | boolean | `false` | This parameter can be used with the elements `defaultRepositoryPathPdf` and `defaultRepositoryPathAlto` and specifies whether this path should be used. |
| `value` | string | `file:///opt/digiverso/viewer/media/` or `.../alto/` | This parameter can be used with all elements and specifies the path to the corresponding folder. |
| `fontFile` | string | | This parameter can only be used with `defaultRepositoryPathAlto` and specifies the path to a font file. |

The `image` data type initially includes all image file types which are not specified in detail. Therefore, `defaultImageConfig` can be used to make settings for image files. The following parameters can be used in the `defaultImageConfig` element:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `defaultFormat` | string | `jpeg` | This parameter specifies the default image type. |

PDF files are configured separately because they have some special properties unlike other image file formats. The following parameters can be used in the `defaultPdfConfig` element:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `pagesize` | string | `A4` | This parameter specifies the page size of the PDF document. Possible values are `A4`, `A4Box`, and `original`. |
| `imageDpi` | float | `0` | This parameter specifies the resolution (pixels per inch / dots per inch). The image file size (in pixels) remains the same. 0 can be specified to disable resolution scaling. |
| `imageScale` | float | `1.0` | This parameter specifies the image scaling. 1.0 means the original size. A value below 1.0 decreases the image size, a value above 1.0 increases it. This value should not be set to 0, otherwise the image will disappear (0 pixel size). |
| `imageScaleToBox` | string | | This parameter specifies how the image file should be scaled. A combination of two positive numbers (width and height) is expected in this field. Both numbers are separated by an `x` and must not contain any other characters (e.g. spaces). For example, this value may look like `1200x900` or `4500x2000`. |
| `imageCompression` | integer | `0` | This parameter specifies how much the image file should be compressed. 0 is a default value where a suitable JPEG compression is automatically selected. 0 should normally always be used. |
| `convertToGrayscale` | boolean | `false` | This parameter specifies whether the image file should be converted to grayscale. |
| `writeAsPdfA` | boolean | `false` | This parameter specifies whether the image file should be of type PDF-A. |
| `metsFileGroup` | string | `DEFAULT` | This parameter specifies which metadata group should be used. |
| `metsFileUrlRemove` | string | | This parameter can be used to specify a URL which should not be used as a reference source for meta information when exporting PDF files. |

A color can be specified to mark different image elements. The following parameters can be used in the `defaultHighlightColor` element:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `valueRed` | integer | `255` | This parameter specifies the red value in the range from 0 to 255. |
| `valueGreen` | integer | `255` | This parameter specifies the green value in the range from 0 to 255. |
| `valueBlue` | integer | `0` | This parameter specifies the blue value in the range from 0 to 255. |
| `valueAlpha` | integer | `255` | This parameter specifies the alpha (transparency) value in the range from 0 to 255. |

The following table shows some simple color examples:

| Configuration | Color |
| ------------- | ----- |
| `valueRed="0" valueGreen="0" valueBlue="0"` | Black |
| `valueRed="0" valueGreen="0" valueBlue="255"` | Blue |
| `valueRed="0" valueGreen="255" valueBlue="0"` | Green |
| `valueRed="0" valueGreen="255" valueBlue="255"` | Cyan |
| `valueRed="255" valueGreen="0" valueBlue="0"` | Red |
| `valueRed="255" valueGreen="0" valueBlue="255"` | Magenta |
| `valueRed="255" valueGreen="255" valueBlue="0"` | Yellow |
| `valueRed="255" valueGreen="255" valueBlue="255"` | White |

Where `alpha="255"` means full opacity of the color (covers the image area completely) and `alpha="0"` means no opacity (invisible).

```xml
<localConfigPath value="/opt/digiverso/config/config_contentServer.xml" />
<defaultResolution
	value="600" />
<connectionTimeout>2000</connectionTimeout>
<openJpeg>
	<binaries>/opt/digiverso/OpenJpeg</binaries>
</openJpeg>
<imageToPdfSizeFactor tiff="0.35" jpg="1.0" />
<maxFileLength
	file=""
	value="0" />
<scaling
	quality="QUALITY"
	thumbnailQuality="SPEED"
	maxStepSize="50" />
<defaultFileNames>
	<image
		value="image_$datetime"
		sendAsAttachment="false" />
	<pdf
		value="ContentServer_$datetime"
		sendAsAttachment="true" />
</defaultFileNames>
<defaultRepositoryPathImages
	value="file:///opt/digiverso/viewer/media/" />
<defaultRepositoryPathPdf
	usage="true"
	value="file:///opt/digiverso/viewer/pdf/" />
<defaultRepositoryPathAlto
	usage="false"
	value="file:///opt/digiverso/viewer/alto/"
	fontFile="font.ttf" />
<defaultRepositoryPathMets
	value="file:///opt/digiverso/viewer/mets/" />
<defaultImageConfig defaultFormat="jpeg" />
<defaultPdfConfig
	pagesize="A4"
	imageDpi="0"
	imageScale="1.0"
	imageScaleToBox=""
	imageCompression="0"
	convertToGrayscale="false"
	writeAsPdfA="false"
	metsFileGroup="PRESENTATION" 
	metsFileUrlRemove="file:\/\/\/opt\/digiverso\/viewer\/media\/" writeAsPdfA="false" />
<defaultHighlightColor
	valueRed="255"
	valueGreen="255"
	valueBlue="0"
	valueAlpha="255" />
```

## Image file types

Within the `imageTypeSettings` element, settings for any number of image file types can be defined. For each image file type a `type` element with the sub-element `settings` is specified.

For file types (`type`) the following parameters can be used:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `format` | string | `default` | This parameter specifies the type of the image file. This type corresponds to the associated file extension. |
| `minSize` | double | `0` | This parameter specifies the minimum size (in bytes) of an image file. |
| `maxSize` | double | `0` | This parameter specifies the maximum size (in bytes) of an image file. |
| `compression` | string | `default` | This parameter specifies a compression type. |
| `colorType` | string | `default` | This parameter specifies the way color values are stored. |
| `embeddedColorProfile` | string | `both` | This parameter specifies a color profile. |
| `watermark` | boolean | | This parameter specifies whether watermarks should be used. |

 **Note:** The `minSize` and `maxSize` parameters are queried as floating point numbers in the configuration, but later processed as `long`-numbers. Therefore, only integers should be specified.

For file type settings (`settings`) the following parameters can be used:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `preferredImageReader` | string | | This parameter specifies a Java class that can read image files of this file type. |
| `preferredImageWriter` | string | | This parameter specifies a Java class that can write image files of this file type. |
| `mergeWithJAI` | boolean | `false` | This parameter specifies whether the "Java Advanced Imaging" library (JAI) should be used. |
| `allowRenderWithJAI` | boolean | `false` | This parameter specifies whether images should be rendered using the "Java Advanced Imaging" library (JAI). |
| `scaleWithScalr` | boolean | `false` | This parameter specifies whether images should be scaled using the "Scalr" algorithm. This gives even better results, but is slower. Normally this value should be `false`.
| `forceConvertToBuffered` | boolean | `false` | This parameter specifies whether images should be buffered during processing. |
| `forceConvertToRGB` | boolean | `false` | This parameter specifies whether images should be converted to the `RGB` color model during processing. |
| `forwardDirectlyIfPossible` | boolean | `true` | This parameter specifies whether images that do not need further processing should be taken directly from the raw data. If this option is set to `true`, some image files may be processed faster. This setting has the side effect that some meta information of image files will be reused without filtering or adjustment by the content server. |
| `allowSubSampling` | boolean | `false` | This parameter specifies whether to use "SubSampling". |

```xml
<imageTypeSettings>
	<type format="png">
		<settings scaleWithScalr="false"></settings>
	</type>
	<type compression="jpeg" colorType="grayscale">
		<settings forceConvertToBuffered="true"></settings>
	</type>
	<type format="jpeg">
		<settings scaleWithScalr="true"></settings>
	</type>
	<type format="tiff" embeddedColorProfile="true">
		<settings scaleWithScalr="false"></settings>
	</type>
	<type format="jpg2000">
		<settings scaleWithScalr="false" allowSubSampling="true"></settings>
	</type>
	<type
		format="default"
		colorType="default"
		compression="default"
		embeddedColorProfile="both"
		minSize="0"
		maxSize="0">
		<settings
			allowRenderWithJAI="false"
			scaleWithScalr="true"
			mergeWithJAI="false"
			forceConvertToBuffered="false"
			forceConvertToRGB="false"
			forwardDirectlyIfPossible="true"
			preferredImageReader="com.github.jaiimageio"
			preferredImageWriter="com.github.jaiimageio">
		</settings>
	</type>
</imageTypeSettings>
```

## Water marks

When automatically processing and checking image files, the content server can set watermarks. These are images or parts of images that are inserted into the processed image as a kind of identity information (of the author). Watermarks can be configured with the `watermark` element and contain the following parameters:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `use` | boolean | `false` | This parameter specifies whether watermarks should be used. |
| `configFile` | string | | This parameter specifies the path to another configuration file for the information in the watermark. |
| `scale` | boolean | `false` | This parameter specifies whether watermarks should be scaled. |
| `scaleToPercent` | integer | `0` | This parameter specifies to which size (in percent) the watermark should be scaled. |
| `convertColorSpace` | boolean | `true` | This parameter can be set to `true` to automatically convert color values for watermarks. This conversion converts from integer to byte values and should normally have no effect on the actual image content. |

Error watermarks can be used not to display errors in documents on a subsequent error web page, but to use them as watermarks (=overlay) directly in the image files. These can be configured with the `errorWaterMark` element and contain the following parameters:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `title` | string | | This parameter specifies the title to be included in an error watermark. |
| `titleFontSize` | integer | | This parameter specifies the font size to use for the title of an error watermark. |
| `messageFontSize` | integer | `14` | This parameter specifies which font size the error message (`message`) of the error watermark should have. |
| `messageMaxLineLength` | integer | `60` | This parameter specifies the maximum number of characters that should be in one line of the error message of an error watermark. |

```xml
<watermark
	use="false"
	scale="true"
	convertColorSpace="false"
	scaleToPercent="6"
	configFile="file:///opt/digiverso/viewer/config/config_imageFooter.xml" />
<errorWaterMark
	title="Error"
	titleFontSize="20" 
	messageFontSize="14"
	messageMaxLineLength="60" />
```

## PDF title pages

The content server can generate three different types of artificial title pages and insert them at appropriate places in multi-page PDF files. Artificial title pages are pages that contain some meta information about the document or chapter or document section that follows. Metadata is read from METS files of the corresponding process. Additionally, it is also possible to display image content linked in the METS file. The layout as well as static contents of the metadata pages are specified by XML documents, so-called templates, which can be customized according to individual needs.

With `pdfTitlePage` a unique title page can be generated for the entire PDF document. It is inserted before the first page and can only contain information about the entire work and the top structural element contained in the PDF file.

The `pdfChapterTitlePages` element can be used to insert title pages before each chapter or structure element and can contain information about the respective structure element and the overall work. For example, these pages can contain information about the document structure (tables of contents, chapters, subchapters, appendices, etc.).

The 'singlePdfTitlePage' element can be used to include additional, individual title pages in the PDF document, which provide information about special places in a book, for example. It can contain only information about the whole work.

.fo` template files can be used to generate additional PDF title pages. These can either be specified in server requests or specified in the following XML elements.

The specified folders (`templateFolder`) must contain at least for each active metadata page the XML file with file extension `.fo` specified in `defaultTemplate`, and the file `fop.xconf` which contains further settings for conversion to PDF using "Apache fop". Details about "Apache fop" can be found [at this location ](https://xmlgraphics.apache.org/fop/).

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `use` | boolean | `false` | This parameter can be used with all types of title pages and specifies whether they should be used. |
| `templateFolder` | string | `/` | This parameter can be used with all types of title pages and specifies a folder where a template file is located. |
| `defaultTemplate` | string | `default` | This parameter can be used with all types of title pages and specifies a (non-default) template to use. A template file has the file extension `.fo` |
| `configFile` | string | | This parameter can only be used with `pdfTitlePage` and specifies the path to another configuration file. |
| `fontFile` | string | | This parameter can only be used with `pdfTitlePage` and specifies the path to a font file (e.g. a `.ttf` file). |

```xml
<pdfTitlePage
	use="true"
	templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
	defaultTemplate="default"
	configFile=""
	fontFile="" />
<pdfChapterTitlePages
	use="true"
	templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
	defaultTemplate="default" />
<singlePdfTitlePage
	use="false"
	templateFolder="file:///opt/digiverso/viewer/config/PDFTitlePage/"
	defaultTemplate="default" />
```

## REST API

The REST API can be used to retrieve information about image files at the content server. The parameters `attribution`, `logo` and `license` are additional specifications that can optionally be set in the image metadata of the returned image files.

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `use` | boolean | `false` | This parameter can be used to specify whether the REST API should be used. |
| `attribution` | string | | This value contains information about an IIIF attribution. |
| `logo` | string | | This value contains information about an IIIF logo. |
| `license` | string | | This value contains information about an IIIF license. |
| `discloseContentLocation` | boolean | `true` | This value can be set to `true` to send the storage path or URI to the client in the REST API request response. |

```xml
<restapi use="false">
	<iiif>
		<attribution></attribution>
		<logo></logo>
		<license></license>
	</iiif>
	<discloseContentLocation>true</discloseContentLocation>
</restapi>
```

## Cache storage

Caches can be used to temporarily store image data so that it is not necessary to recalculate all data for each (possibly identical) request. Different caches are used for processing different file types, which can be configured in more detail with the following XML elements. The `contentCache` element can be used for a general cache for image files, the `pdfCache` element for a cache for PDF files, and the `thumbnailCache` element for a cache for thumbnails.

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `useCache` | boolean | `false` | This parameter can be used with all cache types and specifies whether the respective cache should be used. |
| `size` | long | `100` | This parameter can be used with all cache types and specifies the maximum size in megabytes of the respective cache. |
| `useShortFileNames` | boolean | `false` | This parameter can be used with all cache types and specifies whether to use shortened file names. These will then only contain differing parts of the file path, but are not recommended. |
| `path` | string | | This parameter can be used with `contentCache` and `thumbnailCache` and specifies a path where the cache should be stored. |
| `cachePartialImages` | boolean | `false` | This parameter can only be used with `contentCache` and specifies whether to use a cache for partial images. |

```xml
<contentCache
	useCache="false"
	size="100"
	useShortFileNames="false"
	path=""
	cachePartialImages="false" />
<thumbnailCache
	useCache="false"
	size="100"
	useShortFileNames="false"
	path="" />
<pdfCache
	useCache="true"
	size="100"
	useShortFileNames="false" />
```

## Performance

The `memoryUsage` element can be used to specify some memory and runtime constraints for the content server. The `memoryUsage` element contains general settings and further subelements for specific file types. The following parameters can be used for `memoryUsage`:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `maximalParallelImageRequests` | integer | `0` | This parameter specifies how many requests may be sent simultaneously for image files. |
| `maximalParallelPdfRequests` | integer | `0` | This parameter specifies how many requests may be sent simultaneously for PDF files. |
| `lowMemoryThreshold` | long | `1000 000 000` | This parameter specifies the maximum data transfer time for all file types. |
| `memoryUnit` | string | `B` | This parameter specifies the unit of measurement for the memory size specifications in all `lowMemoryThreshold` elements. |
| `timeoutUnit` | string | `MILLIS` | This parameter specifies the unit of measure for the time information in all `lowMemoryTimeout` elements. |
| `triggerGCAfterAction` | boolean | `true` | This parameter can be set to `true` to periodically trigger the cleaning up of stale data (`garbage collection`). |

For the parameter `memoryUnit` there are some, partly misleading, values. The following table shows in each case which values can be used and which exact numeric values they correspond to internally.

| Unit | Factor | Designation |
| ---- | ------ | ----------- |
| `B` | `1` | Byte |
| `K` or `KB` | `1000` | Kilobyte |
| `KI` or `KIB` | `1024` | Kibibyte |
| `M` or `MB` | `1000*1000` | Megabyte |
| `MI` or `MIB` | `1024*1024` | Mebibyte |
| `G` or `GB` | `1000*1000*1000` | Gigabyte |
| `GI` or `GIB` | `1024*1024*1024` | Gibibyte |
| `T` or `TB` | `1000*1000*1000*1000` | Terabyte |
| `TI` or `TIB` | `1024*1024*1024*1024` | Tebibyte |

There are also several possible values for the `timeoutUnit` parameter. The following table shows in each case how these are interpreted internally:

| Unit | Factor | Designation |
| ---- | ------ | ----------- |
| `S` or `SECOND` or `SECONDS` | `1` | One second |
| `M` or `MS` or `MILLI` or `MILLIS` | `1/1000` | One millisecond |
| `MU` or `MICRO` or `MICROS` | `1/1000 000` | One microsecond |
| `N` or `NS` or `NANO` or `NANOS` | `1/1000 000 000` | One nanosecond |

With the sub-elements `image`, `pdf` and `metsPdf` special settings can be made for the corresponding file types. The following parameters can be used equally for all subelements:

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `maxParallelRequests` | integer | `0` | This value specifies the maximum number of parallel requests that may be made simultaneously. |
| `lowMemoryThreshold` | long | `0` | This value specifies the maximum amount of data that should be sent simultaneously. This value must be configured to match the `memoryUnit` parameter in the `memoryUsage` element. |
| `lowMemoryTimeout` | long | `1000` | This value specifies the maximum data transfer time. This value must be configured to match the `timeoutUnit` parameter in the `memoryUsage` element. |

```xml
<memoryUsage
	maximalParallelImageRequests="0"
	maximalParallelPdfRequests="0"
	lowMemoryShreshold="1000000000"
	memoryUnit="MB"
	timeoutUnit="s"
	triggerGCAfterAction="true">
	<image>
		<maxParallelRequests>20</maxParallelRequests>		
		<lowMemoryThreshold>200</lowMemoryThreshold>
		<lowMemoryTimeout>8</lowMemoryTimeout>
	</image>
	<pdf>
		<maxParallelRequests>8</maxParallelRequests>		
		<lowMemoryThreshold>500</lowMemoryThreshold>
		<lowMemoryTimeout>10</lowMemoryTimeout>
	</pdf>
	<metsPdf>
		<maxParallelRequests>4</maxParallelRequests>		
		<lowMemoryThreshold>1000</lowMemoryThreshold>
		<lowMemoryTimeout>20</lowMemoryTimeout>
	</metsPdf>
</memoryUsage>
```

## S3 storage

The `S3` element can optionally be used to include S3 cloud storage to offload data.

| Property | Type | Default Value | Description |
| -------- | ---- | ------------- | ----------- |
| `useCustom` | boolean | | This value can be used to specify whether S3 storage should be used. |
| `Endpoint` | string | | This value specifies the address (URL) of the S3 server. If necessary, the protocol (`http` or `https`) and the port number must also be specified. |
| `AccessKeyID` | string | | This value specifies the ID of the account on the S3 service. |
| `SecretAccessKey` | string | | This value specifies the key / password of the S3 account. |

```xml
<S3>
	<useCustom>true</useCustom>
	<Endpoint>http://192.168.178.124:9000</Endpoint>
	<AccessKeyID>24JW1VB99T8MAU94TBIC</AccessKeyID>
	<SecretAccessKey>OTrwBXGVBacVdXNSI7SKKrX8b+CqwANa5ngLZ4lB</SecretAccessKey>
</S3>
```