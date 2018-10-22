---
title: Layar API Reference

# language_tabs: # must be one of https://git.io/vQNgJ
#   - shell
#   - ruby
#   - python
#   - javascript

search: true
---

# Introduction

Layar API Documentation. WIP and Draft

Curl example WIP

# Dashboards

## Add a new dashboard

> Example paylaod

```json
{
  "dashboard": "android"
}
```

> Example Response

```json
{
  "status": "success"
}
```

`PUT /dashboard`


## Get all dashboard

> Example response

```json
{
  "dashboards": ["android", "IOS", "WEB", "android-TERA", "Backend-L&D"]
}
```

`GET /dashboard`

# Reports

## Add a new Report


> Example Payload

```json
{
  "dashboard": "android",
  "reportID": "pr-1410",
  "attributes": [
    {
      "key": "commitHash",
      "name": "Commit Hash",
      "value": "d6cd1e2bd19e03a81132a23b2025920577f84e37"
    },
    {
      "key": "branch",
      "name": "Branch",
      "value": "feature/test"
    },
    {
      "key": "target",
      "name": "Target",
      "value": "master"
    },
    {
      "key": "prLink",
      "name": "PR link",
      "value": "https://github.com/traveloka/android-v3/pull/1410"
    },
    {
      "key": "author",
      "name": "Author",
      "value": "fchristysen"
    }
  ],
  "sections": [
    {
      "sectionName": "app",
      "sectionHeader": [
        {
          "key": "apkSize",
          "name": "APK Size",
          "hint": "Appliction APK Size",
          "attributes": [
            {
              "key": "type",
              "name": "Threshold Type",
              "value": "lower"
            },
            {
              "key": "value",
              "name": "Threshold Value",
              "value": 50
            },
            {
              "key": "unit",
              "name": "Unit",
              "value": "%"
            },
            {
              "key": "bounds",
              "name": "Bounds",
              "value": [
                {
                  "key": "google",
                  "name": "Google Recomendation Size",
                  "value": 20000
                },
                {
                  "key": "alibaba",
                  "name": "Alibaba APK Size",
                  "value": 100000
                }
              ]
            }
          ]
        }
      ],
      "sectionDetail": [
        {
          "detailName": "GeneralApps",
          "tags": [],
          "reports": [
            {
              "headerKey": "apkSize",
              "value": 200,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "sectionName": "product",
      "sectionHeader": [
        {
          "key": "unitTestCoverage",
          "name": "Unit Test Coverage",
          "hint": "Unit test coverage",
          "attributes": [
            {
              "key": "type",
              "name": "Threshold Type",
              "value": "Higher"
            },
            {
              "key": "value",
              "name": "Threshold Value",
              "value": 50
            },
            {
              "key": "unit",
              "name": "Unit",
              "value": "%"
            },
            {
              "key": "bounds",
              "name": "Bounds",
              "value": [
                 {
                  "key": "google",
                  "name": "Google Recomendation Size",
                  "value": 20000
                },
                {
                  "key": "alibaba",
                  "name": "Alibaba APK Size",
                  "value": 100000
                }
              ]
            }
          ]
        }
      ],
      "sectionDetail": [
        {
          "detailName": "Flight",
          "tags": ["flight"],
          "reports": [
            {
              "headerKey": "unitTestCoverage",
              "value": 20,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            }
          ]
        },
        {
          "detailName": "Train",
          "tags": ["train"],
          "reports": [
            {
              "headerKey": "unitTestCoverage",
              "value": 30,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "sectionName": "screen",
      "sectionHeader": [
        {
          "key": "ttfi",
          "name": "Time to first interaction",
          "hint": "Interaction Time",
          "attributes": [
            {
              "key": "type",
              "name": "Threshold Type",
              "value": "Lower"
            },
            {
              "key": "value",
              "name": "Threshold Value",
              "value": 50
            },
            {
              "key": "unit",
              "name": "Unit",
              "value": "%"
            }
          ]
        },
        {
          "key": "fps",
          "name": "FPS",
          "hint": "Frame per second",
          "attributes": [
            {
              "key": "type",
              "name": "Threshold Type",
              "value": "higher"
            },
            {
              "key": "value",
              "name": "Threshold Value",
              "value": 60
            },
            {
              "key": "unit",
              "name": "Unit",
              "value": "frame"
            }
          ]
        }
      ],
      "sectionDetail": [
        {
          "detailName": "FlightSearch",
          "tags": ["flight", "search"],
          "reports": [
            {
              "headerKey": "ttfi",
              "value": 2000,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            },
            {
              "headerKey": "fps",
              "value": 40,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            }
          ]
        },
        {
          "detailName": "TrainSearch",
          "tags": ["train"],
          "reports": [
            {
              "headerKey": "ttfi",
              "value": 1000,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            },
            {
              "headerKey": "fps",
              "value": 30,
              "label": "",
              "status": "pass",
              "additionalValue": [
                {
                  "key": "excellenceIndex",
                  "name": "Excellence Index",
                  "value": 60
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}


```

This api is used for send report to layar dashboard <br>
Default behavior for this api is `upsert`

`POST /report`


| Payload    | required | Description                                                 |
| ---------- | -------- | ----------------------------------------------------------- |
| dashboard  | true     | Dashboard ID                                                |
| reportID   | false    | Custom report id, if not provided it will be auto generated |
| attributes | false    | List of [Attribute](#attribute) object                      |
| sections   | true     | List of [Section](#section) object                          |


> Example response

```json
{
  "reportID": "pr-1410",
  "status": "success"
}
```


# Standard Objects
## Attribute

```json
{
  "key": "commitHash",
  "name": "Commit Hash",
  "value": "d6cd1e2bd19e03a81132a23b2025920577f84e37"
}
```

| Payload | required | Description                                               |
| ------- | -------- | --------------------------------------------------------- |
| key     | true     | Attribute key,                                            |
| name    | true     | Attribute name, this fields will shown on dashboard label |
| value   | true     | Value to be shown on dashboard                            |

## Section

```json
{
  "sectionName": "app",
  "sectionHeader": [
    {
      "key": "ttfi",
      "name": "Time to first interaction",
      "hint": "Interaction Time",
      "attributes": [
        {
          "key": "type",
          "name": "Threshold Type",
          "value": "Lower"
        }
      ]
    }
  ],
  "sectionDetail": [
    {
      "detailName": "GeneralApps",
      "tags": [],
      "reports": [
        {
          "key": "apkSize",
          "value": 200,
          "additionalValue": [
            {
              "key": "ExcellenceIndex",
              "value": 60
            }
          ]
        }
      ]
    }
  ]
}
```

| Payload                  | required | Description                                      |
| ------------------------ | -------- | ------------------------------------------------ |
| sectionName              | true     | Section name                                     |
| sectionHeader            | true     | List of [Section Header](#section-header) Object |
| sectionDetail            | true     | List of section detail                           |
| sectionDetail.detailName | true     | Section detail name                              |
| sectionDetail.tags       | false    | List of `string` of tag name                     |
| sectionDetail.reports    | true     | List of [Report](#report) Object                 |

## Section Header

```json

{
  "key": "ttfi",
  "name": "Time to first interaction",
  "hint": "Interaction Time",
  "attributes": [
    {
      "key": "type",
      "name": "Threshold Type",
      "value": "Lower"
    }
  ]
}

```

| Payload    | required | Description                            |
| ---------- | -------- | -------------------------------------- |
| key        | true     | Header Key                             |
| name       | true     | Header Name                            |
| hint       | false    | Hint text for header                   |
| attributes | false    | List of [Attribute](#attribute) object |


## Report

```json
{
  "headerKey": "apkSize",
  "value": 200,
  "label": "This is whitlisted because of reschadule feature release",
  "status": "pass",
  "additionalValue": [
    {
      "key": "excellenceIndex",
      "value": 60,
      "name": "Excellence Index"
    }
  ]
}

```

| Payload         | required | Description                                                                                                                                                            |
| --------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| headerKey       | true     | Threshold key                                                                                                                                                          |
| value           | true     | Report main value                                                                                                                                                      |
| label           | false    | Label for showing label or notes                                                                                                                                       |
| status          | false    | One of this value [`pass`, `warning`, `fail`, `default`] default value is `default` and it will affect the metrix detail field color (green, yellow, red and no color) |
| additionalValue | false    | Additional value is list of [Attribute](#attribute) object. This value can be aggreate later on dashboard                                                              |
