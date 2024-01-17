---
id: raw-document-eth
title: Create raw documents
sidebar_label: Create raw documents
---

Every OA document has a checksum that provides it a tamper-proof property. At the same time, because the checksum can be used to uniquely identify a document, the checksum (or its derived value) is stored onto the document store as evidence of issuance. To compute the checksum, a `raw document` goes through a process known as `wrapping` to become a `wrapped document`. Only then, the document is ready to be issued onto the blockchain.

In this guide, you will learn how to create one raw document that conforms to the OpenAttestation v2 Schema.

## OA document schema

The OpenAttestation v2.0 defines the shape of data for the `raw document` - the data before the wrapping process. It is defined in [JSON Schema](https://json-schema.org/) format.

The official OpenAttestation v2.0 schema can be found at https://schema.openattestation.com/2.0/schema.json

## Using online schema validator

For this guide, you will use an online JSON Schema validator to write the raw document.

### Setting up the JSON schema validator with OA schema

Visit https://www.jsonschemavalidator.net/

Paste the contents from https://schema.openattestation.com/2.0/schema.json into the left panel under "Select Schema".

This will setup the JSON schema validator to validate the JSON inputs on the right against the defined schema.

![Validator Preview](/docs/integrator-section/verifiable-document/ethereum/document-data/validator-preview.png)

If you start editing the JSON data on the right you should see errors if the data does not conform to the OpenAttestation v2.0 schema. A summary of the number of errors is found on top of the right panel and the details of the errors are found below the two panels.

### Creating raw document

To create data for your document, paste the following JSON data into the right panel of the JSON schema validator tool:

```json
{
  "$template": {
    "name": "main",
    "type": "EMBEDDED_RENDERER",
    "url": "https://tutorial-renderer.openattestation.com"
  },
  "recipient": {
    "name": "John Doe"
  },
  "issuers": [
    {
      "name": "Demo Issuer",
      "documentStore": "0xBBb55Bd1D709955241CAaCb327A765e2b6D69c8b",
      "identityProof": {
        "type": "DNS-TXT",
        "location": "few-green-cat.sandbox.openattestation.com"
      }
    }
  ]
}
```

To makes things simple, you will use an existing renderer at [here](https://tutorial-renderer.openattestation.com). However you will still need to replace the following values in your own document, including the issuer's document store and the identity proof location.

#### Replacing the issuer's document store

Replace the value of `issuers[0].documentStore` from `0xBBb55Bd1D709955241CAaCb327A765e2b6D69c8b` to the smart contract address of your document store in the [previous step](/docs/integrator-section/verifiable-document/ethereum/document-store).

#### Replacing the identity proof location

Replace the value of `issuers[0].identityProof.location` from `few-green-cat.sandbox.openattestation.com` to the dns name used to bind the document store's identity in the [previous step](/docs/integrator-section/verifiable-document/ethereum/dns-proof).

![Validator Completed](/docs/integrator-section/verifiable-document/ethereum/document-data/validator-completed.png)


### Verification
Once all the values are configured and the raw document conforms to the schema, you will see the message `No errors found. JSON validates against the schema`.

## Saving the raw document
To save the raw document:

1. At the same level with the `wallet.json` file, create a folder named `raw-documents`. 

2. Inside that folder create a file named `certificate-1.json` and paste the validated JSON from above.

3. Create another file named `certificate-2.json`. 

4. Paste the same validated JSON into the `certificate-2.json` file. Change the `recipient.name` to a different name.

  At this point in time, your directory should look like the following:

  ```text
  wallet.json
  raw-documents
    |-- certificate-1.json
    |-- certificate-2.json
  ```

  You are now ready to wrap the documents.