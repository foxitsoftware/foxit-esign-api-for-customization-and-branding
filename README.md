# Customization and Branding with Foxit eSign APIs

Foxit eSign provides a range of customization and branding options through its APIs, enabling seamless integration into your applications. These APIs include a set of common parameters that can be easily added to API requests for customization, allowing you to tailor the user experience to match your application’s theme, workflow, and feature requirements.

## Embed Foxit eSign in Your Application or Website

Foxit eSign's Envelope and Template endpoints offer parameters that generate embeddable URLs. These URLs can be embedded within web applications using an iFrame or accessed directly via a browser, depending on how document sending or signing is integrated within your application.

There are two embeddable views available for integration:
1. **Embedded Signing View**
2. **Embedded Sending View**

### Embedded Signing View

The **Embedded Signing View** allows you to embed the document signing experience directly within your application or website. This view enables users to sign documents without leaving the platform, providing a seamless experience.

You can generate an embeddable URL for the signing view using the following endpoints:

#### **Envelope Endpoints:**
- `/folders/createfolder`
- `/folders/sendDraftFolder`
- `/folders/modifySharedFolder`

#### **Template Endpoints:**
- `/templates/createFolder`

**Parameters to Generate Embedded Signing View URL:**

To generate the Embedded Signing View URL, include the following parameters in your API request:
1. `createEmbeddedSigningSession`
2. `createEmbeddedSigningSessionForAllParties`

Set both parameters to *true* to receive the Embedded Signing View URL in the API response. The resulting URL will resemble this format:


```
https://{{HOST_NAME}}/embedded/embeddedsign?eetid={URL-ENCODED EMBEDDED-TOKEN}
```


**iFrame Example:** You can embed the Foxit eSign signing view within your application using an iFrame like this:
```html
<div style="height: 100%; width: 100%; overflow: auto;" data-role="content">
  <iframe id="esignIframe" src="[EMBED_SESSION_URL]" style="width: 99% !important; height: 99% !important; position: absolute;" frameborder="0"></iframe>
</div>
```

### Embedded Sending View 
The **Embedded Sending View** offers a document preparation interface that allows users to add fields to a document, manage signers, and send documents directly from within your application. This view is perfect for applications where users need to prepare documents for signature before sending.
Generate an embeddable URL for the sending view using the following endpoints: <br>
#### **Envelope Endpoints:**
- `/folders/createfolder`
- `/folders/modifySharedFolder`

#### **Template Endpoints:**
- `/templates/createFolder`

**Parameters to generate Embedded Sending View URL**<br>
To generate the Embedded Sending View URL, include the following parameter in your API request:<br>
 - `createEmbeddedSendingSession`


Set this parameter to true to receive the Embedded Sending View URL in the API response. The resulting URL will resemble this format:
```
 https://{{HOST_NAME}}/embedded/embeddedsend?eetid={URL-ENCODED-EMBEDDED-TOKEN}
 ```

 **iFrame Sample**: Embed Foxit eSign in your application using iFrame like:
 ```html
 <div style="height: 100%; width: 100%; overflow: auto;" data-role="content">
<iframe src="[EMBED_SESSION_URL]" style="width: 99% !important;height: 99% !important;position: absolute;" frameborder="0"></iframe>
</div>
```

## Email Templates for Personalized Email Notifications
Significantly improve the signer experience with Email Personalization. Select an Email Template for recipients with customized contents. These email templates can be sent to a specific recipient or group of recipients as invitaion notification utilizing Foxit eSign's API. 


The email templates can be customized at the account level from settings under "Email templates" tab.

<img src="email templates tab.png">

We provide customization of email content, logo, button color and email footer.

<img src="email customization features.png">

### Email Temaplate Id
Each email template created will have a unique Email Template id which will be used in the API request to add the email template.
<img src="email template id.png">
<br><br>
The endpoints which can access this feature are:

#### **Envelope Endpoints:**
- `/folders/createfolder`
- `/folders/sendDraftFolder`
- `/folders/modifySharedFolder`

#### **Template Endpoints:**
- `/templates/createFolder`

**Parameter to add Email template for personalized experience**<br>
Send a document with personalized email content using template email id by including the following parameter in your API request:<br>
 - `emailTemplateId`

Pass the particular email template id to use the email template other than the default email.<br>
Below is the sample of the personalized email sent to recipient:<br>
<img src="email personalization.png">

## Redirect Signers and Users to Custom Pages

Foxit eSign APIs offer the flexibility to redirect signers and users to custom pages at various stages of the document signing process. This feature allows companies to provide a seamless, tailored experience that aligns with their application’s theme and user journey.

### Redirect Signers to Custom Pages

Foxit eSign provides several API parameters to control the redirection of signers based on their actions in the embedded signing view. 

![Redirecting signers options](redirecting%20signers%20options.png)

In the embedded signing view, a signer can either eSign the document or choose other actions via the **"More Actions"** dropdown, which includes options like **Decline to Sign** or **Sign Later**. Based on the signer's selection, you can redirect them to custom pages:

1. **Redirect signers upon successfully signing the document.**
2. **Redirect signers when they select the *Decline to Sign* option from the *More Actions* dropdown.**
3. **Redirect signers when they choose the *Sign Later* option from the *More Actions* dropdown.**

This gives a full control over the post-signing user experience, ensuring a smooth and branded journey for customers/signers.

The endpoints which can access this feature are:

#### **Envelope Endpoints:**
- `/folders/createfolder`
- `/folders/sendDraftFolder`
- `/folders/modifySharedFolder`

#### **Template Endpoints:**
- `/templates/createFolder`

**Parameters to Redirect Signers**<br>
Send a document including the following parameters in your API request to redirect users in different scenarios:<br>
 - `signSuccessUrl` - Add the absolute URL for the custom landing page of a website/application, which the signer will be redirected to after **successfully signing** the folder in the embedded signing view.
 - `signDeclineUrl` - Add the absolute URL for the custom landing page of a website/application, which the signer will be redirected to if **declines** to sign the folder in the embedded signing view.
 - `signLaterUrl` - Add the absolute URL for the custom landing page of a website/application, which the signer will be redirected to if **chooses** to sign the folder later in the embedded signing view.
 - `signErrorUrl` - Add the absolute URL for the custom landing page of a website/application, which the user will be redirected to if **error** comes during signing the folder in the embedded signing view.

 **JSON Sample**: Please find the sample of `/folders/createfolder` endpoint. 
 ```JSON
 {
  "folderName": "Foxit eSign Contract.pdf",
  "fileNames": [
    "Foxit eSign Contract.pdf"
  ],
    "parties": [
    {
      "firstName": "M",
      "lastName": "H",
      "emailId": "spider.man@marvel.com",
      "permission": "FILL_FIELDS_AND_SIGN",
      "sequence": 1,
      "workflowSequence": 1,
      "allowNameChange": true
    }
  ],
  "processTextTags": true,
  "processAcroFields": true,
  "signSuccessUrl": "www.redirect-custom-success.com",
  "signDeclineUrl": "www.redirect-custom-decline.com",
  "signLaterUrl": "www.redirect-custom-later.com",
  "signErrorUrl": "www.redirect-custom-error.com"
}
```

For any queries and support, please contact:

[![Foxit eSign](/foxitsign_newlogo.png)](https://www.foxit.com/esign-pdf/api/)

Email us at support@foxitsoftware.com

 <center>2024 © Foxit Software Incorporated. All rights reserved.<center>

[Terms of Use](https://www.foxit.com/product/terms-of-service.html) | [Privacy Policy](https://www.foxit.com/company/privacy-policy.html) 
