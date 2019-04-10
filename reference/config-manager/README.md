# Config Manager

## Components Configuration

All components configuration can be stored within common configuration. Betbook FE application is aware of specific sections in this configuration, that are being used for rendering UI components.

Here is a brief example of how this configuration might look like:

```javascript
{
  "brand": "com",
  "components": {
    "header": {
      "options": {
        "items": [
          {
            "id": "burger"
          },
          {
            "id": "search"
          }
        ]
      },
      "presets": [
        {
          "rules": {
            "user": {
              "isLoggedIn": true
            }
          },
          "options": {
            "items": [
              {
                "id": "burger"
              },
              {
                "id": "search"
              }
            ]
          }
        }
      ]
    }
  }
}
```

In general, the configuration structure should conform the following format:

```javascript
{
  "brand": "com",
  "components": {
    "fooComponent": { /* ... */ },
    "barComponent": { /* ... */ }
  }
}
```

Once the Betbook FE application is loaded, it gets the configuration from server and gets initialized with options, specified in this file. It resolves current brand by **brand** field, and uses **components** section to configure the UI components themselves.

Each component has its own code name \(e.g. **sportsNavigation**\), and it tries to get the configuration from the corresponding section.

All default configuration options are stored within **options** section and can have any structure, suitable for each particular component. For instance:

```javascript
"sportsNavigation": {
  "options": {
    "items": { /* ... */ },
    "titles": { /* ... */ },
    "devices": { /* ... */ }
  }
}
```

Besides this, each component can be configured differently for special cases \(e.g. for logged in users only\). Special section, called **presets** can be used to define a list of options and rules. Those rules are then get matched against current application state in a run-time and corresponding options are applied, overriding default ones. Here is an example:

```javascript
"sportsNavigation": {
  "options": {
    "background": "red",
  },
  "presets": [
    {
      "rules": {
        "user": {
          "isLoggedIn": true
        }
      },
      "options": {
        "background": "green"
      }
    },
    {
      "rules": {
        "user": {
          "age": 18
        }
      },
      "options": {
        "background": "yellow"
      }
    }
  ]
}
```

As you can see, you can have as much presets as you need. First matched preset will be picked in case of rules overlapping.

Currently Betbook FE application supports a single predicate only, that can be used for defining preset rules: **isLoggedIn**. Any other predicates can be added on-demand.

