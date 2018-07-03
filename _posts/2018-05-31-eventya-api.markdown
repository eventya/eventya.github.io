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
      "id": 3,
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

#### filters:
***

You can filter the list of results by setting the parameter `?filter=`.
Below are a list of available filters:

`with_location_tag id_of_location_tag`

Example of usage: `?filter=with_location_tag 3` It will give you a list of Profiles that are related to the location-tag with id 3.

---
#### Location Tag

```
GET
https://api.eventya.eu/v1.0/instance/location_tags.json?access_token=access_token
```

#### output:

```json
{
  "countries": [
    {
      "name": "Name of country",
      "cities": [
        {
          "id": 3,
          "name": "Name of city"
        }
      ]
    }
  ]
}
```
