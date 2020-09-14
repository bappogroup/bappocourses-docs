---
description: Code your own action and use in View Editor
---

# Coded Actions

You can create an action with Bappo's Coding Tool and use it within the Action Flow in View Editor. 

Below example creates a sample action, which takes `objectKey` as an option, and a `Record` typed parameter  named `item` .

#### 1. Create a Package and select "Action" as the Package Type in the Coding tool

You get `index.js` where you can code your function as action inside the `createFunction` method and `config.json` where you can define options and parameters this action can accept.

![](../.gitbook/assets/image%20%282%29.png)

#### 2. Code the action in `index.js`

Use the auto-generated template and code your component in the `createFunction` method. Here we just logs the `objectKey` and `item` the action received when executed:  

```text
const codedFunction = {
  createFunction: (context, options) => {
    const { objectKey } = options;

    return async function codedAction(props) {
      const { item } = props;

      console.log('object key:', objectKey);
      console.log('item', item)
    };
  },
};

export default codedFunction;
```

#### 3. Configure the action's `options` and `parameters`

Open `config.json`, add config for `objectKey` in options and config for `item` in parameters:

Difference between options and parameters:

* options: static values that already defined after designing the when
* parameters: might contain dynamic values\(e.g. the name of a record from the database\) that can only be determined during run-time

`optionTypes` is the type definition of the option and `defaultOptionConfigs` gives the option a default value. Similarly, `parameters` defines the props the component can receive and `defaultArgumentConfigs` gives the param a default value when executed in the Action Flow.

In this example we declare the action needs an option `objectKey` and a parameter `item`. The `config.json` now becomes:

```text
{
  "label": "Log Record",
  "optionTypes": {
    "objectKey": {
      "type": "BAPPO_OBJECT",
      "label": "Object"
    }
  },
  "defaultOptionConfigs": {
    "objectKey": {
      "configValueKind": "BAPPO_OBJECT",
      "objectKey": null
    }
  },
  "parameters": {
    "item": {
      "type": {
        "kind": "CREATE_RECORD_INPUT",
        "objectKey": {
          "referenceKind": "OptionReference",
          "optionName": "objectKey"
        }
      },
      "label": "Record"
    }
  },
  "defaultArgumentConfigs": {
    "item": {
      "configValueKind": "RECORD_VALUES",
      "objectKey": {
        "referenceKind": "OptionReference",
        "optionName": "objectKey"
      },
      "fieldValues": {}
    }
  },
  "returnType": {
    "kind": "RECORD",
    "objectKey": {
      "referenceKind": "OptionReference",
      "optionName": "objectKey"
    }
  }
}

```

Save and sync the package.

#### 4. Use the action in Action Flow, View Editor

Go to View Editor and create an Action Flow. Your coded action should appear in the Coded section in the left action panel. Drag it into the action flow to use it.

![coded action panel in Action Flow](../.gitbook/assets/image%20%283%29.png)

Options and props you declared in `config.json` should appear in the right-side panel and ready for you to configure. Select an object and specify some field values as the `item`.

Preview the view, execute the action flow, then `objectKey` and field values you specified should appear in console log.

