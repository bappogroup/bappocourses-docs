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
For more details about the usePopup Form, please refer to the official [help document](https://bappogroup.github.io/bappo-developer-docs/docs/custom-view-popup.html#form)
{% endhint %}

## The Form Component \(bappo-components\)

The Form Component is part of bappo-components and can be used to embed a form into an existing view. This form cannot pop up as a modal form. As a rule, in Bappo, we normally code modal forms that pop up. However in some cases you might want to embed a form into a list page for instance. so that the user can add records or modify records in place. Example: A user list page, with a form at the bottom of the page that contains only one field \(email\) and a button for adding the user.

```text
import React, { useState } from "react";
import {
  View,
  Form,
  SubmitButton,
  Text,
  TextField,
  styled
} from "bappo-components";

export default () => {
  const [tasks, setTasks] = useState([]);

  return (
    <View style={{ padding: 50 }}>
      {tasks.map(taskName => (
        <Item>
          <Text>{taskName}</Text>
        </Item>
      ))}
      <Form onSubmit={data => setTasks([...tasks, data.taskName])}>
        {({ getFieldValue }) => {
          const userPref = getFieldValue("userPref");
          return (
            <React.Fragment>
              <Form.Field name="taskName" label="Task" component={TextField} />
              <SubmitButton text="Add Task" />
            </React.Fragment>
          );
        }}
      </Form>
    </View>
  );
};

const Item = styled(View)`
  justify-content: center;
  align-items: center;
  height: 40px;
  background-color: #f6f6f6;
  margin: 3px;
`;

```

In the example above, the form is embedded inside a list page. When the form is submitted, an Item is added to the list. This requires more coding than usePopup, but the form comes with more features, some of them:

1. You can embed other components inside the form
2. You have more control over styling, spacing and layout
3. Form fields can respond to the values, e.g. the list of states is based on the selected country
4. Form fields can hide themselves based on values of other fields

##  The ModalForm Component \(Bappo Component\)

The ModalForm component is similar to the Form component above, with the exception that it pops up as a modal form. 

```text
import React, { useState } from "react";
import {
  View,
  Form,
  ModalForm,
  Text,
  TextField,
  Button,
  styled
} from "bappo-components";

export default () => {
  const [tasks, setTasks] = useState([]);
  const [formVisible, setFormVisible] = useState(false);

  return (
    <View style={{ padding: 50 }}>
      <Tasks>{tasks.map(renderItem)}</Tasks>
      <Button text="Add Task" onPress={() => setFormVisible(true)} />
      {formVisible && (
        <ModalForm
          visible
          onSubmit={data => {
            setTasks([...tasks, data.taskName]);
            setFormVisible(false);
          }}
        >
          {({ getFieldValue }) => {
            return (
              <Form.Field name="taskName" label="Task" component={TextField} />
            );
          }}
        </ModalForm>
      )}
    </View>
  );
};

const Item = styled(View)`
  justify-content: center;
  align-items: center;
  height: 40px;
  background-color: #f6f6f6;
  margin: 3px;
`;

const Tasks = styled(View)`
  margin-bottom: 20px;
`;

const renderItem = taskName => (
  <Item>
    <Text>{taskName}</Text>
  </Item>
);
```

In the above example a list of tasks contains a modal form. When the user clicks on the "Add Task" button, the modal form will become visible and when the onSubmit function is executed the form becomes invisible again.

## Conditional Fields

Fields can be hidden/shown based on values of other fields. This can be done with the **Form** and **ModalForm** components.

```text
import React, { useState } from "react";
import { View, Form, TextField, SwitchField, Button } from "bappo-components";

export default () => {
  const [tasks, setTasks] = useState([]);
  const [formVisible, setFormVisible] = useState(false);

  return (
    <View style={{ padding: 50 }}>
      <Form>
        {{getFieldValue} => {
          const flagValue = getFieldValue("flag");
          actions.changeValue('flag', true);
          
          return (
            <>
              <Form.Field
                name="flag"
                label="Show Secret Field"
                component={SwitchField}
              />
              {flagValue && (
                <Form.Field
                  name="secret"
                  label="Secret Field"
                  component={TextField}
                />
              )}
            </>
          );
        }}
      </Form>
    </View>
  );
};
```

In the code example above, The Secret Text Field is only shown if the Flag Field is On.

## Dependant Fields

Field configurations can be dependant on values of other fields. For instance the State Selector can show a list of states based on the Country selection. This can be done with the **Form** and **ModalForm** components.

```text
import React, { useState } from "react";
import { View, Form, TextField, SwitchField, Button } from "bappo-components";

export default () => {
  const [tasks, setTasks] = useState([]);

  return (
    <View style={{ padding: 50 }}>
      <Form>
        {({ getFieldValue }) => {
          const topSecret = getFieldValue("topSecret");
          return (
            <>
              <Form.Field
                name="topSecret"
                label="Top Secret"
                component={SwitchField}
              />
              <Form.Field
                name="Comment"
                label={topSecret ? "Comment (Confidential)" : "Comment"}
                component={TextField}
              />
            </>
          );
        }}
      </Form>
    </View>
  );
};

```

In the above example the second field shows a different label depending on the value of the first field.

## Database Fields inside &lt;Form /&gt; and &lt;ModalForm /&gt;

As you would have noticed, the usePopup hook makes it easy to use forms with database fields in it. The Form and ModalForm components are part of the  bappo-components library, an open-source library that is not connected to the bappo database. However in the internal @bappo-sdk library there is a component called &lt;DatabaseField /&gt; that comes to the rescue. 

```text
import React, { useState } from "react";
import { View, Form, TextField, SwitchField, Button } from "bappo-components";
import { DatabaseField } from "@bappo/sdk";

export default () => {
  return (
    <View style={{ padding: 50 }}>
      <Form>
        {({ getFieldValue }) => {
          const topSecret = getFieldValue("topSecret");
          return (
            <>
              <DatabaseField
                objectKey="Invoice"
                fieldName="customer"
                label="Customer"
                name="customer_id"
              />
            </>
          );
        }}
      </Form>
    </View>
  );
};

```

In the example above the DatabaseField component renders the customer field on the Invoice Object.

## Methods in functional body

Apart from `getFieldValue` , you also have a bunch of other useful methods provided from the function param. An example is `actions.changeValue` . 

```text
{(params) => {
  console.log(params); // see a full list of available methods
  
  const { getFieldValue, actions } = params;
  
  // this programmatically changes the value of a field
  actions.changeValue(fieldName, newValue); 
  
  return (
    <>
      // form fields..
    </>
  );
}}
```



