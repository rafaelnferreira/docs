<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-comms](./foundation-comms.md) &gt; [MessageBuilder](./foundation-comms.messagebuilder.md) &gt; [createMetaRequestMessage](./foundation-comms.messagebuilder.createmetarequestmessage.md)

## MessageBuilder.createMetaRequestMessage() method

Creates a metadata fetch message.

**Signature:**

```typescript
createMetaRequestMessage(resourceName: string, messageType?: EventMessageType): Message<MessageDetails.MetaRequest>;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  resourceName | string | The resource name. |
|  messageType | [EventMessageType](./foundation-comms.eventmessagetype.md) | _(Optional)_ The event message type. |

**Returns:**

[Message](./foundation-comms.message.md)&lt;[MessageDetails.MetaRequest](./foundation-comms.messagedetails.metarequest.md)&gt;

The meta request message.

## Remarks

META\_REQUEST

