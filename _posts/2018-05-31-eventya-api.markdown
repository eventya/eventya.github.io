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
The API is structured as a *json* web service and can be called through any library that supports the format.

#### Basic example:

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

```json
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

#### pagination:
***
If there are multiple pages of results you can browse by adding the parameter `?page=`.
The value of the parameter must be an integer of at least `1`.


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


`gallery`

Gallery of images of the profile.
``` json
  "gallery": [
    {
      "url": "url"
    }
  ]
```


`location_tags`

A set of city / country tags.
``` json
  "location_tags": [
    {
      "name": "Kinshasa",
      "country": "Democratic Republic of the Congo"
    }
  ]
```


`contact_details`

Details like email, phone number, website url.
``` json
  "contact_details": {
    "phone": "321321321",
    "contact_email": "aluca@i-consult.ro"
  }
```


`features`

Extra features depending on the configuration of each category of profiles.
``` json
  "features": [
    {
      "name": "Name of feature",
      "value": "Value"
    },
  ]
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


`business_hours`

Opening and closing hours of the profile.
``` json
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
``` json
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
