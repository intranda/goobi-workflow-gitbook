# goobi_exportXml.xml

The `goobi_exportXml.xml` file specifies technical details about the properties and associated XML namespaces used when generating docket files.

The file is usually located at the following location:

```bash
/opt/digiverso/goobi/config/goobi_exportXml.xml
```

For example, this configuration file looks as follows:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<config_exportXml>

	<namespace name="mets" value="http://www.loc.gov/METS/" />
	<namespace name="mods" value="http://www.loc.gov/mods/v3" />
	<namespace name="goobi" value="http://meta.goobi.org/v1.5.1/" />
	<namespace name="xlink" value="http://www.w3.org/1999/xlink" />
	<namespace name="dv" value="http://dfg-viewer.de/" />
	<namespace name="wt" value="http://wellcome.ac.uk/" />

	<mets>
		<property name="shelfmarksource" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='shelfmarksource']" />
		<property name="TitleDocMain" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='TitleDocMain']" />
		<property name="CorporateName" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='CorporateName']" />
		<property name="PublicationYear" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='PublicationYear']" />
	</mets>

	<!--
	<anchor>
		<property name="ManifestationType" value="//mets:mets/mets:dmdSec[1]/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi/goobi:metadata[@name='_ManifestationType']" />
	</anchor>
	-->

</config_exportXml>
```

## General

This configuration file is used to specify additional properties to be included when exporting docket files. Since these properties can be gathered from different areas, it is necessary to specify for each property where it is defined. This is done with the help of namespaces, which are also defined beforehand.

## Defining namespaces

The `<namespace>` elements are used to define namespaces that can be used to add further properties for exporting metadata. There are some projects and institutions that define such namespaces. In this configuration file, a `<namespace>` element is created for each required namespace definition.

Namespaces are identified by a name or abbreviation specified with the `name` parameter. This should be short and descriptive, as it will be used often later. Namespace names may not occur more than once. Usually the project name or an abbreviation of it is used. The project name is usually evident from the domain in the specified URL.

Accordingly, namespaces refer to a URL defined in the `value` parameter. This URL must point to an XML specification that contains further information about the respective namespace and the available property names. Further information can be found in the respective documentation for the namespace specifications.

For example, if the following namespace is defined,

```xml
<namespace name="mets" value="http://www.loc.gov/METS/" />
```

so an element `mets:xmlData` can be used later. Goobi can then assign that in the namespace `mets`, which in turn is defined in the specification under `http://www.loc.gov/METS/`, the element `xmlData` should be searched for. There it is defined according to the project.

## Define properties

Properties to be included in the export are specified in `<property>` elements. The title specified in the `name` parameter will be reused for the structure of the exported docket file. The `value` parameter contains one or more properties which are structured as follows.

### Syntax for properties

All properties are separated with slashes (`/`). Additionally, the entire entry starts with two slashes. The basic syntax is as follows:

```xml
value="//field1/field2/field3"
```

Since no default namespace can be defined in the list of namespaces, each property is assigned a namespace, resulting in the following syntax:

```xml
value="//namespace1:field1/namespace2:field2/namespace3:field3"
```

Any number of elements can be specified. Only namespaces that have been previously defined in the `<namespace>` elements can be used. According to the namespaces, only certain properties can be specified. For example, it looks like this:

```xml
value="//mets:mets/mets:mdWrap/mets:xmlData/mods:mods/mods:extension/goobi:goobi"
```

It may happen that properties exist as lists. In this case the number of the list element is indicated with square brackets. It should be noted that the count starts at 0. In the following example the second element from the list `dmdSec` is used. (The first element would then have the number 0).

```xml
mets:dmdSec[1]
```

In addition, for more complex properties, it is possible to select which component of the property should be used. In the following example, the sub-element with the property `name` = `PublicationYear` is selected from the `metadata` element.

```xml
goobi:metadata[@name='PublicationYear']
```

### meta.xml or meta_chanor.xml

If only a `meta.xml` is used to describe the process, all `<property>` elements are created inside a `<mets>` element.

If an additional `meta_anchor.xml` is used to describe the process, then all `<property>` elements are created within an `<anchor>` element.

For an export, only the `<property>` elements from one of the two elements are ever used.

If a `goobi_exportXml.xml` file is to be used for different projects, some of which use only the `meta.xml` and some of which also use the `meta_anchor.xml`, both elements can be specified with their respective `<property>` subelements without any problems. These do not influence each other.