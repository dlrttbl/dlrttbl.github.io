# DLR Timetable Explorer Tool - ReadMe

## Overview
The **DLR Timetable Explorer Tool** is a web-based utility for viewing Docklands Light Railway (DLR) timetables. It uses JavaScript to load CSV timetable data from external files specified in `paths.txt`, providing users with interactive train schedule details.

## Project Directory Layout
- `main/index.html`: The main HTML file for the tool.
- `main/paths.txt`: A text file containing links to timetable CSV files.
- `main/base timetables/`: Directory containing base timetable CSV files.

## paths.txt
The `paths.txt` file is crucial for configuring the tool. It contains pairs of lines specifying the name of each timetable and its corresponding CSV file URL. The format is as follows:
```
Name
URL
```
Example:
```
Weekdays:
https://github.com/dlrttbl/dlrttbl.github.io/raw/refs/heads/main/base%20timetables/241104mf-public.csv
Saturdays:
https://github.com/dlrttbl/dlrttbl.github.io/raw/refs/heads/main/base%20timetables/241109sa-public.csv
Sundays:
https://github.com/dlrttbl/dlrttbl.github.io/raw/refs/heads/main/base%20timetables/241110su-public.csv
```
The file links are dynamically read by `index.html` to populate the timetable dropdown and display the relevant timetable data.

## How It Works
- The HTML file (`index.html`) uses JavaScript to fetch `paths.txt` and parse it for available timetables.
- The `fetch()` function loads `paths.txt` with the `{ cache: 'no-store' }` option to ensure the latest version is always used.
- CSV files are fetched based on the URLs in `paths.txt`, allowing the tool to dynamically load and display timetable data.

## Notes
- Make sure `paths.txt` is kept up to date with the correct URLs for both base and temporary timetables.
- Timetable file in use have their names displayed in the "About" section of the tool.

## Disclaimer
The tool is for informational use only, with no guarantee of accuracy. Cross-check with official sources as needed.

## Credits
Created by **Omari A.** using **publicly available data** from [Transport for London (TfL)]([https://tfl.gov.uk](https://tfl.gov.uk/corporate/transparency/freedom-of-information/foi-request-detail?referenceId=FOI-2196-2425)).

