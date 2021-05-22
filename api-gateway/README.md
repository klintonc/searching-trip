# API Gateway

Express server that searches trips from the data source (`json-server`) and returns paginated results.

## Run

Start `json-server` first, then:

```bash
cp .env.example .env
yarn install
yarn dev
```

The gateway runs on port `4000` by default. Example requests are in [`API_GATEWAY.http`](./API_GATEWAY.http).

## Endpoints

### `GET /api/v1/trip`

Returns a paginated list of trips matching the keyword.

| Query     | Type   | Default | Description             |
| --------- | ------ | ------- | ----------------------- |
| `page`    | number | `1`     | Page number             |
| `limit`   | number | `2`     | Trips per page          |
| `keyword` | string |         | Search keyword (optional) |

```http
GET /api/v1/trip?page=1&limit=2&keyword=ธรรมชาติ
```

```json
{
  "tripList": [
    {
      "eid": "6",
      "title": "...",
      "url": "...",
      "description": "...",
      "photos": ["..."],
      "tags": ["ทะเล", "เกาะ", "ธรรมชาติ"]
    }
  ],
  "metadata": {
    "totalPage": 4
  }
}
```

### `GET /api/v1/trip/suggestion`

Returns all trips matching the keyword, without pagination. Used for search suggestions.

| Query     | Type   | Description    |
| --------- | ------ | -------------- |
| `keyword` | string | Search keyword |

```http
GET /api/v1/trip/suggestion?keyword=ธรรมชาติ
```

```json
{
  "suggestionTrips": [
    { "eid": "1", "title": "...", "url": "...", "description": "...", "photos": ["..."], "tags": ["..."] }
  ]
}
```

### Errors

On failure, both endpoints respond with status `500` and `{ "message": ... }`.
