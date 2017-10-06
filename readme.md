# Avro Schema Editor

The aim of this project is to provide a graphical Avro Schema editor based on Eclipse technologies. 

Visit the Apache Avro site [here](https://avro.apache.org)

The latest specifications of Avro Schema can be found [here](https://avro.apache.org/docs/1.8.2/spec.html).

This project focuses on the following points:

* graphical representation of an Avro schema 
* ergonomics
* performance
* customization

## Installation

This project is basically an Eclipse plugin.
The installation is quite simple:

* fetch the project
* build it (mvn clean install)
* launch an eclipse
* Select "Install New Softwares..." >> "Add repository" >> select the p2 repository generated by the build 'org.talend.avro.schema.editor.repository/target/repository'
* restart eclipse

The plugin defines an eclipse editor binded to text files with ".avsc" file extension.


## First Avro schema

To create your first Avro schema, right click in project explorer and select "New..." then "File", enter "sample.avsc" name and click on "Finish".


## Quick presentation of the editor

The Avro schema editor is divided in two parts, a left one displaying the schema in a tree viewer, and a right one displaying the attributes of the current selected element in the tree.

![](https://github.com/Talend/avro-schema-editor/raw/master/images/sample_1.png)

We use specific icons in order to distinguish the different types of element 
(e.g. orange icon for a record, green icon for enumeration, dark blue icon for fields, light blue for opional fields, and so on).

The tree label display the name of the elements and their type between brackets 
(e.g. for record element we display "record" and for fields we usualy display the name of the primitive type).

The schema tree provides a maximum of legible information, but not all the information,
it is why we have the right part displaying all the information of a selected element.

The attribute viewer displays obviously the standard avro attributes (namespace, name, doc, and so on).
It displays customized attributes and sometime editing features (as the 'optional' button which allows to set a field as optional).

## Editing features

The use of a tree viewer provides all the standard interactions: selection, drag and drop and so on.

We have access to editing features by three ways:

1. a bottom toolbar ![](https://github.com/Talend/avro-schema-editor/raw/master/images/bottom_toolbar.png) provides the main editing features: add a new element, remove selected elements, move up or down selected elements, make a copy and paste it.

2. a richt click on the tree open a popup menu providing the same editing features

3. we can also performs drag and drop of a selected element. The result depends on the kind of the selected and target elements:
	* for a field, drag and drop allows us to reorder the fields of a record, or to make a copy of a field
	* for a record, drag and drop offers three options:
		* we can move the selected record onto a new place in the schema
		* we can make a copy of this record
		* we can make a reference on this record. This allows to change the type of the target field. Of course the ref record is exactly the same as the original record.
		If we edit the original record, the ref record we be automatically updated to take account of the changes.

All the editing features are undoable.

## Advanced features

To be defined

## Full example

You can see below an example of a complex schema using all the kind of Avro elements.

![](https://github.com/Talend/avro-schema-editor/raw/master/images/figure.png)


You can see below the corresponding figure.avsc file. 

    {
    	"type": "record",
    	"name": "Figure",
    	"namespace": "org.example.com",
    	"fields": [{
    		"name": "name",
    		"type": "string"
    	},
    	{
    		"name": "identifier",
    		"type": "long"
    	},
    	{
    		"name": "date_of_creation",
    		"type": ["null",
    		"long",
    		"string"],
    		"doc": "Can be defined in two ways: a long (which represents the number of milliseconds since January 1, 1970, 00:00:00 GMT) or a string (DD-MM-YYY format)"
    	},
    	{
    		"name": "origin",
    		"type": {
    			"type": "record",
    			"name": "Point",
    			"fields": [{
    				"name": "x",
    				"type": "float"
    			},
    			{
    				"name": "y",
    				"type": "float"
    			}]
    		}
    	},
    	{
    		"name": "shapes",
    		"type": {
    			"type": "array",
    			"items": {
    				"type": "record",
    				"name": "Shape",
    				"doc": "Define a shape.",
    				"fields": [{
    					"name": "name",
    					"type": ["null",
    					"string"]
    				},
    				{
    					"name": "type",
    					"type": [{
    						"type": "enum",
    						"name": "ShapeType",
    						"symbols": ["Circle",
    						"Triangle",
    						"Cross",
    						"Square"]
    					},
    					"string"],
    					"doc": "The type of the shape."
    				},
    				{
    					"name": "anchor",
    					"type": "Point"
    				},
    				{
    					"name": "width",
    					"type": "float"
    				},
    				{
    					"name": "height",
    					"type": "float"
    				},
    				{
    					"name": "angle",
    					"type": ["null",
    					"float"]
    				},
    				{
    					"name": "color",
    					"type": {
    						"type": "record",
    						"name": "Color",
    						"fields": [{
    							"name": "red",
    							"type": "int"
    						},
    						{
    							"name": "green",
    							"type": "int"
    						},
    						{
    							"name": "blue",
    							"type": "int"
    						},
    						{
    							"name": "alpha",
    							"type": ["null",
    							"int"]
    						}]
    					}
    				},
    				{
    					"name": "properties",
    					"type": ["null",
    					{
    						"type": "map",
    						"values": "string"
    					}]
    				}]
    			}
    		},
    		"doc": "List of shapes defining the figure."
    	}]
    }

## Customization

To be defined

## Contributing

We welcome contributions of all kinds from anyone.

## License

Copyright (c) 2006-2017 Talend

Licensed under the [Apache Licence v2](https://www.apache.org/licenses/LICENSE-2.0.txt)
