# jolpica-f1 API Reference

## Base Information

- **Base URL**: `https://api.jolpi.ca/ergast/f1/`
- **Format**: Add `.json` to any endpoint
- **Rate Limit**: 200 requests/hour (unauthenticated)
- **Documentation**: [GitHub](https://github.com/jolpica/jolpica-f1/blob/main/docs/README.md)

## Query Parameters

All endpoints support:
- `limit` - Max results returned (default: 30, max: 100)
- `offset` - Pagination offset (default: 0)

**Example**: `?limit=10&offset=20`

## Special Keywords

- `current` - Current season
- `last` - Most recent race/round

## Endpoints

### 1. Seasons
```bash
GET /ergast/f1/seasons.json
```
Returns all F1 seasons (1950-present).

### 2. Circuits
```bash
GET /ergast/f1/circuits.json
GET /ergast/f1/circuits/{circuitId}.json
```
Returns circuit information including location coordinates.

**Example**: `/ergast/f1/circuits/monaco.json`

### 3. Drivers
```bash
GET /ergast/f1/drivers.json
GET /ergast/f1/drivers/{driverId}.json
GET /ergast/f1/{season}/drivers.json
```
Returns driver information (name, nationality, DOB, permanent number).

**Examples**:
- `/ergast/f1/drivers/max_verstappen.json`
- `/ergast/f1/2025/drivers.json`

### 4. Constructors (Teams)
```bash
GET /ergast/f1/constructors.json
GET /ergast/f1/constructors/{constructorId}.json
GET /ergast/f1/{season}/constructors.json
```
Returns constructor/team information.

**Examples**:
- `/ergast/f1/constructors/red_bull.json`
- `/ergast/f1/constructors/mclaren.json`

### 5. Race Schedule
```bash
GET /ergast/f1/{season}.json
GET /ergast/f1/{season}/races.json
GET /ergast/f1/current.json
```
Returns race calendar with dates, times, and circuit info.

**Example**: `/ergast/f1/2025.json`

### 6. Race Results
```bash
GET /ergast/f1/{season}/{round}/results.json
GET /ergast/f1/{season}/last/results.json
GET /ergast/f1/current/last/results.json
```
Returns race results with positions, times, points, and fastest laps.

**Example**: `/ergast/f1/2024/last/results.json`

### 7. Qualifying Results
```bash
GET /ergast/f1/{season}/{round}/qualifying.json
GET /ergast/f1/{season}/qualifying.json
```
Returns qualifying results with Q1, Q2, Q3 times.

**Example**: `/ergast/f1/2024/24/qualifying.json`

### 8. Sprint Results
```bash
GET /ergast/f1/{season}/sprint.json
GET /ergast/f1/{season}/{round}/sprint.json
```
Returns sprint race results.

**Example**: `/ergast/f1/2024/sprint.json`

### 9. Driver Standings
```bash
GET /ergast/f1/{season}/driverstandings.json
GET /ergast/f1/{season}/{round}/driverstandings.json
GET /ergast/f1/current/driverstandings.json
```
Returns championship standings with points, wins, and positions.

**Example**: `/ergast/f1/current/driverstandings.json`

### 10. Constructor Standings
```bash
GET /ergast/f1/{season}/constructorstandings.json
GET /ergast/f1/{season}/{round}/constructorstandings.json
GET /ergast/f1/current/constructorstandings.json
```
Returns team championship standings.

**Example**: `/ergast/f1/current/constructorstandings.json`

### 11. Pit Stops
```bash
GET /ergast/f1/{season}/{round}/pitstops.json
```
Returns pit stop data with lap, stop number, time, and duration.

**Example**: `/ergast/f1/2024/1/pitstops.json`

### 12. Lap Times
```bash
GET /ergast/f1/{season}/{round}/laps.json
GET /ergast/f1/{season}/{round}/laps/{lapNumber}.json
```
Returns lap-by-lap timing data.

**Example**: `/ergast/f1/2024/1/laps/1.json`

### 13. Status Codes
```bash
GET /ergast/f1/status.json
```
Returns all finishing status codes (Finished, Engine, Accident, etc.).

## Response Structure

All responses follow this structure:

```json
{
  "MRData": {
    "xmlns": "",
    "series": "f1",
    "url": "https://api.jolpi.ca/ergast/f1/...",
    "limit": "30",
    "offset": "0",
    "total": "100",
    "[TableName]": {
      // Data here
    }
  }
}
```

## Common Driver/Constructor IDs

### Drivers (driverId)
- `max_verstappen` - Max Verstappen
- `norris` - Lando Norris
- `leclerc` - Charles Leclerc
- `hamilton` - Lewis Hamilton
- `russell` - George Russell
- `sainz` - Carlos Sainz
- `piastri` - Oscar Piastri
- `alonso` - Fernando Alonso

### Constructors (constructorId)
- `red_bull` - Red Bull Racing
- `mclaren` - McLaren
- `ferrari` - Ferrari
- `mercedes` - Mercedes
- `aston_martin` - Aston Martin
- `williams` - Williams
- `alpine` - Alpine
- `haas` - Haas F1 Team
- `rb` - RB F1 Team
- `sauber` - Sauber

## Useful Examples

**Get current season schedule:**
```bash
curl "https://api.jolpi.ca/ergast/f1/current.json"
```

**Get latest race results:**
```bash
curl "https://api.jolpi.ca/ergast/f1/current/last/results.json"
```

**Get driver standings after specific round:**
```bash
curl "https://api.jolpi.ca/ergast/f1/2025/10/driverstandings.json"
```

**Get all wins by a driver:**
```bash
curl "https://api.jolpi.ca/ergast/f1/drivers/max_verstappen/results/1.json"
```

**Get specific circuit info:**
```bash
curl "https://api.jolpi.ca/ergast/f1/circuits/monaco.json"
```

## Notes

- All endpoints should end with `/` or `.json`
- The API is backward compatible with the deprecated Ergast API
- Timestamps are in UTC
- Coordinates use decimal degrees (lat/long)
- Wikipedia links included for most entities

