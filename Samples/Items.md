# Sample: Item Elements

## Create a New Item Element

```(csharp)
ItemDocumentElement itemElement = (ItemDocumentElement) this.Factory.NewElement("aras-part");

// get item from Innovator
Item itemItem = this.Factory.InnovatorInstance.newItem("Part", "get");
itemItem.setID("CD2B48A0C3C042898AC00254930FC8A1");
itemItem = itemItem.apply();

// set item reference
itemElement.SetItem(itemItem);
```