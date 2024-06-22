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
    *DateTable = CALENDAR(MIN('hotel data'[Arrival Date]), MAX('hotel data'[Arrival Date]))
    *Month = FORMAT('Date Table'[Date], "mmm")
    *Month Number = MONTH('Date Table'[Date])
    *Quarter = QUARTER('Date Table'[Date])
    *Quarter Name = CONCATENATE("Q", 'Date Table'[Quarter])
    *Week = WEEKNUM('Date Table'[Date])
    *Year = YEAR('Date Table'[Date])

