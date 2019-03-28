# Content Generator Samples for Aras Tech Docs

This project contains samples for operations on different document elements, in the context of a Content Generator method.

## About Content Generators

Content Generators are server-side methods that populate a document element with content. The method executes when the associated document element is created.

## Samples

* [Tables](Samples/Tables.md)
* [Lists (and List Items)](Samples/Lists.md)
* [Text](Samples/Text.md)
* [Graphics (Images)](Samples/Graphics.md)
* [Items](Samples/Items.md)
* [Blocks](Samples/Blocks.md)

Here are some other examples:

* [Blog: Using Content Generators](https://community.aras.com/b/english/posts/using-content-generators-in-tech-docs)
* [Project: Custom Tech Docs](https://github.com/ArasLabs/custom-tech-docs)

## Tips

### 1. Reference the Content Generator Method Template

All content generator methods *must* begin with the following comment. This reference ensures that Aras Innovator uses the correct method template to execute your method code.

```(csharp)
//MethodTemplateName=CSharp:Aras.TDF.ContentGenerator(Strict);
```

### 2. Insert Content Into the Target Element

Every content generator has an element `targetElement` in its context. This is the element that is created by the Content Generator. Any content you want to add to the element being created needs to be added to this element.

#### Example 1:

This method is the default content generator for the ItemInfo element in the Standard schema. Since it is adding an Item element, the `targetElement` is cast as an ItemDocumentElement object to the `targetItem` variable. The method then builds a table of data and adds it to `targetItem` at the end. 

Without the final line (`targetItem.AddChild(tableElement);`) the ItemInfo element would not contain the table of data.
```(csharp)
//MethodTemplateName=CSharp:Aras.TDF.ContentGenerator(Strict);
ItemDocumentElement targetItem = targetElement as ItemDocumentElement;

if (targetItem != null) {
	targetItem.ClearChilds();

	// if referenced item was set, then
	if (!targetItem.IsEmpty)
	{
		TableDocumentElement tableElement = (TableDocumentElement) this.Factory.NewTable("Table", 3, 5);
		tableElement.GetCell(0, 0).AddChild(this.Factory.NewText("Title", "Item Info Table"));

		for (int i = 0; i < tableElement.CellCount; i++)
		{
			tableElement.MergeCells(0, i, MergeDirection.Right);
		}

		tableElement.GetCell(1, 0).AddChild(this.Factory.NewText("Title", "Id"));
		tableElement.GetCell(1, 1).AddChild(this.Factory.NewText("Title", "Name"));
		tableElement.GetCell(1, 2).AddChild(this.Factory.NewText("Title", "Classification"));
		tableElement.GetCell(1, 3).AddChild(this.Factory.NewText("Title", "Status"));
		tableElement.GetCell(1, 4).AddChild(this.Factory.NewText("Title", "Date of creation"));

		tableElement.GetCell(2, 0).AddChild(this.Factory.NewText("Title", targetItem.ItemId));
		tableElement.GetCell(2, 1).AddChild(this.Factory.NewText("Title", targetItem.GetItemProperty("name", " ")));
		tableElement.GetCell(2, 2).AddChild(this.Factory.NewText("Title", targetItem.GetItemProperty("classification", " ")));
		tableElement.GetCell(2, 3).AddChild(this.Factory.NewText("Title", targetItem.GetItemProperty("state", " ")));
		tableElement.GetCell(2, 4).AddChild(this.Factory.NewText("Title", targetItem.GetItemProperty("created_on")));

		targetItem.AddChild(tableElement);
	}
}
```

#### Example 2:

For more simple content generators, it is possible to add elements directly to `targetElement` instead of casting it to another object. This sample creates a text element and adds it to the `targetElement`.

```(csharp)
TextDocumentElement textElement = (TextDocumentElement) this.Factory.NewText("ptxt", "My very special content\n");

targetElement.AddChild(textElement);
```

> Note: The samples in this project do not include the step of adding elements to the `targetElement`, but it is necessary for your content to appear in the document element being created.

### 3. Get an Innovator Object

In most server-side methods you can use `this.getInnovator()` to get an Innovator object. However, content generators use a different method template (context), so we need to get the Innovator object with a different call.

```(csharp)
Innovator inn = this.Factory.InnovatorInstance;
```

### 4. Get the Current Document's ID

In most server-side methods you can use `this.getID()` to get the id of the current Item. However, content generators use a different method template (context), so we need to get the document id with a different call.

```(csharp)
string doc_id = executionContext.DocumentId;
```

### 5. Get the current document's content

You may want to add content to your new element based on other content in the document. (Ex: an auto-generated table of contents populated with section titles) To do so, you will need to retrieve that content and put it in a format you can consume.

```(csharp)
// get document id
string doc_id = executionContext.DocumentId;
Innovator inn = this.Factory.InnovatorInstance;

// get document content
Item doc_content = inn.newItem("tp_Block","tp_DocumentGet");
doc_content.setID(doc_id);
doc_content = doc_content.apply();

Item doc = doc_content;

// Load the results into an xml string
string docXml = doc.dom.InnerXml;

// Unescape the XML in the content property to make its content part of the main xml
docXml = docXml.Replace("&apos;", "'").Replace("&quot;", "\"").Replace("&gt;", ">").Replace("&lt;", "<").Replace("&amp;", "&");

// Handle namespace issues
docXml = docXml.Replace(" xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\"","").Replace(" xmlns:aras=\"http://aras.com/ArasTechDoc\"","").Replace(" xmlns=\"http://www.aras.com/TechDocExample\"","");

docXml = docXml.Replace("<SOAP-ENV:Envelope","<SOAP-ENV:Envelope xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\" xmlns:aras=\"http://aras.com/ArasTechDoc\"");

// load the xml string into an XmlDocument 
XmlDocument xmlDoc = new XmlDocument();
xmlDoc.LoadXml(docXml);

// you can now use xmlDoc.SelectNodes() or xmlDoc.SelectSingleNode() to find elements using XPath
```

> Note: This sample may not work with all releases of Aras Innovator that support the Technical Documentation application.
