# OpenXMLEditor-Java



A web browser based XML editor. It provides a general use graphical tool for creating new or modifying existing XML documents in your web browser. Information is extracted from an XML schema (XSD file) to provide the user with information about what elements, sub elements and attributes are available at different points in the structure, and a GUI based means of adding or removing them from the document.
Additionally, this project includes a tool for generating JSON objects from XML schemas, which can either be directly used in browsers or precompiled (see xsd/xsd2json.js).
Browser support
The editor should work in current versions of Chrome, Firefox, Safari, Opera, and IE9-10. Performance will vary. IE7-8 are mostly functional, although not all features work.

**Features**

•	Graphical editor mode for displaying and modifying XML elements

•	Text editor mode for directly modifying the underlying document (using the Cloud9 editor)

•	Contextual, schema driven menus for adding new elements, sub elements and attributes in both the graphical and text editing modes

•	Fully javascript and CSS based, jquery widget

•	AJAX submission of document modifications

•	Export the document to a file in web browsers that support it

•	Keyboard shortcuts for navigation and other operations

•	Standalone tool for building JSON representations of XML schemas (see the xsd/ folder in this project)

**How to use**

**Installing**

•	(Manual Way) Download the package and include the file open xml file.js after jQuery in the head of your web page.

•	Alternatively projects using bower can install it from the bower registry: bower install open xml editor
Locating schema files
Due to restrictions web browsers have on cross domain requests in javascript, all necessary XSD files must be located in the same domain as the page the editor is embedded in.
But rather than lugging the XSD files around everywhere, you can precompile a JSON representation of your schemas to include instead.
It'll also save your users some loading time.

**Embedding the editor**

<div id="xml_editor">&lt;rootElement&gt;&lt;/rootElement&gt;</div>
<script>
  $(function() {
        $("#xml_editor").xmlEditor({
        schema: schema
    });
  });
</script>

**Start-up options for open xml editor**

**Schema**

The editor must be provided with an XML schema via the schema parameter, which can be provided in two ways:

1) Directly from an Xsd2Json object, extracted at runtime. 

     $(function() {
          var extractor = new Xsd2Json("mods-3-4.xsd", {"schemaURI":"mods-3-4/", "rootElement": "mods"});
         $("#mods_editor").xmlEditor({
              schema: extractor.getSchema()
         });
    });
    
2) URL to a precomputed JSON file, generated by the Xsd2Json plugin

    $("#xml_editor").xmlEditor({
      schema : "demo/examples/mods.json"
    });
    
**Initial document**

**Embedded document**

The editor can be initialized on an existing textarea element. If so, the contents of the text area will be extracted to populate the starting document. 
Alternatively, if the editor is initialized on a div element, the starting document should be XML escaped text inside the div:
If it is not escaped, the contents will still be used, but can result in parsing issues since the browser's DOM parser will process it first.

**Remote document**

**To retrieve the starting document from a remote location use:**

•	ajaxOptions

    o	xmlRetrievalPath - URL to retrieve the starting XML document from
    o	xmlRetrievalParams - Any additional parameters to submit in the retrieval request
    
**Submission configuration**


**Configure the standard**

•	ajaxOptions - Used for communicating with a remote source for receiving and/or submitting documents. It is an object containing the following properties:
   
    o	xmlUploadPath - URL where the current document will be uploaded when submitting. If not set, then an "Export" button will be shown instead.
    o	xmlRetrievalPath - URL to retrieve the starting XML document from
    o	xmlRetrievalParams - Any additional parameters to submit in the retrieval request

•	submitResponseHandler - Function called after the document is submitted when there is no HTTP error. Passed AJAX response object as parameter. Return true if the upload was considered to be successful.

**Submit buttons**

There are two ways to configure buttons which show up in the status

xmlUploadPath

Default, single upload button. By providing an xmlUploadPath option, a "Submit Changes" button will appear.

    {
      ajaxOptions : {
        xmlUploadPath : "/submit"
      },
      submitResponseHandler : myResponseHandler
     }

An additional submitResponseHandler function can also be provided:

•	submitResponseHandler - Function called after the document is submitted when there is no HTTP error. Passed AJAX response object as parameter. Return true if the upload was considered to be successful.
Custom errorHandler

You can specify a custom error handler function if you need something specific for your situation.

     {
       $("#xml_editor").xmlEditor({
         submitErrorHandler : function(jqXHR, exception) {
          // my custom error handling code here
         };
        });
     }

**submitButtonConfigs**

Alternatively, any number of buttons can be created by providing the submitButtonConfigs option. It expects an array containing button configuration objects, each of which can contain the following options:

•	url - URL where the document will be sent to via POST. Optional. If not provided, then the document is not uploaded, but the submit function is still called.

•	responseHandler - Function called after the document is submitted when there is no HTTP error. Passed AJAX response object as parameter. Return true if the upload was considered to be successful. Optional.


•	errorHandler - Function called when the upload the upload to the server results in an HTTP error response code. Optional.

•	onSubmit - Function called after clicking the button, before upload. Passed the config object, called with the context of the editor object.

•	createDomElement - Whether or not to create a new button element. Set to false if using an existing element. Default: true.

•	label - Text displayed on the button. Default: "Submit Changes"

•	id - id attribute value of the button created.

•	cssClass - class attribute added to the button created

•	disabled - If true, then button will start off disabled.

     {
       submitButtonConfigs : [
         {
          url : "/submit",
          responseHandler : myResponseHandler,
           label : "Upload"
         },
        {
           label : "Download",
           onSubmit : function() {
            // do work
          }
        }
      ]
     }
Providing a submitButtonConfigs option will override the creation of the standard submit/export button.

**Other editor configuration**

•	documentTitle - Title for the document being edited, which is displayed at the top of the editor.

•	elementUpdated - An optional event function which is triggered whenever an XML element is updated or rendered. It is triggered in the context of the element object modified, and includes an event object indicating which event took place and any additional information.

•	menuEntries - A list of additional entries to add to the top menu bar, such as adding new help entries.

•	confirmExitWhenUnsubmitted - Causes web browsers to prompt users if they try to navigate away from the editor while there are unsubmitted changes. Valid values: True or false.

•	undoHistorySize - The number of history states remembered by the undo/redo feature. Default is 20.

**License Information**

Copyright (c) 2016, University of South Africa and/or its affiliates. All rights reserved.
DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
This code is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License version 2 only, as published by the Free Software Foundation.
This code is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License version 2 for more details (a copy is included in the LICENSE file that accompanied this code).

You should have received a copy of the GNU General Public License version 2 along with this work; if not, write to the Free Software Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.

**Authors**

Benedict M Pabazhira

Isaac Motale Mbaka



