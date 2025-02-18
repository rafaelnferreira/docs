---
title: 'Web Components - File Upload'
sidebar_label: 'File Upload'
id: file-upload
keywords: [web, web components, file upload]
tags:
    - web
    - web components
    - file upload
---

The `file-upload` component can be used to select single or multiple files from the local file system. Selected files can be uploaded to a server using the **Upload** button.

![](/img/file-upload-component-file-selected.PNG)

:::note 
The Upload button is disabled if no file is selected.
::: 

In addition, the uploaded files can be viewed in the [`data-grid`](../../grids/data-grid/). The `data-grid` also provides a **Download** button.

![](/img/file-upload-component.PNG)

## Set-up
In order to use the `file-upload` component, you need to import it from a design system. In the example below, we import it from zero-design-system and register it.

```ts
import { provideDesignSystem, zeroFileUpload } from '@genesislcap/zero-design-system';

provideDesignSystem().register(zeroFileUpload());
```

## Usage
The `file-upload` component can be used as shown below:

```html title="Basic example"
    <zero-file-upload     
          entity-id="Demo"
          field-name="ENTITY_ID"
          upload-key="series">
    </zero-file-upload>
```
:::warning
Please note that the `entity-id`, `upload-key` and `field-name` attributes are required for the `file-upload` component to work. Additionally, if no other attributes are passed, the `file-upload` component will use the default values for those attributes.
:::

If you want to customize the `file-upload` component, you can pass the attributes as shown below:
```html title="Customized example"
    <zero-file-upload
          label="Upload Files"
          accept="image/*,.doc,.docx,application/pdf"
          file-size-limit-bytes="104857600"
          uploaded-files-resource-name="ALL_FILE_ATTACHMENTS"
          entity-id="Demo"
          field-name="ENTITY_ID"
          upload-key="series"
          grid-fields="FILE_NAME DOWNLOAD LAST_UPDATED_BY LAST_UPDATED_AT"
          :downloadEventName=${(x, c) => x.handleDownload.bind(c.event)}>
    </zero-file-upload>
```
For more detailed information, see the [Attributes and Props](#attributes-and-props) section below.

## Attributes and Props
The following attributes can be used to customize the `file-upload` component:

:::note
Please note that the attributes marked with an  _(optional)_ tag are not required for the `file-upload` component to work. If no value is passed for those attributes, the `file-upload` component will use the default values.
:::

| Attribute Name | Description | 
| --- | --- |
| `label` _(optional)_ | The **label** attribute provides the caption for the file input, similar to HTML **Label** element. There is no default value specified for **label**. | 
| `accept` _(optional)_ | The **accept** attribute is used to determine the file formats that the file input should be able to select. Multiple file formats can be specified by separating them with a comma: *accept=".doc,.docx,application/pdf"*. By default all file formats are allowed. |
|`fileSizeLimitBytes` _(optional)_| This attribute refers to the maximum file size in bytes that is supported by the file input. The default value used is *104_857_600* (100MiB).|
| `uploadedFilesResourceName` _(optional)_ | The **uploadedFilesResourceName** attribute is the target [Data Server](../../../../../server/data-server/introduction/) or [Request Server](../../../../../server/request-server/introduction/) name that the `data-grid` uses to display the uploaded files. The default value for this attribute is *ALL_FILE_ATTACHMENTS*. |
|`uploadEventName` _(optional)_ | This attribute refers to the HTTP endpoint that will be used to upload the files. The default value is *attachment-handler/upload*. |
|`fieldName` | The **fieldName** attribute refers to the field name that will be used by the **uploadedFilesResourceName** as key for filtering the files list. |
| `entityId` | This attribute refers to the unique identifier that will be used by the **uploadEventName** endpoint to upload the files. This unique identifier will also be used by **uploadedFilesResourceName** as a value to filter the files list. |
| `uploadKey` | The **uploadKey** attribute is a unique key that will be used by the **uploadEventName** endpoint to upload the files. |
| `grid-fields` _(optional)_ | This attribute refers to the name of fields that you want to display as grid columns from the metadata of the `data-grid` datasource. By default all the fields from `data-grid` datasource metadata will be displayed. They must be specified in the format: *FILE_NAME DOWNLOAD LAST_UPDATED_BY LAST_UPDATED_AT*. The ordering which the fields are specified, will be reflected in the `data-grid` columns. If you want to display the **Download** button in the grid, you must include the **DOWNLOAD** field in the **grid-fields** attribute list along with **downloadEventName** attribute. |
| `errorOut` _(optional)_ | The **errorOut** attribute refers to the event that is triggered when an error occurs during the upload process. |
| `downloadEventName` _(optional)_ |The **downloadEventName** is an `observable` of type `function`. When you click the `download` button from a row in `data-grid`, it sends the `rowData` object as a parameter to the **downloadEventName** function. It should return the name of the endpoint that will be used to download the file. This is required in order to enable the download functionality. | 
## Use cases

The `file-upload` component can be used for the following use cases:

* uploading and downloading files
* displaying uploaded files in a grid
