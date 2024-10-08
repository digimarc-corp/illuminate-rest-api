# Illuminate REST API

The illuminate-rest-api repository contains information, examples, and useful 
links for using the Illuminate REST API to work with platform resources, such 
as digital twins.

* [Getting Started](#getting-started)
* [Resource Schemas](#resource-schemas)
* [Requests](#requests)
* [Examples](#examples)
* [Help](#help)


## Getting Started

You access the API with keys that are created and managed in the 
Illuminate UI. API keys can have read-only or writable access with
the `API_READ_ONLY` and `API_EDITOR` roles, respectively.

After a key has been created, include it in the authorization header 
for every request. See the [Examples](#examples).

The base API URL is:

```
https://api.dmrc.app/rest
```

For each [request](#requests) detailed below, append the path and any 
parameters to the base URL.

> The limit for GET operations is 1000 records per request.

### Tips

* For date parameters, use the ISO standard datetimes, such as 
`2024-12-31T23:59:59.999Z`. Always include the time component.
* For product variant reason codes, see [GS1 Consumer Product Variant in GDSN Implementation Guide](https://www.gs1.org/docs/gdsn/3.1/CPV_GDSN_Implementation_Guide.pdf).
* For Global Product Classification (GPC) category codes, see the [GPC Browser](https://gpc-browser.gs1.org/).


## Resource Schemas

To help formulate requests and make use of responses, the schemas for resource
types related to digital twins are detailed below.

* [Digital Twin](#digital-twin)
* [Product](#product)
* [Product Variant](#product-variant)
* [Promotional Asset](#promotional-asset)
* [Brand](#brand)
* [Functional Name](#functional-name)
* [Asset Type](#asset-type)

### Digital Twin 

A digital twin resource can represent one of many types, such as products,
product variants, and promotional assets. See [List Digital Twins](#list-digital-twins).

> Excludes joined related resources

| Field | Type | Description |
|-------|------|-------------|
| `created` | String | Creation date of the digital twin |
| `createdById` | String | ID of the user who created the digital twin |
| `id` | String | ID of the digital twin |
| `modified` | String | The timestamp the digital twin was last modified |
| `modifiedById` | String | ID of the user who last modified the digital twin |
| `productId` | String | ID of the product the digital twin relates to, if it relates to a product |
| `resourceId` | String | ID of the resource the digital twin relates to |
| `resourceType` | String | Type of the resource the digital twin relates to |

### Product

A product resource represents a physical class of products. To create a product, an
existing [brand](#brand) resource is required.

> Excludes joined related resources

See

* [Create a Product](#create-a-product)
* [Update a Product](#update-a-product)
* [List Products](#list-products)

| Field | Type | Description |
|-------|------|-------------|
| `accountId` | String | ID of the account |
| `additionalTradeItemIdentification` | String | Additional trade item identification of the product |
| `created` | String | Creation date of the product |
| `createdById` | String | ID of the user who created the product |
| `customAttributes` | Object | Custom attributes of the product |
| `dataCarrierTypeCode` | String | Data carrier type code of the product |
| `dataCarrierValue` | String | Data carrier value of the product |
| `descriptionShort` | String | Name of the product |
| `descriptiveSize` | String | Descriptive size of the product |
| `endAvailabilityDateTime` | String | End availability date and time of the product |
| `firstOrderDateTime` | String | First order date and time of the product |
| `functionalNameId` | String | ID of the product's [functional name](#functional-name) |
| `gpcCategoryCode` | String | [Global Product Classification (GPC) category code](#tips) of the product |
| `id` | String | ID of the product |
| `identifier` | String | Primary identifier of the product, such as the GTIN or SKU |
| `modified` | String | The timestamp the product was last modified |
| `modifiedById` | String | ID of the user who last modified the product |
| `netContent` | String | Net content of the product |
| `productVariantsCount` | Number | Number of product variants for the product |
| `productVariantsWithTagsCount` | Number | Number of product variants that have a data carrier |
| `subBrandName` | String | Sub-brand name of the product (for future use) |
| `targetMarketCountryCodes` | String list | Target market country codes of the product |
| `tradeItemDescription` | String | Product's trade item description |

### Product Variant

A product variant resource represents a consumer product variant (CPV) of an 
existing product. See

* [Create a Product Variant](#create-a-product-variant)
* [Update a Product Variant](#update-a-product-variant)
* [List Product Variants](#list-product-variants)

| Field | Type | Description |
|-------|------|-------------|
| `accountId` | String | ID of the account |
| `consumerProductVariantDescription` | String | Product variant name up to 256 characters long |
| `consumerProductVariantEndEffectiveDateTime` | String | Product variant end effective date and time |
| `consumerProductVariantIdentification` | String | Product variant identifier |
| `consumerProductVariantReasonCode` | Number | Product variant reason code |
| `consumerProductVariantStartEffectiveDateTime` | String | Product variant start effective date and time |
| `created` | String | Creation date of the product variant |
| `createdById` | String | ID of the user who created the product variant |
| `customAttributes` | Object | Custom attributes of the product variant |
| `id` | String | ID of the product variant |
| `modified` | String | The timestamp the product variant was last modified |
| `modifiedById` | String | ID of the user who last modified the product variant |
| `productId` | String | ID of the product this variant belongs to |
| `productIdentifier` | String | Primary product identifier, such as GTIN or SKU |

### Promotional Asset

A promotional asset resource represents any media or other collateral that's 
associated with a product or its variants. Examples of promotional assets 
include TV commercials, brochures, posters, email marking campaigns, digital 
banner ads, and life-sized cardboard displays. See

* [Create a Promotional Asset](#create-a-promotional-asset)
* [Update a Promotional Asset](#update-a-promotional-asset)
* [List Promotional Assets](#list-promotional-assets)
* [Asset Type](#asset-type)

| Field | Type | Description |
|-------|------|-------------|
| `accountId` | String | ID of the account |
| `assetTypeId` | String | ID of the [asset type](#asset-type) |
| `brandId` | String | ID of the associated product's [brand](#brand) |
| `created` | String | Creation date of the promotional asset |
| `createdById` | String | ID of the user who created the promotional asset |
| `customAttributes` | Object | Custom attributes of the promotional asset |
| `customerIdentifier` | String | Customer identifier of the promotional asset |
| `descriptionShort` | String | Short description of the promotional asset up to 512 characters long |
| `endDate` | String | End date of the promotional asset |
| `id` | String | ID of the promotional asset |
| `modified` | String | The timestamp the promotional asset was last modified |
| `modifiedById` | String | ID of the user who last modified the promotional asset |
| `productCount` | Number | Number of related products for the promotional asset |
| `productVariantCount` | Number | Number of related product variants for the promotional asset |
| `startDate` | String | Start date of the promotional asset |

### Brand

A brand represents a customer's brand. See

* [Create a Brand](#create-a-brand)
* [List Brands](#list-brands)

| Field | Type | Description |
|-------|------|-------------|
| `accountId` | String | ID of the account |
| `created` | String | Creation date of the brand |
| `createdById` | String | ID of the user who created the brand |
| `id` | String | ID of the brand |
| `modified` | String | The timestamp the brand was last modified |
| `modifiedById` | String | ID of the user who last modified the brand |
| `name` | String | Name of the brand |

### Functional Name

A functional name represents the type or purpose of a product. In the 
Illuminate UI, this is labeled the "Product type." Examples are "hand 
sanitizer" and "flour." See

* [Create a Functional Name](#create-a-functional-name)
* [List Functional Names](#list-functional-names)

| Field | Type | Description |
|-------|------|-------------|
| `accountId` | String | ID of the account |
| `created` | String | Creation date of the functional name |
| `createdById` | String | ID of the user who created the functional name |
| `id` | String | ID of the functional name |
| `modified` | String | The timestamp the functional name was last modified |
| `modifiedById` | String | ID of the user who last modified the functional name |
| `name` | String | Functional name |

### Asset Type

An asset type represents a specific type of promotional asset, such as a
poster or advertisement. See

* [Create an Asset Type](#create-an-asset-type)
* [List Asset Types](#list-asset-types)

| Field | Type | Description |
|-------|------|-------------|
| `accountId` | String | ID of the account |
| `created` | String | Creation date of the asset type |
| `createdById` | String | ID of the user who created the asset type |
| `id` | String | ID of the asset type |
| `modified` | String | The timestamp the asset type was last modified |
| `modifiedById` | String | ID of the user who last modified the asset type |
| `name` | String | Asset type name |


## Requests

This section contains request examples and parameters for the available endpoints.

* [List Digital Twins](#list-digital-twins)
* [Create a Product](#create-a-product)
* [List Products](#list-products)
* [Update a Product](#update-a-product)
* [Create a Product Variant](#create-a-product-variant)
* [List Product Variants](#list-product-variants)
* [Update a Product Variant](#update-a-product-variant)
* [Create a Promotional Asset](#create-a-promotional-asset)
* [List Promotional Assets](#list-promotional-assets)
* [Update a Promotional Asset](#update-a-promotional-asset)
* [Create a Promotional Asset Link](#create-a-promotional-asset-link)
* [List Promotional Asset Links](#list-promotional-asset-links)
* [Delete a Promotional Asset Link](#delete-a-promotional-asset-link)
* [Create a Data Carrier](#create-a-data-carrier)
* [List Data Carriers](#list-data-carriers)
* [List Digital Twin Images](#list-digital-twin-images)
* [Upload a Digital Twin Image From File](#upload-a-digital-twin-image-from-file)
* [Update a Digital Twin Image](#update-a-digital-twin-image)
* [Create a Digital Twin Image From URL](#create-a-digital-twin-image-from-url)
* [Delete a Digital Twin Image](#delete-a-digital-twin-image)
* [Create a Brand](#create-a-brand)
* [List Brands](#list-brands)
* [Create a Functional Name](#create-a-functional-name)
* [List Functional Names](#list-functional-names)
* [Create an Asset Type](#create-an-asset-type)
* [List Asset Types](#list-asset-types)

#### About the Digital Twin ID

When updating information about a product, variant, or promotional asset, 
you're amending *a part of* the digital twin. For example, adding 
`customAttributes` to a product entails adding additional data to the product 
record of a digital twin. When you add images to a product (or product 
variant or promotional asset), you're actually adding another `resourceType` 
to the digital twin itself. The digital twin can contain a product, variant, 
or promotional asset record, images, data carriers, and more.

Each digital twin has a unique `id`, which isn't displayed in the Illuminate 
UI. For example, if you use the UI to look at a product digital twin, the URL 
in the browser's address bar takes this form:
https://*domain*/*accountId*/digital-twins/*productId*

Some endpoints take a `digitalTwinId` as input, such as 
`POST /digitalTwinImages/create` and `POST /dataCarriers`. The `productId` isn't 
the same as the digital twin's `id` (that is, the `digitalTwinId`); setting 
`digitalTwinId` to the `productId` value won't return the correct result.

An easy way to get the digital twin's `id` is to call `GET /digitalTwins` with 
a filter and include the `productId` in the `product.ids` array:

```json
"filter": {
    "product": {
        "ids": [
            "$PRODUCT_ID"
        ]
    }
}
```

Similarly, to get the digital twin's `id` for a product variant or promotional 
asset, the filter might look like this:

```json
"filter": {
    "productVariant": {
        "ids": [
            "$VARIANT_ID"
        ]
    }
}
```

or 

```json
"filter": {
    "promotionalAsset": {
        "ids": [
            "$PROMOASSET_ID"
        ]
    }
}
```

In the sample `GET /digitalTwins` output below, note the 
`dataCarriers.digitalTwinId` value. This is the digital twin's `id` for the 
specified product (or product variant or promotional asset) twin. You set 
the `digitalTwinId` to that value when calling endpoints that require it.

> The `dataCarriers` array is empty for digital twins that have no data carriers.

```json
[
    {
        "created": "2024-05-01T21:51:18.776Z",
        "createdById": "auth0|12345a6789b012c345d67d8e",
        "dataCarriers": [
            {
                "accountId": "a1b2c3d4-e5f6-a1b2-c3d4-e3cacf1d35a3",
                ...
                "digitalTwinId": "aaaa1111-f211-44fa-ef56-96ce6b23797b",
                "id": "d1c2b3a4-58f6-66ee-55ff-2c4f92205b8f",
                ...
            }
        ],
        "id": "aaaa1111-f211-44fa-ef56-96ce6b23797b",
        "modified": "2024-05-01T21:51:18.776Z",
        "modifiedById": "auth0|12345a6789b012c345d67d8e",
        "product": {
            "accountId": "a1b2c3d4-e5f6-a1b2-c3d4-e3cacf1d35a3",
            ...
            "id": "4321dcba-a09b-48fb-76fe-c7d11e79b3ac",
            "identifier": "00987654000321",
            ...
        },
        "productId": "4321dcba-a09b-48fb-76fe-c7d11e79b3ac",
        ...
    },
    ...
]
```

### List Digital Twins

Displays the list of [digital twins](#digital-twin) in the account. 

```
GET /digitalTwins
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `CREATED_ASC`, `CREATED_DESC`, `MODIFIED_ASC`, `MODIFIED_DESC`, `TYPE_ASC`, or `TYPE_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `query` | String | Search query to apply |
| `resourceTypes` | String list | Resource types: `PRODUCT`, `PRODUCT_VARIANT`, or `PROMOTIONAL_ASSET` |
| `digitalTwinIds.in` | String list | List of digital twin IDs to return |
| `digitalTwinIds.notIn` | String list | List of digital twin IDs to exclude |
| `modified.from` | String | Return results modified after YYYY-MM-DD |
| `modified.to` | String | Return results modified before YYYY-MM-DD |
| `product.ids` | String list | List of product IDs to return twins for |
| `product.brandId.eq` | String | ID of the [brand](#brand) |
| `product.brandId.in` | String list | List of brands |
| `product.gpcCategoryCode.eq` | String | [Global Product Classification (GPC) category code](#tips) |
| `product.gpcCategoryCode.in` | String list | List of category codes |
| `product.identifiers.eq` | String | Product identifier |
| `product.identifiers.in` | String | Partial product identifier |
| `product.identifiers.starts` | String | Start of partial product identifier |
| `product.identifiers.ends` | String | End of partial product identifier |
| `promotionalAsset.ids` | String list | IDs of promotional assets |
| `promotionalAsset.brandId.eq` | String | Promotional asset brand ID |
| `promotionalAsset.brandId.in` | String list | IDs of promotional asset brands |
| `productVariantids.ids` | String list | IDs of product variants |
| `productVariantids.brandId.eq` | String | Product variant's product brand ID |
| `productVariantids.brandId.in` | String list | IDs of possible product variant brands |
 

### Create a Product

Setting `useDefaultSettings` to true eliminates the need to set the 
`shortUrlDomain` and `urlFormat`; Illuminate creates all the account's default 
data carrier type formats using their default values. 

If the account was configured to allow an additional identifier, such as for an 
online retailer, you can specify it in the `additionalTradeItemIdentification` 
property. The max length is configured for each account, but it can't be longer 
than 64 characters. 

Creating a [product](#product) requires a [brand](#brand) ID. See

* [Create a Brand](#create-a-brand)
* [List Brands](#list-brands)

```
POST /products
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `additionalTradeItemIdentification` | String | no | Additional trade identifier |
| `brandId` | String | yes | Product's [brand](#brand) ID |
| `customAttributes` | Object | no | Custom attributes |
| `descriptionShort` | String | yes | Name of the product up to 64 characters long |
| `descriptiveSize` | String | no | Descriptive size |
| `digitalTag` | String | no | Data carrier type format: `DIGITAL_WATERMARK`, `DIGITAL_WATERMARK_AND_QR_CODE`, or `QR_CODE` |
| `endAvailabilityDateTime` | String | no | End availability date time |
| `firstOrderDateTime` | String | no | First order date time |
| `functionalNameId` | String | no | ID of the product's [functional name](#functional-name) |
| `gpcCategoryCode` | String | yes | [Global Product Classification (GPC) category code](#tips) |
| `identifier` | String | yes | Product primary identifier, such as GTIN or SKU |
| `netContent` | String | no | Net content |
| `shortUrlDomain` | String | no | Short URL domain preference for creating a `QR_CODE` (ignored if `urlFormat` is `DigitalLink`) |
| `subBrandName` | String | no | Sub-brand name (for future use) |
| `targetMarketCountryCodes` | String list | no | Target market country codes |
| `tradeItemDescription` | String | no | Product description up to 512 characters long |
| `urlFormat` | String | no | Data carrier link format: `DigitalLink` or `ShortUrl` |
| `useDefaultSettings` | Boolean | no | Use default settings to create the data carrier(s) |

### List Products

```
GET /products
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `MODIFIED_ASC`, `MODIFIED_DESC`, `NAME_ASC`, or `NAME_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `product.identifiers` | String list | List of product identifiers to filter on |
| `product.ids` | String list | List of products to filter on |

### Update a Product

If the account was configured to allow an additional identifier, such as for an 
online retailer, you can specify it in the `additionalTradeItemIdentification` 
property. The max length is configured for each account, but it can't be longer 
than 64 characters.

```
PUT /products
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | ID of the target account |
| `id` | String | yes | ID of the target product |
| `patch` | `UpdateProductPatch` | yes | Data patch to apply to the target product 
(see below) |

**UpdateProductPatch**

| Name | Type | Description |
|------|------|-------------|
 | `additionalTradeItemIdentification` | String | Additional trade identifier |
 | `brandId` | String | ID of the product's [brand](#brand) |
 | `customAttributes` | Object | Custom attributes |
 | `descriptionShort` | String | Name of the product up to 64 characters long |
 | `descriptiveSize` | String | Descriptive size |
 | `endAvailabilityDateTime` | String | End availability date time |
 | `firstOrderDateTime` | String | First order date time |
 | `functionalNameId` | String | ID of the product's [functional name](#functional-name) |
 | `gpcCategoryCode` | String | [Global Product Classification (GPC) category code](#tips) |
 | `netContent` | String | Net content |
 | `subBrandName` | String | Sub-brand name (for future use) |
 | `targetMarketCountryCodes` | String list | Target market country codes |
 | `tradeItemDescription` | String | Product's description up to 512 characters long |

### Create a Product Variant

Creates a [variant](#product-variant) of an existing product with the same 
primary identifier. 

For the reason code, see the 
[GS1 Consumer Product Variant in GDSN Implementation Guide](#tips). 

Setting `useDefaultSettings` to true eliminates the need to set the 
`shortUrlDomain` and `urlFormat`; Illuminate creates all the account's default 
data carrier type formats using their default values. 

```
POST /productVariants
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `consumerProductVariantDescription` | String | yes | Product variant name up to 256 characters long |
| `consumerProductVariantEndEffectiveDateTime` | String | no | Effective end date time |
| `consumerProductVariantIdentification` | String | yes | Product variant identifier |
| `consumerProductVariantReasonCode` | String | yes | Product variant reason code |
| `consumerProductVariantStartEffectiveDateTime` | String | no | Effective start date time |
| `customAttributes` | Object | no | Custom attributes |
| `digitalTag` | String | no | Data carrier type: `DIGITAL_WATERMARK`, `DIGITAL_WATERMARK_AND_QR_CODE`, or `QR_CODE` |
| `productIdentifier` | String | yes | Primary identifier (such as GTIN or SKU) of the product that's related to the variant |
| `shortUrlDomain` | String | no | Short URL domain preference |
| `urlFormat` | String | no | Data carrier link format: `DigitalLink` or `ShortUrl` |
| `useDefaultSettings` | Boolean | no | Use default settings for data carrier |

### List Product Variants

```
GET /productVariants
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `MODIFIED_ASC`, `MODIFIED_DESC`, `NAME_ASC`, or `NAME_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `productVariant.ids` | String list | List of product variants to filter on |
| `productVariant.productIds` | String list | List of products to filter on |


### Update a Product Variant

For the reason code, consult the <em>GS1 Consumer Product Variant in GDSN
Implementation Guide</em>.

```
PUT /productVariants
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | ID of the target account |
| `id` | String | yes | ID of the target product variant |
| `patch` | `UpdateProductVariantPatch` | yes | Data patch to apply to the target product variant |

**UpdateProductVariantPatch**

| Name | Type | Description |
|------|------|-------------|
| `consumerProductVariantDescription` | String | Product variant name up to 256 characters long |
| `consumerProductVariantEndEffectiveDateTime` | String | Effective end date time |
| `consumerProductVariantReasonCode` | String | Product variant reason code |
| `consumerProductVariantStartEffectiveDateTime` | String | Effective start date time |
| `customAttributes` | Object | Custom attributes |


### Create a Promotional Asset

Promotional assets don't have a GTIN, but they might have another identifier 
such as an internal part number that you can set in `customerIdentifier`.

Setting `useDefaultSettings` to true eliminates the need to set the 
`shortUrlDomain` and `urlFormat`; Illuminate creates all the account's default 
data carrier type formats using their default values. 

```
POST /promotionalAssets
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `assetTypeId` | String | yes | Associated [asset type](#asset-type) ID |
| `brandId` | String | yes | ID of the associated product's [brand](#brand) |
| `customAttributes` | Object | no | Custom attributes |
| `customerIdentifier` | String | no | Customer-provided identifier |
| `descriptionShort` | String | yes | Short description of the asset up to 512 characters long |
| `digitalTag` | String | no | Data carrier type: `DIGITAL_WATERMARK`, `DIGITAL_WATERMARK_AND_QR_CODE`, or `QR_CODE` |
| `endDate` | String | no | The date the promotional asset was or will be removed from use. Must be on or after the `startDate` |
| `shortUrlDomain` | String | no | Short URL domain preference |
| `startDate` | String | no | The date the promotional asset was or will be first put into use. Must be on or before the `endDate`|
| `urlFormat` | String | no | Data carrier link format: `DigitalLink` or `ShortUrl` |
| `useDefaultSettings` | Boolean | no | Use default settings for data carrier |

### List Promotional Assets

```
GET /promotionalAssets
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `MODIFIED_ASC`, `MODIFIED_DESC`, `NAME_ASC`, or `NAME_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `promotionalAsset.ids` | String list | IDs of promotional assets to filter on |

### Update a Promotional Asset

```
PUT /promotionalAssets
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | ID of the target account |
| `id` | String | yes | ID of the target promotional asset |
| `patch` | `UpdatePromotionalAssetPatch` | yes | Data patch to apply to the target promotional asset |

**UpdatePromotionalAssetPatch**

| Name | Type | Description |
|------|------|-------------|
| `assetTypeId` | String | [Promotional asset type](#asset-type) ID |
| `brandId` | String | ID of the promotional asset's [brand](#brand) |
| `customAttributes` | Object | Custom attributes |
| `customerIdentifier` | String | Promotional asset's customer-provided identifier |
| `endDate` | String | The date the promotional asset was or will be removed from use. Must be on or after the `startDate` |
| `startDate` | String | The date the promotional asset was or will be first put into use. Must be on or before the `endDate` |

### Create a Promotional Asset Link

Promotional assets relate to the products or variants they are associated with
by using promotional asset links. Each `PromotionalAssetLink` is a combination 
of `promotionalAssetId` + `productId` or `promotionalAssetId` + 
`productVariantId`.


```
POST /promotionalAssetLinks
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `links` | `PromotionalAssetLink` list | yes | Array of promotional asset links (see below) |

**PromotionalAssetLink**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `productId` | String | no | Associated product ID |
| `productVariantId` | String | no | Associated product variant ID |
| `promotionalAssetId` | String | yes | Associated promotional asset ID |


### List Promotional Asset Links

```
GET /promotionalAssetLinks
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `CREATED_ASC` or `CREATED_DESC` |
| `promotionalAssetId` | String | no | ID of the promotional asset to filter on |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `product.ids` | LinkProductIDs | IDs of the products to filter on |
| `productVariant.ids` | LinkProductVariantIDs | IDs of the product variants to filter on |
| `promotionalAsset.ids` | LinkPromotionalAssetIDs | IDs of the promotional assets to filter on |

### Delete a Promotional Asset Link

> You can't use the API to delete digital twins, only to delete the links between a 
promotional asset twin and its associated product or variant twins.

```
DELETE /promotionalAssetLinks
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `ids` | String list | yes | Array of promotional asset link IDs to delete |

### Create a Data Carrier

Creates a data carrier for a digital twin that doesn't have one. 

Setting `useDefaultSettings` to true eliminates the need to set the 
`shortUrlDomain` and `urlFormat`; Illuminate creates the specified data carrier 
type format using its default values.

> \* If `useDefaultSettings` is set to false, `shortUrlDomain` and `urlFormat` 
must be set regardless of `carrierType`.

```
POST /dataCarriers
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `consumerProductVariantIdentification` | String | no | Customer-provided product variant identifier |
| `digitalTwinId` | String | yes | Digital twin ID associated with the data carrier |
| `shortUrlDomain` | String | * | URL of the data carrier |
| `carrierType` | String | yes | Data carrier type format: `DIGITAL_WATERMARK` or `QR_CODE` |
| `urlFormat` | String | * | Data carrier link format: `DigitalLink` or `ShortUrl` |
| `useDefaultSettings` | Boolean | yes | Use default settings for generating the data carrier |

### List Data Carriers

```
GET /dataCarriers
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `filter` | Object | yes | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `digitalTwin.ids` | String list | yes | List of digital twins to filter on |
| `carrierTypes` | String list | yes | List of data carrier types to filter on |

### List Digital Twin Images

```
GET /digitalTwinImages
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `digitalTwinId` | String | yes | Digital twin ID associated with the data carrier |
| `first` | Number | yes | Number of results to return per page |

### Upload a Digital Twin Image From File

1. Start the upload by declaring the image to be uploaded.
2. Upload the data with a `PUT` request to the URL returned.
3. Complete the upload, which prepares thumbnail images.

```
POST /digitalTwinImages/uploads/start
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `contentType` | String | yes | Digital twin image content type: `jpg` or `png` |
| `digitalTwinId` | String | yes | Digital twin ID |
| `fileName` | String | yes | Digital twin image file name |
| `isDefault` | Boolean | yes | Set an image as the default |


```
POST /digitalTwinImages/uploads/finalize
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `digitalTwinImageId` | String | yes | Digital twin image ID |

### Update a Digital Twin Image

```
PUT /digitalTwinImages
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | ID of the target account |
| `digitalTwinImageId` | String | yes | ID of the digital twin image |
| `patch` | `UpdateDigitalTwinImagePatch` | yes | Data patch to apply to the target digital image |

**UpdateDigitalTwinImagePatch**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `isDefault` | Boolean | yes | Sets the image as the default. Must be `true`. If another image was previously set as the default, the flag is unset for that image. |

### Create a Digital Twin Image From URL

```
POST /digitalTwinImages/create
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `contentType` | String | yes | Digital twin image content type: `jpg` or `png` |
| `digitalTwinId` | String | yes | Digital twin ID |
| `fileName` | String | yes | Digital twin image file name |
| `isDefault` | Boolean | yes | Setting an image as default |
| `sourceUrl` | String | yes | Source URL |

### Delete a Digital Twin Image

```
DELETE /digitalTwinImages
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `digitalTwinImageId` | String | yes | Digital twin image ID |

### Create a Brand

```
POST /brands
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `name` | String | yes | Brand name |

### List Brands

```
GET /brands
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `MODIFIED_ASC`, `MODIFIED_DESC`, `NAME_ASC`, or `NAME_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `brand.ids` | String list | List of brands to filter on |

### Create a Functional Name

```
POST /functionalNames
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `name` | String | yes | Functional name |

### List Functional Names

```
GET /functionalNames
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `MODIFIED_ASC`, `MODIFIED_DESC`, `NAME_ASC`, or `NAME_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `functionalName.ids` | String list | List of functional names to filter on |


### Create an Asset Type

```
POST /assetTypes
Authorization: ApiKey $API_KEY
Content-Type: application/json
```

**Body Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Associated account ID |
| `name` | String | yes | Asset type name |

### List Asset Types

```
GET /assetTypes
Authorization: ApiKey $API_KEY
```

**Query Parameters**

| Name | Type | Required? | Description |
|------|------|-----------|-------------|
| `accountId` | String | yes | Account ID |
| `first` | Number | yes | Number of results to return per page |
| `after` | String | no | ID given as the cursor in the previous page to read the next one |
| `order` | String | yes | Sort order for results: `MODIFIED_ASC`, `MODIFIED_DESC`, `NAME_ASC`, or `NAME_DESC` |
| `filter` | Object | no | Filter to apply (see below) |

**Filter Parameters**

| Name | Type | Description |
|------|------|-------------|
| `assetType.ids` | String list | List of [asset types](#asset-type) to filter on |


## Examples

The following examples will help you understand what you can do with the 
Illuminate API.

* [List Digital Twins with Search](#list-digital-twins-with-search)
* [Create a Product Example](#create-a-product-example)
* [Filter Products by GTIN](#filter-products-by-gtin)
* [Filter Promotional Assets by ID](#filter-promotional-assets-by-id)
* [Update a Product Variant Example](#update-a-product-variant-example)
* [Create a Data Carrier Example](#create-a-data-carrier-example)

### List Digital Twins with Search

Search for digital twins of all types where an applicable field
(for example, descriptions) includes the text 'example':

```shell
curl -H "Authorization: ApiKey $API_KEY" \
  -X GET '$API_URL/digitalTwins?accountId=$ACCOUNT_ID&first=30&order=MODIFIED_DESC&filter={"query":"example"}'
```

### Create a Product Example

Create a product digital twin with data carrier(s) in the 'Beauty/Personal Care/Hygiene'
category using the account's default data carrier settings:

```shell
curl -H "Authorization: ApiKey $API_KEY" \
  -H Content-Type:application/json \
  -X POST '$API_URL/products' \
  -d '{
    "accountId": "$ACCOUNT_ID",
    "brandId": "$BRAND_ID",
    "descriptionShort": "Example Product",
    "gpcCategoryCode": "53000000",
    "identifier": "01234567891224",
    "customAttributes": {
        "first": "one",
        "second": "two",
        "third": "three"
    },
    "useDefaultSettings": true
}'
```

### Filter Products by GTIN

Get product digital twins using a filter on the GTIN or other primary identifier (such as SKU).

```shell
curl -H "Authorization: ApiKey $API_KEY" \
  -H Content-Type:application/json \
  -X GET '$API_URL/products' \
  -d '{
    "accountId": "$ACCOUNT_ID",
    "order": "MODIFIED_ASC",
    "first": 30,
    "filter": {
        "product": {
            "identifiers": [
                "$GTIN1",
                "$GTIN2",
                "$GTINn"
            ]
        }
    }
}'
```

### Filter Promotional Assets by ID

Get promotional asset digital twins using a filter on the promotional asset's identifier (`promotionalAsset.id`).

```shell
curl -H "Authorization: ApiKey $API_KEY" \
  -H Content-Type:application/json \
  -X GET '$API_URL/promotionalAssets' \
  -d '{
    "accountId": "$ACCOUNT_ID",
    "order": "MODIFIED_DESC",
    "filter": {
        "promotionalAsset": {
            "ids": [
                "$PROMOASSET_ID1",
                "$PROMOASSET_ID2",
                "$PROMOASSET_IDn"
            ]
        }
    },
    "first": 10
}'
```

### Update a Product Variant Example

Update the reason code and remove custom attributes for a product variant digital twin.

```shell
curl -H "Authorization: ApiKey $API_KEY" \
  -H Content-Type:application/json \
  -X PUT '$API_URL/productVariants' \
  -d '{
    "accountId": "$ACCOUNT_ID",
    "id": "$PRODUCTVARIANT_ID",
    "patch": {
        "consumerProductVariantReasonCode": "ADD_ADDITIONAL_LANGUAGE",
        "customAttributes": {}
    }
}'
```

### Create a Data Carrier Example

Create a digital watermark for a digital twin that doesn't have one. Be sure to use the digital twin's `id` rather than the `productId`, `productVariant.id`, or `promotionalAsset.id` for the `digitalTwinId` parameter. It might be helpful to run `GET /digitalTwins` first to get the digital twin's `id`.

```shell
curl -H "Authorization: ApiKey $API_KEY" \
  -H Content-Type:application/json \
  -X POST '$API_URL/dataCarriers' \
  -d '{
    "accountId": "$ACCOUNT_ID",
    "digitalTwinId": "$DIGITAL_TWIN_ID",
    "carrierType": "DIGITAL_WATERMARK",
    "useDefaultSettings": true
}'
```

## Help

You can request assistance by creating a support ticket in the Illuminate UI. 
Log into Illuminate and click the Help icon to get started.
