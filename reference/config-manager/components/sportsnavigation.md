# SportsNavigation

### Configuration example

```javascript
"items": [
  {
    "feedId": "AF",
    "id": "american-football",
    "title": "American Football",
    "icon": "SI_AmFootball"
  },
  {
    "feedId": "BB",
    "id": "baseball",
    "title": "Baseball",
    "icon": "SI_Baseball"
  },
}
```

### Item model description

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| feedId | String | Yes | Feed model ID from Air Backend. |
| id | String | Yes | Internal ID used within Betbook FE application. |
| title | String | Yes | Custom title for sport to be displayed for the end-user. Can contain Locize key. |
| icon | String | Yes | Custom icon code. Available icon codes can be found here: TBD. |

