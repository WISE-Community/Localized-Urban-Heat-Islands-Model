# Localized Urban Heat Islands Model

A configurable, interactive 3D city model for exploring the **Urban Heat Island (UHI)** effect and how surface reflectivity and urban greenery influence daytime and nighttime city temperatures. Built as a single-file, zero-build HTML/JS prototype for [WISE](https://wise.berkeley.edu/) (Web-based Inquiry Science Environment) curricula.

## Features

- **Interactive 3D City View**
  - Renders real 3D building footprints and road networks for any location using [MapLibre GL JS](https://maplibre.org/) and [OpenFreeMap](https://openfreemap.org/) vector tiles.
  - Dynamically updates building roof reflectivity (cool white roofs vs. standard dark roofs), 3D extruded street trees, ground-level grassy areas, and rooftop gardens as students adjust sliders.
  - Animated canvas overlay showing incoming sunlight rays, reflected sunlight (bouncing off cool roofs and high-albedo surfaces), absorbed heat, and evapotranspiration cooling.
- **24-Hour Temperature Simulation & Graph**
  - Simulates a full 24-hour temperature cycle (`12:00 am` to `12:00 am`) driven by monthly baseline temperatures, latitude/season solar strength, surface albedo, and green-space cooling.
  - Plots real-time temperature curves in **°F** or **°C** with interactive hover/click tooltips.
- **Trial Comparison Table**
  - Automatically saves completed 24-hour runs into a comparison table displaying the location, reflective roof percentage, tree & green space percentage, average daytime temperature, and daily high temperature.
  - Re-running the model with the same location, month, and slider settings re-runs the existing trial in place rather than creating duplicates.
  - Includes per-trial visibility checkboxes, a select/deselect-all header checkbox, and per-row delete buttons to compare or clear trials on the graph.
- **Teacher / Curriculum Authoring Panel**
  - **Localize to Any Place on Earth**: Choose from 8 built-in US cities or search any city, neighborhood, or school address worldwide.
  - **Configurable Variables**: Choose which student sliders to include (`Reflective roofs`, `Tree & green space`) so curriculum steps can introduce one variable at a time or both together.
  - **Shareable URLs & WISE API**: Export a JSON config, copy a shareable URL with query parameters, or configure the model programmatically via `window.UHI.setConfig(...)` while emitting student interaction events via `postMessage`.

## URL Parameters

You can pre-configure the model via URL query parameters:

| Parameter             | Description                                                                                                            | Example                               |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------- | :------------------------------------ |
| `city`                | Built-in city key (`san-francisco`, `oakland`, `richmond`, `berkeley`, `los-angeles`, `phoenix`, `chicago`, `atlanta`) | `?city=oakland`                       |
| `loc`                 | Custom location in `Name@lat,lon` format (fetches 10-year monthly normals automatically)                               | `?loc= Seattle, WA@47.6062,-122.3321` |
| `month`               | Month index (`0` = January … `11` = December)                                                                          | `?month=6`                            |
| `unit`                | Temperature display unit (`F` or `C`)                                                                                  | `?unit=F`                             |
| `label`               | Custom scene caption shown in the map info box                                                                         | `?label=Our+Neighborhood`             |
| `roofs` / `showRoofs` | Set to `0` or `false` to hide the Reflective roofs slider                                                              | `?roofs=0`                            |
| `trees` / `showTrees` | Set to `0` or `false` to hide the Tree & green space slider                                                            | `?trees=0`                            |

## Data Sources

- **Geocoding & 3D Map Geometry**: [OpenStreetMap](https://www.openstreetmap.org/) contributors via [Nominatim](https://nominatim.org/) (location search) and [OpenFreeMap](https://openfreemap.org/) (vector tiles and 3D building extrusions).
- **Historical Climate Baselines**: [Open-Meteo Historical Weather API](https://open-meteo.com/) using 10 years of daily mean temperatures (`2014–2023` ERA5 reanalysis) averaged into monthly normals for searched locations, plus 1991–2020 monthly climate normals for built-in cities.

## Running Locally

Open `index.html` directly in a browser or serve the directory with any static file server:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.
