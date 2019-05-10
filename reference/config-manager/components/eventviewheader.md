# EventViewHeader

## Configuration example

```javascript
"sportConfigurations": [
  {
    "feedSportId": "F",
    "backgroundUrl": "https://raw.githubusercontent.com/Krakke193/files/master/soccer.png",
    "sportName": "soccer"
  },
  {
    "feedSportId": "T",
    "backgroundUrl": "https://raw.githubusercontent.com/Krakke193/files/master/soccer.png",
    "sportName": "tennis"
  },
  {
    "feedSportId": "VB",
    "sportName": "volleyball"
  }
]
```

## Models description

### SportConfiguration

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| feedSportId | String | Yes | Sport ID from the Air Backend. |
| backgroundUrl | String | Yes | Desired background image URL for sport. |
| sportName | String | Yes | Will be **deprecated** soon. |

