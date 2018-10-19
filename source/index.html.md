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
      "sectionDetail": [
        {
          "detailName": "GeneralApps",
          "tags": [],
          "reports": [
            {
              "thresholdId": "apkSize",
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
      "sectionDetail": [
        {
          "detailName": "Flight",
          "tags": ["flight"],
          "reports": [
            {
              "thresholdId": "unitTestCoverage",
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
              "thresholdId": "unitTestCoverage",
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
      "sectionDetail": [
        {
          "detailName": "FlightSearch",
          "tags": ["flight", "search"],
          "reports": [
            {
              "thresholdId": "ttfi",
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
              "thresholdId": "fps",
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
              "thresholdId": "ttfi",
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
              "thresholdId": "fps",
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
Default behavior for this api is upsert

`PUT /report`


| Payload    | required | Description                                                 |
|------------|----------|-------------------------------------------------------------|
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


# Thresholds

## Add a Threshold

`PUT /threshold`

> Example Paylaod

```json
{
  "dashboard": "android",
  "section": "app",
  "thresholdId": "apkSize",
  "thresholdName": "APK Size",
  "thresholdType": "Lower",
  "thresholdValue": 30000,
  "unit": "KB",
  "bounds": [
    {
      "key": "Google Recomendation Size",
      "value": 20000
    },
    {
      "key": "Alibaba APK Size",
      "value": 100000
    }
  ]
}
```

| Payload        | required | Description                                                        |
|----------------|----------|--------------------------------------------------------------------|
| dashboard      | true     | One of [Dashboard](#get-all-dashboard)                             |
| section        | true     | Section name                                                       |
| thresholdId    | true     | Threshold id                                                       |
| thresholdName  | true     | Threshold name                                                     |
| thresholdType  | true     | Threshold type is one of this value `["Lower", "Higher", "Equal"]` |
| thresholdValue | true     | Threshold value                                                    |
| unit           | false    | Threshold unit                                                     |
| bounds         | false    | List of [Attribute](#attribute) object                             |


## Get Thresholds by dashboard name

`GET /threshold?dashboard=android`

> Example response

```json
{
  "sections": [
    {
      "sectionName": "app",
      "thresholds": [
        {
          "thresholdId": "apkSize",
          "thresholdName": "APK Size",
          "thresholdType": "Lower",
          "thresholdValue": 30000,
          "unit": "KB",
          "bounds": [
            {
              "key": "googleSize",
              "name": "Google Recomendation Size",
              "value": 20000
            },
            {
              "key": "alibabaAPKSize",
              "name": "Alibaba APK Size",
              "value": 100000
            }
          ]
        },
        {
          "thresholdId": "assetSize",
          "thresholdName": "Asset Size",
          "thresholdType": "Lower",
          "thresholdValue": 3000,
          "unit": "KB",
          "bounds": []
        }
      ]
    },
    {
      "sectionName": "product",
      "thresholds": [
        {
          "thresholdId": "unitTestCoverage",
          "thresholdName": "Unit Test Coverage",
          "thresholdType": "Higher",
          "thresholdValue": 50,
          "unit": "%",
          "bounds": []
        }
      ]
    },
    {
      "sectionName": "screen",
      "thresholds": [
        {
          "thresholdId": "ttfi",
          "thresholdName": "Time to first interaction",
          "thresholdType": "Lower",
          "thresholdValue": 200,
          "unit": "ms",
          "bounds": []
        },
        {
          "thresholdId": "fps",
          "thresholdName": "Frame per second",
          "thresholdType": "Higher",
          "thresholdValue": 60,
          "unit": "frame",
          "bounds": []
        },
        {
          "thresholdId": "noWarning",
          "thresholdName": "No lint Warning",
          "thresholdType": "Equal",
          "thresholdValue": true,
          "unit": "",
          "bounds": []
        }
      ]
    }
  ]
}
```

## Get Thresholds by section & dashboard

`GET /threshold?dashboard=android&section=app`

> Example response

```json
{
  "sections": [
    {
      "sectionName": "app",
      "thresholds": [
        {
          "thresholdId": "apkSize",
          "thresholdName": "APK Size",
          "thresholdType": "Lower",
          "thresholdValue": 30000,
          "unit": "KB",
          "bounds": [
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
        },
        {
          "thresholdId": "assetSize",
          "thresholdName": "Asset Size",
          "thresholdType": "Lower",
          "thresholdValue": 3000,
          "unit": "KB",
          "bounds": []
        }
      ]
    }
  ]
}
```

## Update Thresholds

//TODO


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
|---------|----------|-----------------------------------------------------------|
| key     | true     | Attribute key,                                            |
| name    | true     | Attribute name, this fields will shown on dashboard label |
| value   | true     | Value to be shown on dashboard                            |

## Section

```json
{
  "sectionName": "app",
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

| Payload                  | required | Description                      |
|--------------------------|----------|----------------------------------|
| sectionName              | true     | Section name                     |
| sectionDetail            | true     | List of section detail           |
| sectionDetail.detailName | true     | Section detail name              |
| sectionDetail.tags       | false    | List of `string` of tag name     |
| sectionDetail.reports    | true     | List of [Report](#report) Object |


## Report

```json
{
  "key": "apkSize",
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

| Payload         | required | Description                                                                                                                                                        |
|-----------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| key             | true     | Threshold key                                                                                                                                                      |
| value           | true     | Report main value                                                                                                                                                  |
| label           | false    | Label for showing label or notes                                                                                                                                   |
| status          | false    | One of this value [`pass`, `warning`, `fail`, `default`] default value is `default` and it will affect the metrix detail field color (green, yellow, red,no color) |
| additionalValue | false    | Additional value is list of [Attribute](#attribute) object. This value can be aggreate later on dashboard                                                          |
