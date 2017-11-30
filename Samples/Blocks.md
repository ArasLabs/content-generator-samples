# Sample: Block Elements

By default, BlockElements are simple containers that can contain any schema elements.

<!--## Create New Section

```(csharp)
BlockDocumentElement blockElement = (BlockDocumentElement) this.Factory.NewBlock("Section");
```
-->

## Create New External Content Block

```(csharp)
BlockDocumentElement blockElement = (BlockDocumentElement) this.Factory.NewBlock();

// set block reference
blockElement.SetExternalBlock("9D0639A0EA13403A9FEBC6007D2D7E89");
```

> Note: The method `SetExternalBlock` takes the id of another Technical Document as a parameter. If a user sets the reference, then the block type will is changed from *internal* to *external* and all existing content is replaced with content of the referenced block.