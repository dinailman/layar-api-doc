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

# Dashboards

## Add a new dashboard

`PUT /dashboard`

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

## Get all dashboard

`GET /dashboard`

> Example response

```json
{
  "dashboards": ["android", "IOS", "WEB", "android-TERA", "Backend-L&D"]
}
```

# Reports

## Add a new Report

This api is used for send report to layar dashboard <br>

`PUT /report`

> Example Payload
> `CustomID` in this case is combination of string `pr-` and PR number

```json
{
  "dashboard": "android",
  "attributes": [
    {
      "key": "commitHash",
      "value": "d6cd1e2bd19e03a81132a23b2025920577f84e37"
    },
    {
      "key": "branch",
      "value": "feature/test"
    },
    {
      "key": "target",
      "value": "master"
    },
    {
      "key": "prLink",
      "value": "https://github.com/traveloka/android-v3/pull/1410"
    },
    {
      "key": "author",
      "value": "fchristysen"
    }
  ],
  "useCustomID": "true",
  "customID": "pr-1410",
  "sections": [
    {
      "sectionName": "app",
      "sectionDetail": [
        {
          "detailName": "GeneralApps",
          "reports": [
            {
              "key": "apkSize",
              "value": 200,
              "tags": []
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
          "reports": [
            {
              "key": "unitTestCoverage",
              "value": 20,
              "tags": ["flight"]
            }
          ]
        },
        {
          "detailName": "Train",
          "reports": [
            {
              "key": "unitTestCoverage",
              "value": 30,
              "tags": ["train"]
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
          "reports": [
            {
              "key": "ttfi",
              "value": 2000,
              "tags": ["flight", "ttfi"]
            },
            {
              "key": "fps",
              "value": 40,
              "tags": ["flight", "fps"]
            }
          ]
        },
        {
          "detailName": "TrainSearch",
          "reports": [
            {
              "key": "ttfi",
              "value": 1000,
              "tags": ["flight", "ttfi"]
            },
            {
              "key": "fps",
              "value": 30,
              "tags": ["flight", "fps"]
            }
          ]
        }
      ]
    }
  ]
}
```

> Example response
> If `useCustomID` value is `true`, reportID will generate using `customID` value with `dashboard` name as prefix, if `customID` key already defind on DB, it will be overwritten

```json
{
  "reportID": "android-pr-1410",
  "status": "success"
}
```

## Update a report

This api is used for Update a report and it will upsert the data<br>

`POST /report`

> Example Payload

```json
{
  "reportID": "android-pr-1410",
  "sections": [
    {
      "sectionName": "app",
      "sectionDetail": [
        {
          "detailName": "GeneralApps",
          "reports": [{ "key": "assetSize", "value": 3000 }]
        }
      ]
    }
  ]
}
```

> Example Response

```json
{
  "reportID": "android-pr-1410",
  "status": "success"
}
```

# Thresholds

## Add a Threshold

`thresholdType` is one of this value `["Lower", "Higher", "Equal"]`
if all of this fields `dashboard`, `section` and `thresholdID` are found on DB, it will overwritten the old value.

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
              "key": "Google Recomendation Size",
              "value": 20000
            },
            {
              "key": "Alibaba APK Size",
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
          "thresholdType": "Lower",
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
              "key": "Google Recomendation Size",
              "value": 20000
            },
            {
              "key": "Alibaba APK Size",
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

# Threshold whitelist

//TODO
