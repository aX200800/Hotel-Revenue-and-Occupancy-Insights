# Project Title

## Hotel Revenue and Occupancy Insights

# Project Description
This project involves analyzing hotel revenue and occupancy metrics using Power BI. Advanced DAX queries have been utilized to provide in-depth insights into various key performance indicators (KPIs) related to hotel operations, including total revenue, occupancy rates, average daily rates, and more. The dashboard enables dynamic filtering by period, assigned room type, market segment, country, and hotel to allow for comprehensive analysis.

# Installation / Prerequisites
* **Power BI Desktop**: Ensure you have Power BI Desktop installed.
* **Data Source**: Access to the hotel revenue and occupancy data.
* **Figma and Adobe Photoshop**: These tools were used for designing the background and visual elements of the dashboard.

# Project Structure
## DAX Calculations
1. **Date Table**:
   <ul>
   <li>DateTable = CALENDAR(MIN('hotel data'[Arrival Date]), MAX('hotel data'[Arrival Date]))</li>
   <li>Month = FORMAT('Date Table'[Date], "mmm")
   <li>Month Number = MONTH('Date Table'[Date])
   <li>Quarter = QUARTER('Date Table'[Date])
   <li>Quarter Name = CONCATENATE("Q", 'Date Table'[Quarter])
   <li>Week = WEEKNUM('Date Table'[Date])
   <li>Year = YEAR('Date Table'[Date])</ul>

