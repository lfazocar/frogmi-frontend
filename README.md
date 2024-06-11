# GeoJSON API Frontend

This application retrieves earthquake data from the USGS feed and displays it in a user friendly manner

### Setup

The app fetches data via a GET request to `VITE_API_URL`/features?queryString and sends comments via a POST request to `VITE_API_URL`/features/:id/comments. Set up your environment variables accordingly to use with your own API.

### Expected response data structure

- GET request to API: 
```json
{
  "data": {
    [
      {
        "id": 1,
        "attributes": {
          "external_id": "string",
          "some_attribute": "string or object"
        }
      }
    ]
  },
  "links": {
    "external_link": "url string"
  },
  "pagination": {
    "current_page": 1,
    "total": 1,
    "per_page": 1
  }
}
```

- POST request to API:
```json
{
  "body": "string"
}
```

### Usage

Once you have your backend API and this app up and running you only need to input a page number, the number of features per page you want to see and mark the magnitudes to want to filter, if any, to query the API and fetch the relevant data.

### Created with

[Vite 5.1.6](https://vitejs.dev/)  
[Vue 3.4.21](https://vuejs.org/)  
[Pico CSS 2.0.6](https://picocss.com/)  
