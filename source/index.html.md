---
title: API Reference

toc_footers:
  - <a href='https://www.co2signal.com/' target='_blank'>Sign Up for a Developer Key</a>
  - Questions? <a href='mailto:hello@tomorrow.com'>Reach out to us</a>

search: true
---

# Introduction

Welcome to the CO2 Signal API! You can use our API to get access to information about

- where the electricity in a specific region comes from
- how it was produced
- how much carbon was emitted to produce it

<aside class="warning">
This API is free for <b>non-commercial use</b>. <a href="mailto:pro@electricitymap.org">Reach out to us</a> if you plan to commercialise it.
</aside>

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl 'https://api.co2signal.com/v1/latest?countryCode=DK-DK1'
  -H 'auth-token: myapitoken'
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
  -H 'auth-token: myapitoken'
```

> The above command returns JSON structured like this:

```json
{
    "countryCode": "FR",
    "data": {
        "carbonIntensity": 92.97078744790771,
        "datetime": "2017-02-09T08:30:00.000Z",
        "fossilFuelPercentage": 12.028887656434616
    },
    "status": "ok",
    "units": {
        "carbonIntensity": "gCO2eq/kWh"
    }
}
```

This endpoint retrieves the last known state of a country. It is also possible to get data for a specific zone, in case the country is divided by zones on electricitymap.org.

See [http://api.electricitymap.org/v3/zones](http://api.electricitymap.org/v3/zones) for list of available zones.

### HTTP Request

`GET https://api.co2signal.com/v1/latest`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
countryCode | | two-letter iso country code

## Get latest by geographic coordinate

```shell
curl 'https://api.co2signal.com/v1/latest?lon=6.8770394&lat=45.9162776'
  -H 'auth-token: myapitoken'
```

> The above command returns JSON structured like this:

```json
{
    "countryCode": "FR",
    "data": {
        "carbonIntensity": 93.0727344671727,
        "datetime": "2017-02-09T08:30:00.000Z",
        "fossilFuelPercentage": 12.032514442152996
    },
    "status": "ok",
    "units": {
        "carbonIntensity": "gCO2eq/kWh"
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
