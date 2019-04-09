# TabPanel

## Configuration example

```javascript
{
  "tabs": [
    {
      "id": "scoreboard",
      "icon": "AI_Scoreboard"
    },
    {
      "id": "video",
      "icon": "AI_Video"
    }
  ],
  "defaultTabId": "scoreboard"
}
```

## Model description

### Options

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| tabs | Array | Yes | A list of available tabs to be displayed for the end-user. |
| defaultTabId | String | Yes | ID of the tab, that should be activated by default. |

### Tab

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| id | String | Yes | Internal tab ID, used by Betbook FE application. |
| icon | String | Yes | Custom icon code for the tab. TBD. |

