# goobi_processProperties.xml

In the configuration file `goobi_processProperties.xml` further properties for projects, processes and steps can be specified. The file is usually located at the following memory path:

```bash
/opt/digiverso/goobi/config/goobi_processProperties.xml
```

For example, this configuration file looks like this:

{% code title="goobi_processProperties.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<config_processProperties>
	<property name="Example" container="0">
		<project>Project 1</project>
		<project>Project 2</project>
		<workflow>Workflow 1</workflow>
		<workflow>Workflow 2</workflow>
		<showStep name="Scanning" access="READ" duplicate="" />
		<showStep name="Check resolution" access="WRITE" duplicate="" />
		<showProcessCreation template="*" access="write">
          <display property="Resolution" value="undefined" />
        </showProcessCreation>
		<showProcessGroup access="write" />
		<validation>\w</validation>
		<type>LIST</type>
		<defaultvalue>Please select...</defaultvalue>
		<value>Value 1</value>
		<value>Value 2</value>
	</property>
</config_processProperties>
```
{% endcode %}

## General

With each `<property>` element a property is defined. This can be configured to apply to one or more projects, one or more tasks, or one or more steps. Combinations are also possible. Instead of a project name, task title or step title, an asterisk (`*`) can be used to address all projects, tasks or steps.

For each `<property>` a name is specified with the `name` parameter, this should be unique and meaningful.

For each `<property>` a container is specified with the parameter `container`, in which the defined property should be internally classified.

## Available configurations

The following tags are available as subelements for the `<property>` tag:

| Tag                  | Usable multiple times      | Description |
| -------------------- | -------------------------- | ------------------------------------------ |
| `<project>`          | yes                        | This element can be used to specify one or more projects for which the property should apply. Alternatively, an asterisk (`*`) can be used to address all projects. |
| `<workflow>`         | yes                        | This element can be used to specify one or more process templates to which the property should apply. Alternatively, an asterisk (`*`) can be used to display the property inside of all process templates. |
| `<showStep>`         | yes                        | This element specifies that a single step is displayed in the user interface. The `name` parameter is used to specify the step title. The `access` parameter is used to specify an access right, see below. The `duplicate` parameter specifies whether steps may appear more than once. |
| `<showProcessCreation>`| ja                      | This element can be used to define that the property is displayed in the process creation screen. |
| `<showProcessGroup>` | no                         | In this element, the `access` parameter defines an access right for groups of processes. For details, see below. |
| `<validation>`       | no                         | This element can be used to specify parameters for a validation. |
| `<type>`             | no                         | This element specifies the data type of this property. For supported data types, see below. |
| `<defaultvalue>`     | no                         | This element specifies the default value of an input field or selection. |
| `<value>`            | in lists yes, otherwise no | For simple input field types, this element specifies a predefined value. For lists, multiple `<value>` elements specify a list of selectable entries. |

### Available access rights

<!--- Note for developers: The access rights are defined in the enum org.goobi.production.properties.AccessCondition. -->

All access rights can be written in any capitalization, this will be ignored when reading.

If no value is specified or it is written incorrectly, `READ` is the default value.

| Access right    | Description                                     |
| --------------- | ------------------------------------------------- |
| `READ`          | The property can be accessed in read-only mode. |
| `WRITE`         | The property can be accessed in write mode.  |
| `WRITEREQUIRED` | The property must be set individually.   |

### Available data types

<!--- Note for developers: The data types are defined in the enum org.goobi.production.properties.Type. -->

All data types can be written in any capitalization, this will be ignored when reading.

If no value is specified or it is written incorrectly, `TEXT` is the default value.

| Data type         | Description |
| ----------------- | ----------- |
| `BOOLEAN`         | A boolean value can be specified. Valid values are `true` and `false`. |
| `DATE`            | A date can be selected. |
| `HTML`            | An HTML coded text can be used. Depending on the used internet browser all common HTML tags are supported. |
| `LINK`            | A URL can be used. This should exist and be freely accessible. |
| `LIST`            | An element can be selected from a list of choices. |
| `LISTMULTISELECT` | Any number of elements can be selected from a list of choices. |
| `METADATA`        | Additional metadata can be specified. |
| `NUMBER`          | A number can be specified. |
| `TEXT`            | Any text can be used. This text does not support HTML. |

For the `LIST` and `LISTMULTISELECT` datatypes, a text such as `Please select` or one of the specified values can be specified as the default value with the `<defaultvalue>` tag. If the field is required, one of the specified values must be selected later, even if the value in `<defaultvalue>` differs.

## Special features for processes

There are two cases where the properties defined in this file are queried. Either information about processes or about steps is queried.

In the case of a process, not all sub-elements are used. Only the elements shown in the following example are observed:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config_processProperties>
	<property name="Example" container="0">
		<project>Project 1</project>
		<project>Project 2</project>
		<showProcessGroup access="write" />
		<validation>\w</validation>
		<type>LIST</type>
		<defaultvalue>Please select...</defaultvalue>
		<value>Value 1</value>
		<value>Value 2</value>
	</property>
</config_processProperties>
```

The `<workflow>` and `<showStep>` elements are not used for processes.

## Conditional display of properties

Properties can also be displayed conditionally. To do this, you can define that another property must have a certain value in order to control the display. The following example illustrates this:

```xml
	<property name="Resolution" container="Images">
        <project>*</project>
        <showProcessCreation template="*" access="writeRequired"/>
        <type>List</type>
        <value>300</value>
        <value>400</value>
        <value>600</value>
        <value>Other</value>
    </property>
    <property name="Special Resolution" container="Images">
        <project>*</project>
        <showProcessCreation template="*" access="write">
        	<display property="Resolution" value="Other" />
        </showProcessCreation>
		<showStep name="Scanning preparation" access="write">
		    <display property="Resolution" value="Other" />
		</showStep>
        <type>Text</type>
    </property>
```

The `Special Resolution` property is only displayed here both in the creation screen and in the `Scanning preparation` task if the value `Other` has been selected from the list in the `Resolution` property. If a different value is selected in the `Resolution` property, the `Special Resolution` text field is not visible.