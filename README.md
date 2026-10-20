# AeroPlanner

### Aircraft Performance Calculator  
**Designed & Developed by Anshul Nagaonkar**

AeroPlanner is a browser-based Aircraft Performance Calculator built with HTML, CSS, and JavaScript. It brings together aircraft and airport reference data with a set of educational calculations for flight planning and performance exploration.

The application runs in the browser and is structured for static website hosting, including GitHub Pages.

> **Educational use only.** AeroPlanner provides estimates from simplified models and project data. It is not approved for real-world flight planning or aircraft operation. Always use current, approved aircraft documentation and operational sources.

---

## Contents

- [Features](#features)
- [How to use AeroPlanner](#how-to-use-aeroplanner)
- [Aircraft database](#aircraft-database)
- [Airport database](#airport-database)
- [Calculator topics](#calculator-topics)
- [Calculation overview](#calculation-overview)
- [Input validation and compatibility checks](#input-validation-and-compatibility-checks)
- [Technology and project structure](#technology-and-project-structure)
- [Run the website locally](#run-the-website-locally)
- [Publish with GitHub Pages](#publish-with-github-pages)
- [Limitations](#limitations)
- [Credits](#credits)

## Features

- A single-page interface that guides users through aircraft selection, airport selection, flight inputs, calculator topics, and results.
- Ten aircraft records covering Airbus and Boeing aircraft.
- An airport database containing airport locations, elevations, operational-category information, taxiway and stand/apron capability data, and runway records.
- Runway selection for supported departure and arrival airports.
- Calculations covering aviation altitudes, route geometry, en-route estimates, fuel planning, weight and balance, wind components, and runway-distance estimates.
- Estimated take-off and landing runway margins.
- Input validation for key numerical fields and time format.
- Aircraft/airport compatibility checks using the reference data included with the project.
- Locally stored aircraft images, country flags, and welcome-screen artwork.

## How to use AeroPlanner

1. **Start the application.** Select the start option on the welcome screen.
2. **Select an aircraft.** Choose one of the available aircraft records. The selected aircraft's stored data is used by the calculators.
3. **Select the airports.** Choose a departure airport and an arrival airport from the available database. Select the relevant runway where prompted.
4. **Enter flight inputs.** Provide the requested weather, wind, departure-time, passenger, cargo, taxi, reserve, alternate, and delay values.
5. **Open a calculator topic.** Use the performance dashboard to access the relevant group of calculations.
6. **Review the results.** Read the displayed estimates, including applicable fuel, weight, wind, distance, and runway-margin values. Review any compatibility messages before interpreting a result.

The interface uses in-page transitions. The workflow does not require opening a separate browser window for each screen.

## Aircraft database

The current website includes the following aircraft:

### Airbus

Aircraft - ICAO designator
Airbus A350-900 - `A359` 
Airbus A350-1000 - `A35K`
Airbus A380-800 - `A388` 
Airbus A321neo XLR - `A21NY`
Airbus A320neo - `A20N`

### Boeing

Aircraft - ICAO designator
Boeing 747-8 Intercontinental - `B748`
Boeing 747-400 - `B744`
Boeing 787-9 Dreamliner - `B789`
Boeing 777-300ER - `B77W`
Boeing 737 MAX 8 - `B38M`

The project data includes aircraft reference values such as operating weights, fuel-related values, wingspan, reference take-off and landing distances, cruise speed, range, and other fields used by the application. These values are project inputs; they should not be treated as verified or approved operational data.

## Airport database

The current database contains these airports:

Airport - ICAO
Pune International Airport - `VAPO`
Chhatrapati Shivaji Maharaj International Airport, Mumbai - `VABB`
Indira Gandhi International Airport, New Delhi - `VIDP`
Kempegowda International Airport, Bengaluru - `VOBL`
Cochin International Airport - `VOCI`
Sardar Vallabhbhai Patel International Airport, Ahmedabad - `VAAH`
Singapore Changi Airport - `WSSS`
London Heathrow Airport - `EGLL`
Dubai International Airport - `OMDB`
Milan Malpensa Airport - `LIMC`
Frankfurt Airport - `EDDF`

The runway database stores runway identifiers, lengths, widths, headings, surfaces, and slope values for the listed airports. The application uses the records available in the project; it does not fetch live airport or runway data.

## Calculator topics

### 1. Aviation Altitudes

- International Standard Atmosphere (ISA) temperature estimate
- Pressure altitude
- Density altitude

### 2. Enroute Performance

- Route track
- Great-circle distance
- Ground speed based on true airspeed and wind inputs
- Estimated en-route flight time
- Estimated time of arrival (ETA), including entered taxi time

### 3. Operational Performance

- Taxi, trip, alternate, reserve, extra, and optional fuel estimates
- Total fuel estimate
- Take-off weight estimate
- Landing weight estimate
- Moment and centre-of-gravity calculations

### 4. Take-off & Landing Performance

- Departure and arrival headwind components
- Departure and arrival crosswind components
- Estimated take-off distance
- Estimated landing distance
- Take-off and landing runway margins

The dashboard groups these functions by topic to make the relevant calculations easier to find.

## Calculation overview

The application uses the equations and constants implemented in its JavaScript calculator module. The following is a high-level guide to the principal calculations.

### ISA temperature

The project estimates ISA temperature using departure-airport elevation:

`ISA temperature (°C) = 15 − 2 × (elevation in feet / 1,000)`

### Pressure altitude

The project calculates pressure altitude from the entered altimeter setting and airport elevation. The calculator module uses the project's standard-pressure constant and input conversion logic.

### Density altitude

Density altitude is estimated from pressure altitude and the difference between outside-air temperature and the calculated ISA temperature.

### Route and distance

The route track and distance are calculated from the departure and arrival airport coordinates using spherical-earth geometry. The project uses an Earth-radius constant of `3443.92 NM`.

### Ground speed and flight time

Ground speed is estimated from true airspeed and the entered wind inputs. Flight time is calculated from route distance and estimated ground speed:

`Flight time (hours) = Distance (NM) / Ground speed (kt)`

The ETA calculation adds the entered taxi time and the rounded en-route flight time to the entered estimated time of departure (ETD). ETA is displayed in 24-hour `HH:mm` format.

### Fuel estimates

The fuel model includes these components:

- Taxi fuel
- Trip fuel
- Alternate fuel
- Reserve fuel
- Extra fuel
- Optional fuel for expected delay

The website displays fuel quantities using the conversions implemented in the project. The fuel-density constant is `0.804 kg/L`.

### Weight and balance

The calculator estimates total weight using the stored operating empty weight, passenger weight, cargo weight, and fuel remaining after taxi. It calculates moment and centre of gravity using the arm values stored in the project data. Landing weight is estimated by subtracting trip fuel from take-off weight.

### Take-off and landing estimates

Take-off and landing distances use the reference distances and simplified weight, wind, and runway-condition factors implemented in the calculator module. The landing calculation also applies the project's landing safety factor. Runway margins are calculated by comparing the estimated distance with the runway length stored in the database.

These equations are simplified estimates. They do not reproduce the complete aircraft-specific performance methods, tables, corrections, or operating procedures required for actual flight operations.

## Input validation and compatibility checks

The application checks key input fields against the bounds defined in the project, including:

Input - Configured range
Outside-air temperature - −80 to 60 °C
Altimeter setting - 800 to 1,100 hPa
Wind direction - 0° to 360°
Wind speed - 0 to 200 kt
Taxi time - 0 to 180 minutes
Reserve time - 1 to 600 minutes
Expected delay - 0 to 600 minutes
Alternate-airport distance - 1 to 10,000 km
True airspeed - 100 to 600 kt
ETD - `HH:mm` format

Passenger and cargo weights must be non-negative. These are broad software input checks, not aircraft operating limitations.

Compatibility checks use the stored aircraft aerodrome reference code, wingspan, runway length and width, and airport taxiway and stand/apron capability records. The application may prevent selection or report a compatibility issue when the stored data does not satisfy its implemented checks. These checks are only as complete and accurate as the project database and rules; they are not a substitute for official airport, runway, aircraft, or operator requirements.

## Technology and project structure

AeroPlanner is a static browser application built with:

- **HTML** for page structure
- **CSS** for layout and visual styling
- **JavaScript ES modules** for application behaviour, stored data, and calculations

Main files and folders:

```
.
├── index.html
├── style.css
├── README.md
├── js/
│   ├── app.js
│   ├── calculators.js
│   └── data.js
└── assets/
    ├── a350-welcomescreen-aeroplanner.jpeg
    ├── Aircrafts/
    │   ├── Airbus/
    │   └── Boeing/
    └── Flags/
        ├── Asia/
        └── Europe/
```

- `index.html` provides the page entry point.
- `style.css` contains the visual styling.
- `js/app.js` manages the interface, screen flow, input handling, and presentation of results.
- `js/calculators.js` contains the calculation functions and compatibility checks.
- `js/data.js` contains the aircraft, airport, runway, and constant data, as well as local asset-path helpers.
- `assets/` contains the images used by the interface.

## Limitations

AeroPlanner is an educational project and is **not certified or approved for operational use**. It must not be used as the sole source for dispatch, take-off, landing, fuel, weight-and-balance, or other flight-operation decisions.

The current implementation does not provide a complete, certified aircraft-specific performance system. Among other limitations, it does not fully model:

- Approved aircraft flight-manual performance tables and all aircraft-specific corrections
- A complete aircraft-specific centre-of-gravity envelope and loading station model
- All regulatory and operator-specific fuel-planning and dispatch requirements
- Live weather, NOTAMs, runway closures, or live airport data
- All runway declared-distance, obstacle, slope, braking-action, contamination, and operational restrictions
- Separate, fully modelled surface-wind and en-route wind datasets
- Certified aircraft/airport compatibility approval

The database may contain simplified, sample, or manually entered values. A displayed margin or compatibility result is not a guarantee of safety or operational suitability. Always consult current official sources, approved aircraft documentation, and qualified operational personnel for real-world aviation decisions.

## Credits

**AeroPlanner**  
Aircraft Performance Calculator  
**Designed & Developed by Anshul Nagaonkar**