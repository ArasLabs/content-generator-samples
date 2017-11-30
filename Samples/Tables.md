# Sample: Table Elements

This document contains sample code for creating and manipulating Table elements in a Content Generator method.

## Create a Table Element

Create a new Table element:
```(csharp)
TableDocumentElement tableElement = (TableDocumentElement) this.Factory.NewTable();

/* OR */

// pass the name of the schema element you want to create
TableDocumentElement tableElement = (TableDocumentElement) this.Factory.NewTable("table");
```

> Note: If the schema element name is not passed in the NewTable constructor, the first appropriate schema element will be used.

Create a Table element with 4 rows and 4 columns
```(csharp)
TableDocumentElement tableElement = (TableDocumentElement) this.Factory.NewTable("table", 4, 4);
```

> Note: If the rowCount and columnCount parameters are not passed, the table will be created with the default 2 rows and 2 columns.


## Add a New Row

Add a new row to the end of the Table:
```(csharp)
tableElement.AddRow();
```

Add a new row to the beginning of the table:
```(csharp)
tableElement.AddRow(0);
```

Add a row at any index:
```(csharp)
// insert new third row
tableElement.AddRow(2);
```

## Delete a Row

Delete the last row:
```(csharp)
tableElement.RemoveRow(tableElement.RowCount - 1);
```

Delete any row by index:
```(csharp)
// delete the third row
tableElement.RemoveRow(2);
```

## Add a New Column

Add a new column to the end of the Table:
```(csharp)
tableElement.AddColumn();
```

Add a new column to the beginning of the Table:
```(csharp)
tableElement.AddColumn(0);
```

Add a new column at any index:
```(csharp)
// add a new column before the second column
tableElement.AddColumn(1);
```

## Delete a Column

Remove the last column:
```(csharp)
tableElement.RemoveColumn();
```

Remove the first column:
```(csharp)
tableElement.RemoveColumn(0);
```

Remove the column at any index:
```(csharp)
// remove the third column
tableElement.RemoveColumn(2);
```

## Merge Cells

MergeCells() Method:
```(csharp)
tableElement.MergeCells(rowIndex,colIndex,mergeDirection);
```

MergeDirection Enumeration:

Use the merge direction name or corresponding integer for the mergeDirection parameter.
* MergeDirection.Up (0)
* MergeDirection.Right (1)
* MergeDirection.Down (2)
* MergeDirection.Left (3)

Merge the first cell to the right:
```(csharp)
tableElement.MergeCells(0, 0, MergeDirection.Right);
```


Merge the third cell in the second row to the left, twice:
```(csharp)
tableElement.MergeCells(1, 2, MergeDirection.Left);
tableElement.MergeCells(1, 2, 3);
```

Merge last cell in second row with cell below, twice
```(csharp)
tableElement.MergeCells(1, 3, MergeDirection.Down);
tableElement.MergeCells(1, 3, 2);
```

## Unmerge Cells

UnmergeCells() Method:
```(csharp)
tableElement.UnmergeCells(rowIndex,colIndex);
```

Unmerge first cell:
```(csharp)
tableElement.UnmergeCells(0, 0);
```