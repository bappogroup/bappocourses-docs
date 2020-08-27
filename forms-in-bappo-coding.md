---
description: There are basically three ways to create forms in Bappo Coding
---

# Forms in Bappo Coding

<table>
  <thead>
    <tr>
      <th style="text-align:left">The three ways</th>
      <th style="text-align:left">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">The usePopup Hook</td>
      <td style="text-align:left">
        <p>Very quick and easy Modal (Popup) Form</p>
        <p>Limited flexibility</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">The Form Component</td>
      <td style="text-align:left">
        <p>For embedding a form inside an existing view</p>
        <p>Very flexible and powerful, but more coding required than usePopup</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">The ModalForm Component</td>
      <td style="text-align:left">Sophisticated Modal (Popup) Form.
        <br />Very flexible and powerful, but more coding required than usePopup</td>
    </tr>
  </tbody>
</table>

## usePopup

```text
import {usePopup} from "@bappo/sdk";

const popup = usePopup();

....

popup.form({
  objectKey: 'Contact',
  fields: ['name', 'email'],
  async onSubmit(contact) {
    await Contact.create(contact);
  },  
});
```

In the above example a popup form will appear for the Contact object, with a name and an email address

```text
import {usePopup} from "@bappo/sdk";

const popup = usePopup();

...

popup.form({
  formKey: 'NocodeContactForm',
  async onSubmit(contact) {
    await Contact.create(contact);
  },
});
```

In the above example a form that was defined in the nocode view editor will open up as a popup.

{% hint style="info" %}
For more details please refer to the official [help document](https://bappogroup.github.io/bappo-developer-docs/docs/custom-view-popup.html#form)
{% endhint %}



