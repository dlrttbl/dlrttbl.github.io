# DLR Timetable Explorer Tool - ReadMe

## Overview

The **DLR Timetable Explorer Tool** is a web-based application for viewing Docklands Light Railway (DLR) timetables. It uses JavaScript to load CSV timetable data from external files specified in `paths.txt` and `archivedpaths.txt`, providing users with interactive train schedule details.

## Project Directory Layout

- `main/index.html`: The main HTML file for the tool.
- `main/search.html`: A dedicated page for searching train services by location, and time.
- `main/paths.txt`: A text file containing links to the current timetable CSV files. (These will populate the timetable dropdown when the site loads.)
- `main/archivedpaths.txt`: A text file containing links to archived timetable CSV files. (These are hidden from the timetable dropdown but can be navigated to directly by URL or found in the dropdown by using /#archived.)
- `main/active timetables/`: Directory containing active timetable CSV files.
- `main/archived timetables/`: Directory containing archived timetable CSV files.
- `main/serviceoverrides.txt`: A file used to override the current TfL API service status.

## paths.txt and archivedpaths.txt

The `paths.txt` and `archivedpaths.txt` files are crucial for configuring the tool. They follow a structured format, making them easier to read and parse.

### paths.txt Format

```
Name: <Timetable Name>
Applies: <Day(s) of the week OR specific date(s)/date range>
URL: <CSV File URL>
```

### archivedpaths.txt Format

```
Name: <Timetable Name>
URL: <CSV File URL>
```

*Note: ********************************************************`archivedpaths.txt`******************************************************** does not use the ********************************************************`Applies:`******************************************************** field.*

### Example

```
Name: Weekdays
Applies: 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'
URL: https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/241104mf-public.csv

Name: Saturdays
Applies: 'Saturday'
URL: https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/241109sa-public.csv

Name: Special Service
Applies: '2025-01-01'
URL: https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/250101public.csv

Name: Temporary timetable
Applies: '2025-01-01/2025-01-20'
URL: https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/250101-250120.csv
```

*Note: ********************************************************`03:00`******************************************************** is treated as the transition point between dates by the tool.* 

- `Applies:` can include:
  - Fixed weekdays (e.g., `'Monday'`, `'Tuesday'`, etc.).
  - A specific date (e.g., `'2025-01-01'`).
  - A date range (e.g., `'2025-01-01/2025-01-20'`).
- The file links are dynamically read by the SPA to populate the timetable dropdown and display the relevant timetable data.
- The timetable dropdown is populated according to the order of the files linked within `paths.txt`.

## How It Works

- The main HTML file (`index.html`) uses JavaScript to fetch `paths.txt` and `archivedpaths.txt` to get available timetables.
- **Timetable Data**: CSV files linked in `paths.txt` and `archivedpaths.txt` are fetched, parsed, and displayed. The tool presents information about train runs, allowing users to see departure and arrival times, platforms, and detailed trip breakdowns.
- **Run and Trip Navigation**: Users can select train run numbers to see detailed schedules, view individual trips within a run, or toggle to see a run's full schedule.
- **Archived Timetables**: Users can access archived timetables using `#archived` in the URL, allowing them to view older schedules if needed.

## Search Page (`search.html`)

The **Search Page** (`search.html`) provides a convenient way to look up **DLR train services** based on station locations, platform numbers, and departure times.

### Features:

- **Search by Location:** Enter a station name or platform number to find trains stopping there.
- **Time Filtering: Specify a time to locate services running around a particular time. Results will be returned for 5 minutes before and 20 minutes after the specified time.**
- **Calling-At Filtering:** Optionally refine results by selecting a station where the train should pass through.

## TfL Service Status Integration

The tool checks the latest DLR service status using [https://api.tfl.gov.uk/Line/dlr/Status](https://api.tfl.gov.uk/Line/dlr/Status).

- If there is active disruption or service modification, a **warning message** is displayed before users proceed, ensuring they are aware that the timetable cannot be relied upon.
- A **'Proceed with Caution'** link allows users to access timetable details despite warnings.

### Manual Service Status Overrides

The tool can override the TfL API-reported status using `serviceoverrides.txt`. This file allows the user to define alternative statuses for a specific date or date range.

### serviceoverrides.txt Format

```
Mapping: <Status Code>
Applies: <Date or Date Range>
```

#### Example

```
Mapping: 7
Applies: '2025-01-01'

Mapping: 5
Applies: '2025-01-5/2025-01-10'
```
This example forces a "Reduced Service" status on January 1, 2025, and a "Part Closure" status from January 5, 2025 to January 10, 2025.

#### Status Code Reference Table

| Status Code | Description     | Status Code | Description     |
| ----------- | --------------- | ----------- | --------------- |
| 0           | Special Service | 6           | Severe Delays   |
| 1           | Closed          | 7           | Reduced Service |
| 2           | Suspended       | 9           | Minor Delays    |
| 3           | Part Suspended  | 10          | Good Service    |
| 4           | Planned Closure | 11          | Part Closed     |
| 5           | Part Closure    | 16          | Not Running     |
| 20          | No Service      |             |                 |

## Automatic 'Run Transition' Detection
The tool detects and displays when a train transitions from one run number to another. This helps users follow the continuity of a train’s journey across different run numbers throughout the day.

## URL Hash Navigation

The tool supports URL hash navigation, allowing users to bookmark and share specific train runs and trips.
- URL structure: `#timetable=<timetable_name>&run=<run_number>&trip=<trip_number>`.
  
*Note: ********************************************************`URLs remain valid for a timetable after it has been archived as long as its filename remains the same.`*********************************************************

## Notes

- Ensure `paths.txt` is kept up to date with the timetable; move outdated timetables to `archivedpaths.txt`.
- Active timetable files within `paths.txt` in use have their names displayed in the "About" section of the tool.
- Archived timetables can be accessed via `#archived` in the dropdown or directly through a URL.

## Disclaimer

The tool is for informational use only, with no guarantee of accuracy. Cross-check with official sources as needed.

## Credits

Created by **Omari A.** using **publicly available data** from [Transport for London (TfL)](https://tfl.gov.uk/corporate/transparency/freedom-of-information/foi-request-detail?referenceId=FOI-2196-2425).

