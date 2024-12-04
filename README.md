# DLR Timetable Explorer Tool - ReadMe

## Overview
The **DLR Timetable Explorer Tool** is a web-based single page application for viewing Docklands Light Railway (DLR) timetables. It uses JavaScript to load CSV timetable data from external files specified in `paths.txt` and `archivedpaths.txt`, providing users with interactive train schedule details.

## Project Directory Layout
- `main/index.html`: The main HTML file for the tool.
- `main/paths.txt`: A text file containing links to the current timetable CSV files. (These will populate the timetable dropdown when the site loads) 
- `main/archivedpaths.txt`: A text file containing links to archived timetable CSV files. (These are hidden from the timetable dropdown but can be navigated to directly by URL or found in the dropdown by using /#archived)
- `main/active timetables/`: Directory containing active timetable CSV files.
- `main/archived timetables/`: Directory containing archived timetable CSV files.

## paths.txt and archivedpaths.txt
The `paths.txt`, and `archivedpaths.txt` files are crucial for configuring the tool. They contains pairs of lines specifying the name of each timetable and its corresponding CSV file URL. The format is as follows:
```
Name
URL
```
Example:
```
Weekdays
https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/241104mf-public.csv
Saturdays
https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/241109sa-public.csv
Sundays
https://raw.githubusercontent.com/dlrttbl/dlrttbl.github.io/refs/heads/main/active%20timetables/241110su-public.csv
```
The file links are dynamically read by the SPA to populate the timetable dropdown and display the relevant timetable data.
N.B. The timetable dropdown is populated according to the order of the files linked within `paths.txt`.

## How It Works
- The main HTML file (`index.html`) uses JavaScript to fetch `paths.txt` and `archivedpaths.txt` to get available timetables.
- **Timetable Data**: CSV files linked in `paths.txt` and `archivedpaths.txt` are fetched, parsed, and displayed. The tool presents information about train runs, allowing users to see departure and arrival times, platforms, and detailed trip breakdowns.
- **Run and Trip Navigation**: Users can select train run numbers to see detailed schedules, view individual trips within a run, or toggle to see a runs full schedule.

## URL Hash Navigation
- The tool supports URL hash navigation, allowing users to bookmark and share specific train runs and trips.
- URL structure: `#timetable=<timetable_name>&run=<run_number>&trip=<trip_number>`.
- URLS will remain valid for a timetable after it has been archived as long as its filename rmains the same.

## Notes
- Make sure `paths.txt` is kept up to date with the timetable, move out of date timetables to `archivedpaths.txt`.
- Active timetable files within `paths.txt` in use have their names displayed in the "About" section of the tool.

## Disclaimer
The tool is for informational use only, with no guarantee of accuracy. Cross-check with official sources as needed.

## Credits
Created by **Omari A.** using **publicly available data** from [Transport for London (TfL)]([https://tfl.gov.uk](https://tfl.gov.uk/corporate/transparency/freedom-of-information/foi-request-detail?referenceId=FOI-2196-2425)).
