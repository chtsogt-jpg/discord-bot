---
name: weather
description: Look up current weather and short-term forecast for a city or location. Trigger when the user asks about weather, temperature, rain, snow, forecast, or "how's the weather in X".
---

# Weather Skill

Provide current conditions and a short forecast for a user-supplied location.

## When to trigger

- "What's the weather in Ulaanbaatar?"
- "Is it going to rain in Tokyo tomorrow?"
- "Temperature in NYC right now"
- Any question about weather, temperature, rain, snow, wind, or forecast tied to a location.

## Instructions

1. **Always fetch fresh data** — never invent values from training data.
2. Resolve the location to coordinates via Open-Meteo's geocoding API:
   `https://geocoding-api.open-meteo.com/v1/search?name=<city>&count=1`
3. Fetch current + daily forecast from Open-Meteo (no API key needed):
   `https://api.open-meteo.com/v1/forecast?latitude=<lat>&longitude=<lon>&current=temperature_2m,relative_humidity_2m,weather_code,wind_speed_10m&daily=temperature_2m_max,temperature_2m_min,weather_code,precipitation_probability_max&timezone=auto&forecast_days=3`
4. Map `weather_code` (WMO codes) to a human label (Clear, Cloudy, Rain, Snow, Thunderstorm, etc.).
5. Report:
   - Location (resolved name + country)
   - Current: temp °C, condition, humidity, wind
   - Next 3 days: high/low, condition, precipitation chance
   - Timestamp (local time)
6. Units: Celsius by default. If user asks in Fahrenheit, convert.

## Edge cases

- **Ambiguous city** (e.g. "Springfield") — show the top match and note there are others; offer to pick a different one.
- **Location not found** — say so and ask the user to clarify (country / nearby major city).
- **API failure** — report the error, don't fabricate numbers.

## Output format

```
**Weather — <City>, <Country>** (as of <local time>)

Now: <temp>°C, <condition>, humidity <h>%, wind <w> km/h

Next 3 days:
- <Day 1>: <lo>–<hi>°C, <condition>, rain <p>%
- <Day 2>: <lo>–<hi>°C, <condition>, rain <p>%
- <Day 3>: <lo>–<hi>°C, <condition>, rain <p>%
```
