---
layout: post
title:  "Eventys API Documentation"
date:   2023-03-06 11:10:07 +0300
categories: api
---

The Basics
---
The API is built in a *RESTful* way, it's endpoints consists of:
- **instance**: The name of the bucket of content. (can be obtain by contacting us)
- **resource**: The type of content.
- **access_token**: Secure encrypted token with which you can access the data. (can be obtain by contacting us)
- **version**: Version of the API.

Structure
---
The API is structured as a *json* web service and can be called through any library that supports the format.

#### Basic example:

```
GET
https://api.eventya.eu/v1.0/instance/resource.json?access_token=access_token
```



Resources
---
#### Events

```
GET
https://api.eventya.eu/v1.0/instance/events.json?access_token=access_token
```

#### output:

```json
{
  "id": "uid",
  "name": "Name of event",
  "cover_url": "url",
  "categories": [
    {
      "category": "Category"
    }
  ],
  "date": {
    "start_at": "timestamp",
    "end_at": "timestamp"
  }
}
```

#### pagination:
***
If there are multiple pages of results you can browse by adding the parameter `?page=`.
The value of the parameter must be an integer of at least `1`.

You can specify how many items per page there can be using `?per_page=`.
The maximum allowed number is 10.


#### fields:
***


You can add an extra parameter `?fields=` to append additional nodes in your output.
Multiple field values can be added separated by `,`.
These will apply depending on your instance's configuration:

`description`

Description of the profile.
``` json
  "description": "The description"
```


`location`

GPS coordontates and address of the profile.
``` json
  "location": {
    "lat": "latitude",
    "lng": "longitude",
    "address": "Address"
  }
```


#### filters:
***

You can filter the list of results by setting the parameter `?filter=`.
Below are a list of available filters:

`past`

Example of usage: `?filter=past` It will give you a list of Eventys that are have been completed

---
