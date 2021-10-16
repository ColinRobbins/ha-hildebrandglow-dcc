# UK Smart Meter (DCC) Integration via Hildebrand Glow API 

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)

[![CodeQL](https://github.com/ColinRobbins/ha-hildebrandglow-dcc/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/ColinRobbins/ha-hildebrandglow-dcc/actions/workflows/codeql-analysis.yml)
[![Validate with hassfest](https://github.com/ColinRobbins/ha-hildebrandglow-dcc/actions/workflows/hassfest.yaml/badge.svg)](https://github.com/ColinRobbins/ha-hildebrandglow-dcc/actions/workflows/hassfest.yaml)
[![Validate with HACS](https://github.com/ColinRobbins/ha-hildebrandglow-dcc/actions/workflows/validate.yaml/badge.svg)](https://github.com/ColinRobbins/ha-hildebrandglow-dcc/actions/workflows/validate.yaml)
[![CodeFactor](https://www.codefactor.io/repository/github/colinrobbins/ha-hildebrandglow-dcc/badge)](https://www.codefactor.io/repository/github/colinrobbins/ha-hildebrandglow-dcc)
[![DeepSource](https://deepsource.io/gh/ColinRobbins/ha-hildebrandglow-dcc.svg/?label=active+issues&show_trend=true&token=MDhJZc9apbqyriqeh0VbEEx8)](https://deepsource.io/gh/ColinRobbins/ha-hildebrandglow-dcc/?ref=repository-badge)

Home Assistant integration for *free* energy consumption data from UK SMETS (Smart) meters using the Hildebrand Glow API.

***This is a fork of the [@HandyHat](https://github.com/HandyHat/ha-hildebrandglow-dcc), pending a set of [pull requests](https://github.com/HandyHat/ha-hildebrandglow-dcc/pulls).***

This integration works, for free, without requiring a consumer device provided by Hildebrand Glow and can work with your existing smart meter. You'll need to set up your smart meter for free in the Hildebrand Bright app on [Android](https://play.google.com/store/apps/details?id=uk.co.hildebrand.brightionic&hl=en_GB) or [iOS](https://apps.apple.com/gb/app/bright/id1369989022). This will only work when using the Data Communications Company (DCC) backend, which all SMETS 2 meters and some SMETS 1 meters do ([more information](https://www.smartme.co.uk/technical.html)). Once you can see your data in the app, you are good to go.

The data provided will be delayed by around 30 minutes. To get real-time consumption data, you can buy [Hildebrand Glow hardware](https://shop.glowmarkt.com/). Although this integration will work with their hardware, you should use the MQTT version [integration](https://github.com/unlobito/ha-hildebrandglow/) to get real-time consumption data.

## Installation

### Automated installation through HACS

You can install this component through [HACS](https://hacs.xyz/) and receive automatic updates.

After installing HACS, visit the HACS _Integrations_ pane and add `https://github.com/ColinRobbins/ha-hildebrandglow-dcc` as an `Integration` by following [these instructions](https://hacs.xyz/docs/faq/custom_repositories/). You'll then be able to install it through the _Integrations_ pane.

### Manual installation

Copy the `custom_components/hildebrandglow_dcc/` directory and all of its files to your `config/custom_components` directory. You'll then need to restart Home Assistant for it to detect the new integration.

## Configuration

Visit the _Integrations_ section within Home Assistant's _Configuration_ panel and click the _Add_ button in the bottom right corner. After searching for "Hildebrand Glow", you'll be asked for your Glow credentials.

During configuration, you will be prompted for the GAS conversion factor and calorific value.
These can be found on your GAS bill (Or accept the default apprximate values).   
(If you don't have a GAS meter, just leave the defaults)

Once you've authenticated to Glow, the integration will automatically set up the following sensors for each of the smart meters on your account.

### Electricity Sensors
- Electric Consumption (Today)
  
  Consumption today in kWh
- Electric Cost (Today)

  Cost in pence of electricity used today
- Electric Tariff Standing

  Todays standing charge for electricity (GBP)
- Electric Tariff Rate

  Current tariff in GBP/kWh
### GAS Sensors
- Gas Consumption (Today)

  Consumption today in kWh
- Gas Consumption Metric (Today)

  Consumption today in m³
- Gas Cost (Today)

  Cost in pence of GAS used today
- Gas Tariff Standing

  Todays standing charge for GAS (GBP)
- Gas Tariff Rate

  Current tariff in GBP/kWh

- Gas Tariff Rate (Metric)

  Current tariff in GBP/m³

## HASS Energy Integration
The sensors created provide everything needed to integrate Electicity and GAS meter readings as well as costs into the HASS [Home Energy Management](https://www.home-assistant.io/docs/energy/).

## Debugging

To debug the integration, add the following to your `configuration.yaml`

```yaml
logger:
  default: warning
  logs:
    custom_components.hildebrandglow_dcc: debug
```

## Credits

- This is a fork of the [@HandyHat](https://github.com/HandyHat/ha-hildebrandglow-dcc) repository, which did all the hard groundwork.
- The HandyHat itself was a fork of the (https://github.com/unlobito/ha-hildebrandglow), which now provides the MQTT interface, for realtime data via a Hildebrand device.
- The Hildebrand API [documentation](https://docs.glowmarkt.com/GlowmarktAPIDataRetrievalDocumentationIndividualUserForBright.pdf) and [Swagger UI](https://api.beething.com/api-docs/v0-1/resourcesys/).
- The [Hildebrand-Glow-Python-Library](https://github.com/ghostseven/Hildebrand-Glow-Python-Library) was great for understanding the API.

### Contributors
- [@ghostseven](https://github.com/ghostseven)
- [@HandyHat](https://github.com/HandyHat)
- [@ColinRobbins](https://github.com/ColinRobbins)
- [@totalitarian](https://github.com/totalitarian)
- [@nlobito](https://github.com/unlobito)
- [@declan-morris](https://github.com/declan-morris)
