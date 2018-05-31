---
layout: post
title:  "API Documentation"
date:   2018-05-31 16:10:07 +0300
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
The API is structured as a *json<* web service and can be called through any library that supports the format.
**Basic example:**

```
GET
https://api.eventya.eu/v1.0/instance/resource.json?access_token=access_token
```



Resources
---
#### Profiles

```
GET
https://api.eventya.eu/v1.0/instance/profiles.json?access_token=access_token
```

#### output:
***

```JSON
{
  "id": "uid",
  "name": "Name of profile",
  "cover_url": "url",
  "logo_url": "url",
  "categories": [
    {
      "category": "Category"
    }
  ]
}
```

#### fields:
***


You can add an extra parameter `?fields=` to append additional nodes in your output.
These will apply depending on your instance's configuration:

`has_location_tags`

A set of city / country tags.
``` JSON
  "location_tags": [
    {
      "name": "Kinshasa",
      "country": "Democratic Republic of the Congo"
    }
  ]
```


`contact_details`

Details like email, phone number, website url.
``` JSON
  "contact_details": {
    "phone": "321321321",
    "contact_email": "aluca@i-consult.ro"
  }
```


`features`

Extra features depending on the configuration of each category of profiles.
``` JSON
  "features": [
    {
      "name": "Name of feature",
      "value": "Value"
    },
  ]
```


`location`

GPS coordontates and address of the profile.
``` JSON
  "location": {
    "lat": "latitude",
    "lng": "longitude",
    "address": "Address"
  }
```


`business_hours`

Opening and closing hours of the profile.
``` JSON
  "business_hours": [
    {
      "label": "Luni",
      "values": [
        [
          "11:00",
          "20:00"
        ]
      ]
    }
  ]
```


`tables`

Extra data associated with a profile.
``` JSON
  "tables": [
    {
      "name": "Name of table",
      "image_url": "url",
      "models": [
        {
          "count": 3,
          "name": "Name of model"
        }
      ]
    }
  ]
```
