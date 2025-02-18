<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@genesislcap/foundation-comms](./foundation-comms.md) &gt; [CredentialManager](./foundation-comms.credentialmanager.md) &gt; [getCredentials](./foundation-comms.credentialmanager.getcredentials.md)

## CredentialManager.getCredentials() method

Retrieves stored credentials.

**Signature:**

```typescript
getCredentials(options?: GetCredentialOptions): Promise<CredentialData | undefined>;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  options | [GetCredentialOptions](./foundation-comms.getcredentialoptions.md) | _(Optional)_ An object containing options for retrieving credentials. |

**Returns:**

Promise&lt;[CredentialData](./foundation-comms.credentialdata_2.md) \| undefined&gt;

A Promise that resolves to a CredentialData object if the credentials are found, or undefined otherwise.

