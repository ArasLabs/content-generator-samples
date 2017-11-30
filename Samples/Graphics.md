# Sample: Graphic Elements

## Create a New Graphic from tp_Image

```(csharp)
ImageDocumentElement imageElement = (ImageDocumentElement) this.Factory.NewElement("graphic");

// get tp_Image item from Innovator
Item imageItem = this.Factory.InnovatorInstance.newItem("tp_Image", "get");
imageItem.setID("70CA6215D95C4658ACA68BFDB73E4DEE");
imageItem = imageItem.apply();

// set reference on image item
imageElement.SetImage(imageItem);
``` 