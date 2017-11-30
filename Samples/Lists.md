# Sample: List Elements

## Create a New List

Create a new empty List:
```(csharp)
ListDocumentElement listElement = (ListDocumentElement) this.Factory.NewList();

/* OR */

ListDocumentElement listElement = (ListDocumentElement) this.Factory.NewList("list1");
```

> Note: If the schema element name is not passed in the NewList constructor, the first appropriate schema element will be used.

Create a new List with three list items:
```(csharp)
ListDocumentElement listElement = (ListDocumentElement) this.Factory.NewList("list1", 3);
```

> Note: If the itemCount parameter is not passed, the list will be created with no child elements.

## Add a New Item to the List

Add a new list item at the end:
```(csharp)
listElement.AddItem();
```

Insert a new list item at the beginning:
```(csharp)
listElement.AddItem(0);
```

Insert a new list item at any index:
```(csharp)
// add a new second list item
listElement.AddItem(1);
```

Add a new list item that contains a text element:
```(csharp)
// get the length of the list 
int new_item_index = listElement.Items.Count;

// add an empty list item to the end of the list
listElement.AddChild();

// create a new text element with the text you want
TextDocumentElement textElement = (TextDocumentElement) this.Factory.NewText("Text", "Initial Text!");

// add the text element to the new empty list item we created 
listElement.Items[new_item_index].AddChild(textElement);
```

## Remove an Item from the List

Remove the last list item:
```(csharp)
listElement.RemoveItem();
```

Remove the first list item:
```(csharp)
listElement.RemoveItem(0);
```

Remove the list item at any index:
```(csharp)
// remove the third list item
listElement.RemoveItem(2);
```

## Set the List Style

The property ListType can take one of these enumeration values:
* ListTypes.Bullet
* ListTypes.Numeric
* ListTypes.Alpha

Set the list style to numeric:
```(csharp)
listElement.ListType = ListTypes.Numeric;
```