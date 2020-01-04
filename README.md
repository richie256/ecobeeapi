# Ecobee thermostat

This ecobee api extends the [python-ecobee-api](https://github.com/nkgilley/python-ecobee-api) by retrieving *ExtendedRuntime* informations. This is useful if we want to know which equipment was running while heating.

We can use this api to retrieve periodical informations then publish it into a InfluxDB.

## Retrive interval

- /thermostat/ecobee/resource/runtime

Ecobee does update the runtime every minutes. so you should retrive the Data every minutes.

- /thermostat/ecobee/resource/extended-runtime

The ExtendedRuntime information is updated every 15 minutes: it will contain 3 series of the last three 5 minutes.


## TODO List

- [x] Adapt the code using the new python-ecobee-api
- [x] Code optimisation
- [x] Fully test expired tokens
- [ ] Add equipmentStatus.
- [ ] Integrate desired temperature.
- [ ] Configure the Ecobee API Key using commands: `docker-compose run --rm ecobee-service is-api` 

## How to update ecobee config
- Log into your Ecobee account and create a new API under Developer.
- Using the API Key, call the `curl http://localhost:5002/thermostat/ecobee/apiKey/<api_key>`
- Put the logs in Debug Mode.
- Request a new pin: `curl http://localhost:5002/thermostat/ecobee/pin/request` then retrieve the PIN from the Debug logs.
- Enter the PIN in your Ecobee Account, then request the token: `curl http://localhost:5002/thermostat/ecobee/token/request`


## Examples

`curl http://localhost:5002/thermostat/ecobee/resource/runtime?format=influx`

`curl http://localhost:5002/thermostat/ecobee/resource/extended-runtime?format=influx`

`curl http://localhost:5002/thermostat/ecobee/equipments/running?format=influx`

