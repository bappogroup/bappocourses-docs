# Types in Coded Component/Action's Config

For better code quality and less error during run-time, Bappo follows strict rules when it comes to the type of values. When you declare the options/props a coded component can accept, or the options/parameters a coded action can accept, you must specify the types.

The format in `component.json` for a coded component:

```text
{
  "optionTypes": {
    [optionName]: {
      "type": [BappoTypeKind],
      "label": Text,
      "canBeDeviceSpecific": Boolean,
      "section": [Section]
    }
  },
  "defaultOptionConfigs": {
    [optionName]: {
      "isDeviceSpecific": Boolean,
      "values": {
        "UNIVERSAL" or [Device Kind]: {
          "configValueKind": [ConfigKind],
          "value": [ConfigKindSpecificValue]
        }
      }
    }
  },
  "propTypes": {
    [propName]: {
      "type": [BappoTypeKind] or [CompositeKind],
      "label": Text,
      "canBeDeviceSpecific": Boolean,
      "section": [Section]
    }
  },
  "defaultPropConfigs": {
    [propName]: {
      "configValueKind": [ConfigKind],
      ...[ConfigKindSpecificValue]
    }
  }
}
```

The format in `config.json` for a coded action:

```text
{
  "optionTypes": {
    [optionName]: {
      "type": [BappoTypeKind],
      "label": Text,
    }
  },
  "defaultOptionConfigs": {
    [optionName]: {
      "configValueKind": [ConfigKind],
      ...[ConfigKindSpecificValue]
    }
  },
  "propTypes": {
    [propName]: {
      "type": [BappoTypeKind] or [CompositeKind],
      "label": Text,
      "canBeDeviceSpecific": Boolean,
      "section": [Section]
    }
  },
  "defaultPropConfigs": {
    [propName]: {
      "configValueKind": [ConfigKind],
      ...ConfigKindSpecificValue
    }
  }
}
```

Below lists available values in the square brackets. Or, jump to **Example** section for sample configs.

### Bappo Type Kind

```text
{
  /* Primitive runtime types */
  BOOLEAN,
  COLOR,
  DATE,
  DATE_TIME,
  EMAIL,
  ICON,
  MONTH,
  NUMBER,
  PHONE_NUMBER,
  TEXT,
  TIME,
  YEAR,

  /* Function runtime types */
  CALLBACK_FUNCTION,

  /* Runtime types inferred from App definition */
  CREATE_RECORD_INPUT,
  EXTERNAL_FORM_VALUES,
  FIXED_LIST,
  FORM_RESULT,
  FORM_VALUES,
  PAGE_PARAM_VALUES,
  RECORD,
  RECORD_ID,
  UPDATE_RECORD_INPUT,
  READ_RECORD_INPUT,

  /* Types for static values */
  BAPPO_FORM,
  BAPPO_OBJECT,
  BAPPO_OBJECT_FIELD,
  BAPPO_PAGE,
  BORDER_RADIUS,
  COLUMN_COUNT,
  COLUMN_LAYOUT,
  DATA_VISUALIZATION_ELEMENT_ID,
  DATA_VISUALIZATION_PRESETS,
  ELEMENTS,
  EXTERNAL_FORM_FIELD,
  LOCAL_FIXED_LIST,
  PADDINGS,
  MARGINS,
  RECORD_ATTRIBUTES_FIELDS,
  SPACING,
  SPACING_SINGLE,
  VIEW_STATE_VARIABLE,

  /* Alias types */
  EXTERNAL_FORM_FIELD_VALUE,
  FORM_FIELD_VALUE,
  RECORD_FIELD_VALUE,

  /* Empty type */
  EMPTY,
}
```

### Config Kind

```text
{
  /* Static primitive values */
  /**
   * Represents no value or empty value.
   * At runtime, it will be converted to `null`.
   */
  EMPTY = 'EMPTY',
  /**
   * `true` or `false`.
   * At runtime, it will be converted to a JavaScript boolean.
   */
  STATIC_BOOLEAN = 'STATIC_BOOLEAN',
  /**
   * A static color value.
   * At runtime, it will be converted to a JavaScript string that's compatible
   * with CSS.
   */
  STATIC_COLOR = 'STATIC_COLOR',
  /**
   * A static date value.
   * At runtime, it will be converted to a JavaScript string in YYYY-MM-DD
   * format.
   */
  STATIC_DATE = 'STATIC_DATE',
  /**
   * A static date and time value.
   * At runtime, it will be converted to a JavaScript number.
   */
  STATIC_DATE_TIME = 'STATIC_DATE_TIME',
  /**
   * A static email value.
   * At runtime, it will be converted to a JavaScript string.
   */
  STATIC_EMAIL = 'STATIC_EMAIL',
  /**
   * The value of one of the fixed list options.
   * At runtime, it will be converted to a JavaScript string.
   */
  STATIC_FIXED_LIST_VALUE = 'STATIC_FIXED_LIST_VALUE',
  /**
   * A static icon value.
   * At runtime, it will be converted to a JavaScript string that's compatible
   * with the Icon component.
   */
  STATIC_ICON = 'STATIC_ICON',
  /**
   * A static month value.
   * At runtime, it will be converted to a JavaScript number.
   */
  STATIC_MONTH = 'STATIC_MONTH',
  /**
   * A number literal.
   * At runtime, it will be converted to a JavaScript number.
   */
  STATIC_NUMBER = 'STATIC_NUMBER',
  /**
   * A static phone number value.
   * At runtime, it will be converted to a JavaScript string.
   */
  STATIC_PHONE_NUMBER = 'STATIC_PHONE_NUMBER',
  /**
   * A string literal.
   * At runtime, it will be converted to a JavaScript string.
   */
  STATIC_TEXT = 'STATIC_TEXT',
  /**
   * A static time value.
   * At runtime, it will be converted to a JavaScript string in HH:mm:ss format.
   */
  STATIC_TIME = 'STATIC_TIME',
  /**
   * A static year value.
   * At runtime, it will be converted to a JavaScript number.
   */
  STATIC_YEAR = 'STATIC_YEAR',

  /* Formula */
  /**
   * At runtime, the variables it references will be replaced their runtime
   * values.
   */
  DYNAMIC_STRING = 'DYNAMIC_STRING',
  /**
   * A formula.
   * At runtime, the formula will be executed to compute the runtime value.
   */
  FORMULA = 'FORMULA',

  /* Complex values */
  /**
   * Reference to an action flow.
   */
  ACTION_FLOW = 'ACTION_FLOW',
  /**
   * A list of elements.
   * At runtime, it will be converted to React elements.
   */
  ELEMENTS = 'ELEMENTS',
  /**
   * A set of key-value pairs that represents values of a form.
   */
  FORM_VALUES = 'FORM_VALUES',
  /**
   * A set of key-value pairs that can be passed to a page as params.
   */
  PAGE_PARAM_VALUES = 'PAGE_PARAM_VALUES',
  /**
   * A set of key-value pairs that represents a record in the database.
   */
  RECORD_VALUES = 'RECORD_VALUES',

  /* Reference to the value of a variable in the scope */
  /**
   * Reference to the value of an action flow input.
   * At runtime, it will be replaced by the runtime value of the referenced
   * action flow input.
   */
  ACTION_FLOW_INPUT_VALUE = 'ACTION_FLOW_INPUT_VALUE',
  /**
   * Reference to the value of an activity result.
   * At runtime, it will be replaced by the runtime value of the referenced
   * activity result.
   */
  ACTIVITY_RESULT_VALUE = 'ACTIVITY_RESULT_VALUE',
  /**
   * Reference to the value of a callback parameter.
   * At runtime, it will be replaced by the runtime value of the referenced
   * callback parameter.
   */
  CALLBACK_PARAMETER_VALUE = 'CALLBACK_PARAMETER_VALUE',
  /**
   * Reference to a single record.
   * At runtime, the system will take care of fetching the record through the
   * data layer and it will be replaced by the record as a JavaScript object.
   */
  SINGLE_RECORD_DATA_SOURCE = 'SINGLE_RECORD_DATA_SOURCE',
  /**
   * Reference to the value of a view param.
   * At runtime, it will be replaced by the runtime value of the referenced
   * prop.
   */
  VIEW_PARAM_VALUE = 'VIEW_PARAM_VALUE',
  /**
   * Reference to a view state variable.
   * At runtime, it will be replaced by the runtime value of the referenced
   * state.
   */
  VIEW_STATE_VARIABLE_VALUE = 'VIEW_STATE_VARIABLE_VALUE',
  /**
   * Reference to an activity option metadata, e.g. singular name of an object
   * in the options of an activity.
   * At runtime, it will be replaced by the runtime value of the referenced
   * value as a JavaScript string.
   */
  ACTIVITY_OPTION_METADATA = 'ACTIVITY_OPTION_METADATA',
  /**
   * Reference to an element option metadata, e.g. singular name of an object
   * in the options of an element.
   * At runtime, it will be replaced by the runtime value of the referenced
   * value as a JavaScript string.
   */
  ELEMENT_OPTION_METADATA = 'ELEMENT_OPTION_METADATA',

  /* Design time only. Only use them in option configs. */
  /**
   * Border radius values for all sides.
   */
  BORDER_RADIUS = 'BORDER_RADIUS',
  /**
   * Local fixed list value.
   */
  LOCAL_FIXED_LIST_VALUE = 'LOCAL_FIXED_LIST_VALUE',
  /**
   * Paddings for all sides.
   */
  PADDINGS = 'PADDINGS',
  /**
   * Margins for all sides.
   */
  MARGINS = 'MARGINS',
  /**
   * Margins and paddings for all sides.
   */
  SPACING = 'SPACING',
  /**
   * Margin or padding for one side.
   */
  SPACING_SINGLE = 'SPACING_SINGLE',

  /* Internal use only. Cannot be used in custom coded components. */
  /**
   * Reference to a Bappo form view.
   */
  BAPPO_FORM = 'BAPPO_FORM',
  /**
   * Reference to a Bappo object.
   */
  BAPPO_OBJECT = 'BAPPO_OBJECT',
  /**
   * Reference to a Bappo object field.
   */
  BAPPO_OBJECT_FIELD = 'BAPPO_OBJECT_FIELD',
  /**
   * Reference to a Bappo page.
   */
  BAPPO_PAGE = 'BAPPO_PAGE',
  /**
   * Data structure for the Columns component.
   */
  COLUMN_COUNT = 'COLUMN_COUNT',
  /**
   * Data structure for the Columns component.
   */
  COLUMN_LAYOUT = 'COLUMN_LAYOUT',
  /**
   * Reference to a DataVisualization element.
   */
  DATA_VISUALIZATION_ELEMENT_ID = 'DATA_VISUALIZATION_ELEMENT_ID',
  /**
   * Data structure for the DataVisualization component.
   */
  DATA_VISUALIZATION_PRESETS = 'DATA_VISUALIZATION_PRESETS',
  /**
   * Reference to a field in a published form.
   */
  EXTERNAL_FORM_FIELD = 'EXTERNAL_FORM_FIELD',
  /**
   * Data structure for the RecordAttributes component.
   */
  RECORD_ATTRIBUTES_FIELDS = 'RECORD_ATTRIBUTES_FIELDS',
  /**
   * Reference to a state variable.
   * Note that this refers to the variable itself rather than its runtime value.
   * For example, in the SetVariable action you will let the user pick which
   * variable should be updated.
   */
  VIEW_STATE_VARIABLE = 'VIEW_STATE_VARIABLE',
}
```

### Section

```text
{
  NONE = 'None',
  LAYOUT = 'Layout',
  SIZE = 'Size',
  SPACING = 'Spacing',
  BORDERS = 'Borders',
  VISIBILITY = 'Visibility',
  BACKGROUNDS = 'Backgrounds',
  TYPOGRAPHY = 'Typography',
  CONTENT = 'Content',
  GENERAL = 'General',
  DATA = 'Data',
  EVENTS = 'Events',
}
```

### Device Kind

```text
{
  DESKTOP = 'DESKTOP', // 992+ pixels
  TABLET = 'TABLET', // 768-991 pixels
  LARGE_PHONE = 'LARGE_PHONE', // 480-767 pixels
  PHONE = 'PHONE', // 240-479 pixels
  UNIVERSAL = 'UNIVERSAL', // Not device specific
}
```

### Examples

1. In `config.json` for a coded action,  declare two `message` params - one static and another dynamic, when executed in action flow:

```text
{
  "parameters": {
    "messageStatic": {
      "type": "TEXT",
      "label": "Message Static"
    },
    "messageDynamic": {
      "type": "TEXT",
      "label": "Message Dynamic"
    }
  },
  "defaultArgumentConfigs": {
    "messageStatic": {
      "configValueKind": "STATIC_TEXT",
      "value": ""
    },
    "messageDynamic": {
      "configValueKind": "DYNAMIC_STRING",
      "ast": {
        "function": "@bappo/concat",
        "argumentConfigs": [
          {
            "configValueKind": "STATIC_TEXT",
            "value": ""
          }
        ]
      }
    }
  }
}
```

