---
title: API Reference

toc_footers:
  - <a href='http://co2signal.com/' target='_blank'>Sign Up for a Developer Key</a>
  - Questions? <a href='mailto:hello@tmrow.co'>Reach out to us</a>

search: true
---

# Introduction

Welcome to the CO2 Signal API! You can use our API to get access to information about

- where the electricity in a specific region comes from
- how it was produced
- how much carbon was emitted to produce it

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl 'https://api.co2signal.com/v1/latest?countryCode=DK'
  -H "Authorization: myapitoken"
```

> Make sure to replace `myapitoken` with your API key.

CO2 Signal uses API keys to allow access to the API. You can get an API key [here](http://www.co2signal.com).

CO2 Signal expects the API key to be included as a header in all requests to the server:

`auth-token: myapitoken`

<aside class="success">
You must replace <code>myapitoken</code> with your personal API key.
</aside>

# Routes

## Get latest by country code
```shell
curl 'https://api.co2signal.com/v1/latest?countryCode=FR'
  -H "Authorization: myapitoken"
```

> The above command returns JSON structured like this:

```json
{
    "countryCode": "FR",
    "data": {
        "carbonIntensity": 92.97078744790771,
        "datetime": "2017-02-09T08:30:00.000Z",
        "exchange": {
            "BE": 1011,
            "CH": -658,
            "DE": -735,
            "ES": 2466,
            "GB": 985,
            "IT": -1730
        },
        "fossilFuelPercentage": 12.028887656434616,
        "price": 70.97,
        "production": {
            "biomass": 776,
            "coal": 592,
            "gas": 8467,
            "hydro": 11226,
            "nuclear": 54085,
            "oil": 918,
            "solar": 926,
            "wind": 1490
        },
        "storage": {
            "hydro": 172
        }
    },
    "status": "ok",
    "units": {
        "carbonIntensity": "gCO2eq/kWh",
        "exchange": "MW",
        "price": "EUR/MWh",
        "production": "MW",
        "storage": "MW"
    }
}
```

This endpoint retrieves the last known state of a country.

### HTTP Request

`GET https://api.co2signal.com/v1/latest`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
countryCode | | two-letter iso country code

## Get latest by geographic coordinate

```shell
curl 'https://api.co2signal.com/v1/latest?lon=6.8770394&lat=45.9162776'
  -H "Authorization: myapitoken"
```

> The above command returns JSON structured like this:

```json
{
    "countryCode": "FR",
    "data": {
        "carbonIntensity": 93.0727344671727,
        "datetime": "2017-02-09T08:30:00.000Z",
        "exchange": {
            "BE": 986,
            "CH": -658,
            "DE": -735,
            "ES": 2466,
            "GB": 985,
            "IT": -1730
        },
        "fossilFuelPercentage": 12.032514442152996,
        "price": 70.97,
        "production": {
            "biomass": 776,
            "coal": 592,
            "gas": 8467,
            "hydro": 11226,
            "nuclear": 54085,
            "oil": 918,
            "solar": 926,
            "wind": 1490
        },
        "storage": {
            "hydro": 172
        }
    },
    "status": "ok",
    "units": {
        "carbonIntensity": "gCO2eq/kWh",
        "exchange": "MW",
        "price": "EUR/MWh",
        "production": "MW",
        "storage": "MW"
    }
}
```

This endpoint retrieves the last known state of the zone.
Currently we default to zones by country, but this will quickly evolve to be as granular as possible.

### HTTP Request

`GET https://api.co2signal.com/v1/latest`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
lon | | longitude
lat | | latitude


## Get history by country code
```shell
curl 'https://api.co2signal.com/v1/history?countryCode=FR'
  -H "Authorization: myapitoken"
```

> Compared to the /latest endpoint, this one returns a list instead of a single element.
 The above command returns JSON structured like this:

```json
{
    "countryCode": "FR",
    "data": [
      {
          "carbonIntensity": 93.0727344671727,
          "datetime": "2017-02-09T08:30:00.000Z",
          "exchange": {
              "BE": 986,
              "CH": -658,
              "DE": -735,
              "ES": 2466,
              "GB": 985,
              "IT": -1730
          },
          "fossilFuelPercentage": 12.032514442152996,
          "price": 70.97,
          "production": {
              "biomass": 776,
              "coal": 592,
              "gas": 8467,
              "hydro": 11226,
              "nuclear": 54085,
              "oil": 918,
              "solar": 926,
              "wind": 1490
          },
          "storage": {
              "hydro": 172
          }
      },
      ...
    ],
    "status": "ok",
    "units": {
        "carbonIntensity": "gCO2eq/kWh",
        "exchange": "MW",
        "price": "EUR/MWh",
        "production": "MW",
        "storage": "MW"
    }
}
```

This endpoint retrieves the states of the last 24h of a country.

### HTTP Request

`GET https://api.co2signal.com/v1/history`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
countryCode | | two-letter iso country code


## Get history by geographic coordinate

```shell
curl 'https://api.co2signal.com/v1/history?lon=6.8770394&lat=45.9162776'
  -H "Authorization: myapitoken"
```

> Compared to the /latest endpoint, this one returns a list instead of a single element.
 The above command returns JSON structured like this:

```json
{
    "countryCode": "FR",
    "data": [
      {
          "carbonIntensity": 93.0727344671727,
          "datetime": "2017-02-09T08:30:00.000Z",
          "exchange": {
              "BE": 986,
              "CH": -658,
              "DE": -735,
              "ES": 2466,
              "GB": 985,
              "IT": -1730
          },
          "fossilFuelPercentage": 12.032514442152996,
          "price": 70.97,
          "production": {
              "biomass": 776,
              "coal": 592,
              "gas": 8467,
              "hydro": 11226,
              "nuclear": 54085,
              "oil": 918,
              "solar": 926,
              "wind": 1490
          },
          "storage": {
              "hydro": 172
          }
      },
      ...
    ],
    "status": "ok",
    "units": {
        "carbonIntensity": "gCO2eq/kWh",
        "exchange": "MW",
        "price": "EUR/MWh",
        "production": "MW",
        "storage": "MW"
    }
}
```

This endpoint retrieves the states of the last 24h of a zone.
Currently we default to zones by country, but this will quickly evolve to be as granular as possible.

### HTTP Request

`GET https://api.co2signal.com/v1/latest`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
lon | | longitude
lat | | latitude

