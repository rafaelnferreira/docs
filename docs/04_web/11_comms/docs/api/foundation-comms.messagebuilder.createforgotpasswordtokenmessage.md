<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-comms](./foundation-comms.md) &gt; [MessageBuilder](./foundation-comms.messagebuilder.md) &gt; [createForgotPasswordTokenMessage](./foundation-comms.messagebuilder.createforgotpasswordtokenmessage.md)

## MessageBuilder.createForgotPasswordTokenMessage() method

Creates a forgot password token message.

**Signature:**

```typescript
createForgotPasswordTokenMessage(username: string, resetToken: string, newPassword: string, requester?: string): Message<MessageDetails.ForgotPasswordToken>;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  username | string | The username. |
|  resetToken | string | The reset token. |
|  newPassword | string | The new password. |
|  requester | string | _(Optional)_ The requester. |

**Returns:**

[Message](./foundation-comms.message.md)&lt;[MessageDetails.ForgotPasswordToken](./foundation-comms.messagedetails.forgotpasswordtoken.md)&gt;

The forgot password token message.

