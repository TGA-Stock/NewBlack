# Product setup and management
EVA, short for Elastic Versatile Architecture, is an ecommerce system created by New Black to make shopping easier and more seamless for you, your business and your customers. It helps you to connect all your sales channels—like online stores, physical shops, and mobile apps—into one system, so you can keep up with modern shopping trends and deliver a smooth, consistent experience to your customers. 

This document describes how you you can migrate your product information into EVA. All product migration can be done using JSON format. For further context and information concerning the use of EVA, please refer to our User Manual.

**Covered in this document**
1. Product Setup and Management
- Product Migration
- Single Product Upload
- Product Types
- Product Hierarchy
- Editing Products
- Deleting Products
- Barcodes

2. Product Content
- Product Content
  - Images
  - Languages
  - Native Content Options
  - USP Text and USP Blobs
- Properties
  - Creating Product Properties
  - Display Values for Customer Properties
  - Product Property Categories
  - Defining Values in ImportProducts
  - Creating Product Properties in ImportProducts
  - Copying Properties to Parents
  - Including Content of Children to Parents/Siblings

3. Error Handling
- Failure Responses
  - Partial Failure
  - Unknown Tax Code
  - Validation Failure

4. Additional Services
- Additional Services

## Single product upload

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

In the above example, we create a product called 'Unisex T-shirt' with a `SystemID`/`BackendID` (ID) and a `TaxCode`. We use `SystemID` to identify the system from which we are importing our products. 

In addition to the SystemID we provide a unique identifier `ID` field, all products can have this `CustomID`. If you don't specify a `CustomID`, the `BackendID` will be used as default. 

#### Response 

Your products will always have an `EvaID` assigned upon creation. Your response will include these EVA IDs, grouped by which products were updated or created. When products are created, they are also updated. Additionally, we return a `BackendID`/`EvaID` mapping. 

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

## Product types 

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
## Barcodes 

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
## Product hierarchy 

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

::: 

## Failure responses 

### Partial failure 

Let's assume you made an API call to update 100 products but out of this only 90 products were updated. The remaining 10 failed to update in EVA. The response would then contain the parts of the call that failed, and the reason why they failed. 

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

## Editing products 

To edit products, just use the same request and alter the information. EVA will know to update the product if the specified `ID` is already in use. 

## Deleting products 

To delete products, use the same request, but add the `"IsDeleted": true` property on the products and set it to true. The products will then be deleted. It's good to know that the products actually remain in EVA, their status will just be: *Deleted* and they won't be visible on the front ends anymore.



# Product 

**Product Content can be included in the 'ImportProducts' service using the 'Content' array on product level.**

## Images 

We will illustrate how this works using a simple product with a simple image first: 

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

## Languages 

Note how the `Content` property in our example request is an array, that's because you can add content for multiple languages: 

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

## Native content options 
EVA ships some native product properties which have some functionalities in our front-ends. If yuo are looking for possibilities beyond our native options though, see[Custome product properties] (/link).

## USP Text and USP Blobs 

Using the `UniqueSellingPointTexts` and `UniqueSellingPointBlobIDs` you can display product information on **POS** and **Companion App** directly in the search result by providing the respective input to the referred to properties. 

Here is what this would look like using our NewBorn T-Shirt example: 

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

>**Important Note:** The text and blobs are order sensitive. So in our example, "Green choice" will link to the first BlobID, "Vegan" to the second, and so forth. For the BlobID you can refer to [Blob management](/link).

## Properties 

You might be wondering about the meaning of each property, but it's quite self- explanatory. Here's a breakdown: 

| Property          | Description                                                        |
|-------------------|--------------------------------------------------------------------|
| **ID**            | This is the product ID.                                            |
| **TaxCode**       | Give the correct [tax code](/link) for your product.               |
| **LanguageID**    | The ID of the language in which the product description is displayed. |
| **ShortDescription** | A brief description of your product.                             |
| **ImageURL**      | The URL to your product image. 

# Custom product properties 

The `ImportProducts` service can be used to fill custom product properties that already exist in EVA. It is also possible to fill properties that do not yet exist, if you define these properties on root level first.

## Creating product properties 

To create a custom product property, use [CreateProductPropertyType](/link): 

```json
{
  "TypeID": "eu_ecolabel",
  "CategoryID": "default",
  "DataType": 3
}
```

Except for `TypeID` and `CategoryID`, this service works the exact same as our [CustomField](/link) services. 

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

### Additional property types
- [SearchProductPropertyType]
- [DeleteProductPropertyType]
- [ListProductPropertyType]

### Product property categories 
- [CreateProductPropertyCategory]
- [EditProductPropertyCategory]
- [ListProductPropertyCategory]

>**Note:** Product property categories can't be deleted.

## Defining values in ImportProducts
To add values for the custom product property we've just created, we use the `Content` object in `ImportProducts`: 

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

Since our custom product property was just a boolean, our case is pretty simple. 

>**Note:**Since these product properties live in the content object, they can have different values for different languages.

## Creating product properties in ImportProducts
If we didn't have our property preconfigured, we could also just provide it in the `ImportProducts` message: 

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

After this message, the product property will be known in EVA and the correct value will be set on the product.

## Copying properties to parents 

On an e-commerce site overview page, you typically want to display color or style-level products instead of size-level products. However, you might want to provide filters on available colors and sizes. This data is often not present at the style or color level unless explicitly provided. 

Using the `ProductPropertyType` called `CopyToParentProductPropertyTypeID`you can refer to the ID of another property whose value will be copied to its parent. 

### Example Usage 

For instance, if a size-level product is available in "S", "M", and "L", setting `CopyToParentProductPropertyTypeID` on the size property to `available_sizes` ensures that these values are copied to the parent (color-level) and grandparent (style-level) products under the `available_sizes` property.

Example of using this feature through ImportProducts:

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

## Including content of children to parents/siblings 

### Overview 

This feature enhances display capabilities by allowing child or sibling content to be included in the parent product. While the previous feature focuses on filtering and aggregation, this functionality is purely for display purposes. 

### Configuration 

Two settings are used to define this behavior: 

- `PIM:Composition:VariationPropertiesToCopy:Children` 

- `PIM:Composition:VariationPropertiesToCopy:Siblings` 

Both accept a comma-separated list of `ProductPropertyTypes`, such as `color_name,color_hex_value`. 

### Example Usage 

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

**Differences from CopyToParentProductPropertyTypeID**

There is a direct reference to the ID of the child/sibling through a product_id property, along with the values of the content. With the CopyToParentProductPropertyTypeID commit, you only get a distinct list of values, with no relation to products. While having just the values is useful for filtering and aggregation, it doesn't work for display or linking.

The contents of variation are entirely unindexed, meaning it's not possible to filter anything inside of it. It's purely intended as enrichment data, not for search or filtering.

>**Note:**
By default, variations are not returned by SearchProducts or other services that accept an IncludedFields property. You specifically have to request the variations field to include it. Changing the value of these two settings has no immediate effect. The value is only checked when a product is composed. After changing the settings, you should perform a ComposeProducts operation. This is not done automatically, as it’s an expensive operation, and you may want to test it by composing a few products first.


