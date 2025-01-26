# EVA - Product setup and management
EVA, short for Elastic Versatile Architecture, is an eCommerce system created by New Black to make shopping easier and more seamless for you, your business, and your customers. It helps you connect all your sales channels, ***such as online stores, physical shops, and mobile apps***, into one system, so you can keep up with modern shopping trends and deliver a smooth, consistent experience to your customers.

This document describes how you can migrate your product information into EVA. All product migration can be done using JSON format. For further context and information concerning the use of EVA, please refer to our User Manual. 

**Level of EVA expertise needed to use this document** - A basic understanding 2/5

It is necessary to have a basic understanding of EVA features and elements to use this document effectively.

**Covered in this document**

- Product setup
  - Single product upload
  - Product types
  - Product hierarchy
  - Editing products
  - Deleting products
  - Barcodes

- Product content
  - Images
  - Languages
  - Native content options
  - USP text and USP blobs

- Properties
  - Creating product properties
  - Display values for customer properties
  - Product property categories
  - Additional services
  - Defining values in ImportProducts
  - Creating product properties in ImportProducts
  - Copying properties to parents
  - Including content of children to parents/siblings

- Error handling - Failure responses
  - Partial failure
  - Unknown tax code
  - Validation failure

## Product setup

### Single product upload

A simple, single product upload through `ImportProducts`can be managed using the following configuration script: 

```json 
{ 
  "SystemID": "InsomniaImport", 
  "Products": [ 
    { 
      "ID": "0001", 
      "Name": "Unisex T-shirt", 
      "TaxCode": "High" 
    } 
  ] 
}
```

In the example above, we create a product called "Unisex T-shirt" with a SystemID/BackendID (ID) and a TaxCode. The SystemID is used to identify the system from which the product is being imported.

In addition to the SystemID, we provide a unique identifier in the ID field, which can be customized for each product. If you don't specify a CustomID, the BackendID will be used as the default identifier.

#### Response 

Every product will be assigned an EvaID upon creation. The response will include the EVA IDs, grouped by whether the products were updated or created. When products are created, they are also considered updated. Additionally, we will return a mapping of BackendID to EvaID.

```json 
{ 
  "UpdatedProductIDs": [1], 
  "CreatedProductIDs": [1], 
  "ProductMap": [ 
    { 
      "BackendID": "0001", 
      "ID": 1 
    } 
  ] 
} 
```
> **Note:** Products with different `BackendIDs` can have the same `CustomID`. For example, the latter can replace the first as a successor.

### Product types 

A product can have several types: 

To describe your product as being one or more of these types, we use the `Type` object: 

```json 
{ 
  "SystemID": "PimCore", 
  "Products": [ 
    { 
      "ID": "121", 
      "Name": "NewBorn T-Shirt", 
      "TaxCode": "High", 
      "Type": { 
        "Stock": true 
      } 
    } 
  ] 
} 
```
### Product hierarchy 

Product hierarchy is defined by the `Variations` property. This in turn contains a new `Products` property where every product should contain a value for the variation. The following request contains a product with four sizes: 

```json
{
  "SystemID": "PimCore",
  "Products": [
    {
      "ID": "121",
      "Name": "NewBorn T-shirt",
      "TaxCode": "High",
      "Variations": {
        "Property": "size",
        "LogicalLevel": "size",
        "Products": [
          {
            "ID": "121-978020137957",
            "Name": "NewBorn T-shirt",
            "VariationValues": [
              {
                "Value": "3-6 months"
              }
            ]
          },
          {
            "ID": "121-978020137958",
            "Name": "NewBorn T-shirt",
            "VariationValues": [
              {
                "Value": "6-12 months"
              }
            ]
          },
          {
            "ID": "121-978020137959",
            "Name": "NewBorn T-shirt",
            "VariationValues": [
              {
                "Value": "12-18 months"
              }
            ]
          },
          {
            "ID": "121-978020137960",
            "Name": "NewBorn T-shirt",
            "VariationValues": [
              {
                "Value": "18-24 months"
              }
            ]
          }
        ]
      }
    }
  ]
}
```
>**Note:** Both `color` and `size` are NOT native EVA product properties. These have to be created before they can be used. See [Custom product properties](/link). 

### Editing products 

To edit products, just use the same request and alter the information. EVA will know to update the product if the specified `ID` is already in use. 

### Deleting products 

To delete products, use the same request but include the "IsDeleted": true property for each product. Once set to true, the products will be marked as deleted. It's important to note that while the products are deleted, they remain in EVA with a status of Deleted, and will no longer be visible on the front end.

### Barcodes 

To add a barcode to a product, use the **Barcodes** element. You can also specify a **Barcode** (and its **Quantity**) for an existing [unit of measure](link) in the call to allow for easy scanning. 

```json 
<Tabs>
  <TabItem value="json1" label="Adding Barcodes">
    <pre>
      {
        "SystemID": "PimCore",
        "Products": [
          {
            "ID": "121",
            "Name": "NewBorn T-Shirt",
            "TaxCode": "High",
            "Barcodes": [
              "978020137957"
            ]
          }
        ]
      }
    </pre>
  </TabItem>
</Tabs>
```
```json 
<Tabs>
  <TabItem value="json2" label="Adding UOM Barcodes">
    <pre>
      {
        "SystemID": "PimCore",
        "Products": [
          {
            "ID": "121",
            "Name": "NewBorn T-Shirt",
            "TaxCode": "High",
            "Barcodes": [
              "978020137957"
            ],
            "UnitBarcodes": [
              {
                "Barcode": "4566569787",
                "Quantity": "48",
                "UnitOfMeasureID": "5"
              }
            ]
          }
        ]
      }
    </pre>
  </TabItem>
</Tabs>
```

## Product content
Product content can be included in the 'ImportProducts' service using the 'Content' array at the product level.

### Images 

In the example below, we associate an image with a product. This is illustrated using a simple product, the "Unisex T-shirt," with a basic image URL provided:

```json
{
  "SystemID": "InsomniaImport",
  "Products": [
    {
      "ID": "1",
      "Name": "Unisex T-shirt",
      "TaxCode": "High",
      "Content": [
        {
          "Images": [
            {
              "ImageUrl": "https://picsum.photos/200"
            }
          ]
        }
      ]
    }
  ]
}
```

### Languages 

Note that the Content property in the example request below is an array. This allows you to add content for multiple languages.

The Content array enables you to define content for different languages by specifying a LanguageID.

In the example below, the product has a short description in Dutch ("nl").

```json  
{
  "SystemID": "InsomniaImport",
  "Products": [
    {
      "ID": "1",
      "Name": "Unisex T-shirt",
      "TaxCode": "High",
      "Content": [
        {
          "LanguageID": "nl",
          "ShortDescription": "Unisex heavyweight t-shirt met geborduurd Nerd logo."
        }
      ]
    }
  ]
}
```

### Native content options 
EVA can ship native product properties which have functionalities at the front-end. If you are looking for possibilities beyond our native options though, see[Custome product properties] (/link).

### USP text and USP blobs 

By using the UniqueSellingPointTexts and UniqueSellingPointBlobIDs, you can display product information directly in the **POS** and **Companion App** search results by providing the corresponding values to these properties.

Here’s an example using the NewBorn T-Shirt:

```json
{
  "SystemID": "PimCore",
  "Products": [
    {
      "ID": "121",
      "Name": "NewBorn T-Shirt",
      "TaxCode": "High",
      "Content": [
        {
          "LanguageID": "nl",
          "ShortDescription": "NewBorn t-shirt voor de kleintjes.",
          "Images": [
            {
              "ImageUrl": "https://i.ibb.co/tDVGybm/newborn-logo.jpg"
            }
          ],
          "UniqueSellingPointTexts": [
            "Green choice",
            "Vegan"
          ],
          "UniqueSellingPointBlobIDs": [
            "290c4a1e-3ac0-4d69-b7d2-c622a55352e2",
            "62cc81df-c975-48de-bba4-0ddf0e85cead"
          ]
        }
      ]
    }
  ]
}
```

>**Important Note**: The order of the text and blob IDs is significant. In this example, "Green choice" will link to the first BlobID, and "Vegan" will link to the second. For managing BlobIDs, refer to the Blob Management.

## Product properties 
The `ImportProducts` service can be used to fill custom product properties that already exist in EVA. It is also possible to fill properties that do not yet exist, if you define these properties at root level first.

Here is a breakdown of each property: 

| Property          | Description                                                        |
|-------------------|--------------------------------------------------------------------|
| **ID**            | This is the product ID.                                            |
| **TaxCode**       | Give the correct [tax code](/link) for your product.               |
| **LanguageID**    | The ID of the language in which the product description is displayed. |
| **ShortDescription** | A brief description of your product.                             |
| **ImageURL**      | The URL to your product image. 

### Creating product properties 

To create a custom product property, use [CreateProductPropertyType](/link): 

```json
{
  "TypeID": "eu_ecolabel",
  "CategoryID": "default",
  "DataType": 3
}
```

This service works similarly to our CustomField services, with the exception of the TypeID and CategoryID fields.

### Display values for custom properties 

In order to give your properties custom names to be displayed in front ends, use [EditProductPropertyType]( /link): 

```json
{
  "ID": "eu_ecolabel",
  "Edits": [
    {
      "LayerID": 1,
      "Content": {
        "display_name": "European economy label"
      }
    }
  ]
}
```
Here, `LayerID` represents your contentlayer ID.

### Product property categories
You can manage product property categories with the following services:
- [CreateProductPropertyCategory]
- [EditProductPropertyCategory]
- [ListProductPropertyCategory]

>**Note:** Product property categories can't be deleted.

### Additional services
The following services are available for managing product property types:
- [SearchProductPropertyType]
- [DeleteProductPropertyType]
- [ListProductPropertyType]

### Defining values in ImportProducts
To add values to the custom product property, we use the `Content` object in `ImportProducts`: 

```json
{
  "SystemID": "PimCore",
  "Products": [
    {
      "ID": "121",
      "Name": "NewBorn T-Shirt",
      "TaxCode": "High",
      "Content": [
        {
          "CustomContent": {
            "eu_ecolabel": true
          }
        }
      ]
    }
  ]
}
```
Since our custom product property is a simple boolean, this case is straightforward.

>**Note**: As these product properties are part of the content object, they can have different values for each language.

### Creating product properties in ImportProducts
If you don't have your property preconfigured, you can provide it in the `ImportProducts` message: 

```json 
{
  "SystemID": "PimCore",
  "CustomPropertyTypes": [
    {
      "ProductPropertyTypeID": "eu_ecolabel",
      "CategoryID": "default",
      "DataType": 3
    }
  ],
  "Products": [
    {
      "ID": "121",
      "Name": "NewBorn T-Shirt",
      "TaxCode": "High",
      "Content": [
        {
          "CustomContent": {
            "eu_ecolabel": true
          }
        }
      ]
    }
  ]
}
```

On receipt of this message, the product property will be known in EVA and the correct value will be set on the product.

### Copying properties to parents 

On an e-commerce site overview page, you typically want to display color or style-level products instead of size-level products. However, you might want to provide filters on available colors and sizes. This data is often not present at the style or color level unless explicitly provided. 

Using the `ProductPropertyType` called `CopyToParentProductPropertyTypeID`you can refer to the ID of another property whose value will be copied to its parent. 

#### Example Usage

For instance, if a size-level product is available in "S", "M", and "L", setting `CopyToParentProductPropertyTypeID` on the size property to `available_sizes` ensures that these values are copied to the parent (color-level) and grandparent (style-level) products under the `available_sizes` property.

You can doe this through ImportProducts:

```json
{
  "CustomPropertyTypes": [
    {
      "ProductPropertyTypeID": "size",
      "CopyToParentProductPropertyTypeID": "available_sizes",
      "DataType": 0,
      "IndexType": 0,
      "IsArray": false
    },
    {
      "ProductPropertyTypeID": "color",
      "CopyToParentProductPropertyTypeID": "available_colors",
      "DataType": 0,
      "IndexType": 0,
      "IsArray": false
    }
  ]
}
```

This configuration automatically copies all distinct size values to their respective parents under `available_sizes`, as well as color. 

Example Response From `SearchProducts`: 

```json
{
  "product_id": 164,
  "available_colors": [
    "blue",
    "red"
  ],
  "available_sizes": [
    "S",
    "M",
    "XL",
    "XS"
  ]
}
```

>**Note:** Changing the value of `CopyToParentProductPropertyTypeID` for an existing property type affects ONLY products provided in the same request. To apply changes to all products, use the `ComposeProducts` service for a full recompose.

### Including content of children to parents/siblings 

This feature enhances display capabilities by allowing child or sibling content to be included in the parent product. While the previous feature focuses on filtering and aggregation, this functionality is purely for display purposes. 

#### Configuration

Two settings are used to define this behavior: 

- `PIM:Composition:VariationPropertiesToCopy:Children` 

- `PIM:Composition:VariationPropertiesToCopy:Siblings` 

Both accept a comma-separated list of `ProductPropertyTypes`, such as `color_name,color_hex_value`. 

#### Example usage

When configured, the resulting product content includes a `variations` array: 

```json
{
  "product_id": 123,
  "variations": [
    {
      "product_id": 456,
      "type": "child",
      "color_name": "Blue",
      "color_hex_value": "0000FF"
    },
    {
      "product_id": 789,
      "type": "sibling",
      "color_name": "Red",
      "color_hex_value": "FF0000"
    }
  ]
}
```
Product 123 has two variations available in blue and red, with the type property indicating if they are children or siblings. If the type is "child," the variation is one level below product 123, while if it's "sibling," the variations are on the same level, sharing the same parent.

#### Differences from CopyToParentProductPropertyTypeID

There is a direct reference to the ID of the child/sibling through a product_id property, along with the values of the content. With the CopyToParentProductPropertyTypeID commit, you only get a distinct list of values, with no relation to products. While having just the values is useful for filtering and aggregation, it doesn't work for display or linking.

The contents of variation are entirely unindexed, meaning it's not possible to filter anything inside of it. It's purely intended as enrichment data, not for search or filtering.

>**Note:**
By default, variations are not returned by SearchProducts or other services that accept an IncludedFields property. You have to request the variations field to include it. Changing the value of these two settings has no immediate effect. The value is only checked when a product is composed. After changing the settings, you should perform a ComposeProducts operation. This is not done automatically, as it’s an expensive operation, and you may want to test it by composing a few products first.

## Error handling - Failure responses

### Partial failure 

**Example**: You made an API call to update 100 products, but only 90 were successfully updated. The remaining 10 failed to update in EVA. The response will include details about the failed items and the reasons for the failure.

### Unknown tax code 

```json
{
  "Error": {
    "Message": "Product 123 uses unknown TaxCode",
    "Type": "ImportProducts:UnknownTaxCode",
    "Code": "JMJVDCGE",
    "RequestID": "1cc5912d5059455594a992d1c17c1a5b"
  }
}
```
This message represents an error response indicating that a product (Product 123) uses a tax code that is not recognized or is unknown.

### Validation failure 

```json
{
  "Error": {
    "Message": "The provided request did not pass validation. Failures:\n- Reason: MissingField, ProductID: , Field: PrimitiveName\n- Reason: MissingField, ProductID: , Field: PrimitiveName\n- Reason: DuplicateBackendID, ProductID: , Field: BackendID, Message: 123",
    "Type": "ImportProducts:ValidationFailures",
    "Code": "BMIYFDBY",
    "RequestID": "2161b89f451b4c47901c74f714c55280"
  }
}
```
The message contains technical-human-readable text that can be used for debugging. 
