# MarketFilters

## Configuration example

```javascript
"availableMarkets": [
  {
    "value": "two-way",
    "label": "Two-way",
    "filter": {
      "marketKind": 1,
      "periods": 0,
      "resultKind": 1
    },
    "headings": [
      "Win1",
      "Win2"
    ]
  },
  {
    "value": "three-way",
    "label": "Three-way",
    "filter": {
      "marketKind": 2,
      "periods": 0,
      "resultKind": 1
    },
    "headings": [
      "Win1",
      "X",
      "Win2"
    ]
  }
},
"prematch": {
  "soccer": [
    "three-way",
    "double-chances"
  ],
  "tennis": [
    "two-way"
  ],
  "default": [
    "three-way"
  ]
},
"live": {
  "volleyball": [
    "two-way"
  ],
  "basketball": [
    "three-way"
  ],
  "default": [
    "three-way"
  ]
}
```

## Models description

### AvailableMarket

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| value | String | Yes | Internal market code used by Betbook FE application. |
| label | String | Yes | Custom market name to be displayed in the markets list. Locize key can be used a a value. |
| filter | Object | Yes | A set of fields \(**marketKind**, **periods** and **resultKind**\) that will be matched against the sport markets |
| headings | Array | Yes | Custom market headings for each column. Locize key can be used a a value. |

### Prematch

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| {sportId} | Array | Yes | Contains a list of market IDs, that should be enabled for a particular sport specified with {sportId}. Possible market IDs are defined in AvailableMarkets model. **default** section represents a list of markets, that should be available for all other sports. |

### Live

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| {sportId} | Array | Yes | Contains a list of market IDs, that should be enabled for a particular sport specified with {sportId}. Possible market IDs are defined in AvailableMarkets model. **default** section represents a list of markets, that should be available for all other sports. |

