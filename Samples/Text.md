# Sample: Text Elements

## Create a New Text Element

Create an empty Text element:
```(csharp)
TextDocumentElement textElement = (TextDocumentElement) this.Factory.NewText();

/* OR */

TextDocumentElement textElement = (TextDocumentElement) this.Factory.NewText("ptxt");
```

Create a Text element with content:
```(csharp)
TextDocumentElement textElement = (TextDocumentElement) this.Factory.NewText("ptxt", "Initial Text!\n");
```

> Note: Factory method NewText() takes a second parameter for initialText value, but this parameter can be skipped.

## String Elements

TextElement contains StringElements as child elements. Separate StringElement can be obtained with indexer property Strings:
```(csharp)
StringDocumentElement stringElement = textElement.Strings[1];
```

Number of strings in TextElement user can get using StringCount property.
```(csharp)
int num_strings = textElement.StringCount;
```

## Add a New String to a Text Element

Replace all existing strings with a new one:
```(csharp)
textElement.Text = "Hello, World!\n";
```

> Note: Property `Text` returns concatenated content of all strings of the TextElement. If the property is used as a setter, then all current strings will be replaced by a new one.

Add new string with **bold** style:
```(csharp)
textElement.AddString("How are you, World?\n", "bold");
```

## Style Strings in Text Element

Set style for second string:
```(csharp)
textElement.Strings[1].SetStyle("italic bold under strike");
```

Set style for substring:
```(csharp)
textElement.Strings[2].SetStyle("sub", 3, 7);
```

> Note: The method `SetStyle` on StringElement takes a textStyle string as a parameter. It contains desired styles, which are split with the 'space' character. Additionally, the `SetStyle` method can take `startRange` and `endRange` parameters. In this case, the string will split on substrings and total number of strings in TextElement will increase.

## Set Link to Another Element

Set link on element of another document (root element in this case):
```(csharp)
textElement.Strings[4].SetLink("1D93C56E1EBA4F6A9B68D348444C9C17", "1D93C56E1EBA4F6A9B68D348444C9C17");
```

> Note: The method `SetLink` takes `targetBlockId` (id of existing Technical Document) and `targetElementId` (id of any element in the Document). 

## Remove Link to Another Element

Remove link:
```(csharp)
textElement.Strings[4].RemoveLink();
```