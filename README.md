## Project Title
**Hotel Revenue and Occupancy Insights**

## Project Description
This project leverages Power BI to analyze and visualize key metrics related to hotel revenue and occupancy. By using advanced DAX queries, the dashboard provides insights into various aspects of hotel performance, including total revenue, occupancy rates, average daily rates, and booking patterns. The interactive features allow for filtering by period, room type, market segment, country, and specific hotels, enabling a detailed and flexible analysis.

## Installation / Prerequisites
- **Power BI Desktop:** Ensure you have Power BI Desktop installed.
- **Data Source:** Access to the hotel's revenue and occupancy data.
- **Figma and Adobe Photoshop:** Used for designing the dashboard background and visual elements.

## Project Structure
### DAX Calculations
1. **Date Table:**
   ```DAX
   DateTable = CALENDAR(MIN('hotel data'[Arrival Date]), MAX('hotel data'[Arrival Date]))
   Month = FORMAT('Date Table'[Date], "mmm")
   Month Number = MONTH('Date Table'[Date])
   Quarter = QUARTER('Date Table'[Date])
   Quarter Name = CONCATENATE("Q", 'Date Table'[Quarter])
   Week = WEEKNUM('Date Table'[Date])
   Year = YEAR('Date Table'[Date])
   ```

2. **Revenue Calculations:**
   ```DAX
   Weekend Rev = 'hotel data'[Stays In Weekend Nights] * 'hotel data'[Revenue Per Stay]
   Week Nights Revenue = 'hotel data'[Stays In Week Nights] * 'hotel data'[Revenue Per Stay]
   Weekend Nights Rev = CALCULATE(SUM('hotel data'[Weekend Rev]))
   Week Nights Rev = CALCULATE(SUM('hotel data'[Week Nights Revenue]))
   Total Revenue = CALCULATE(SUM('hotel data'[Rev]), 'hotel data'[Is Canceled] = 0)
   ```

3. **Occupancy Calculations:**
   ```DAX
   Total Weekend Nights = CALCULATE(SUM('hotel data'[Stays In Weekend Nights]))
   Total Weekday Nights = CALCULATE(SUM('hotel data'[Stays In Week Nights]))
   Total Rooms Booked = CALCULATE(COUNTROWS('hotel data'))
   Total Occupied Rooms = CALCULATE(COUNTROWS('hotel data'), 'hotel data'[Is Canceled] = 0)
   Total Days of Booking = CALCULATE(SUM('hotel data'[Total days]), 'hotel data'[Is Canceled] = 0)
   Total Cancelled Bookings = CALCULATE(COUNTROWS('hotel data'), 'hotel data'[Is Canceled] = 1)
   Occupancy Rate = [Total Occupied Rooms] / [Total Rooms Booked]
   ```

4. **Performance Metrics:**
   ```DAX
   Rev PAR = [Average Daily Rate (ADR)] * [Occupancy Rate]
   PM Total Occupancy = CALCULATE([Total Occupied Rooms], DATEADD('Date Table'[Date], -1, MONTH))
   PM Occupancy Rate = CALCULATE([Occupancy Rate], DATEADD('Date Table'[Date], -1, MONTH))
   PM ADR = CALCULATE([Average Daily Rate (ADR)], DATEADD('Date Table'[Date], -1, MONTH))
   CM Occupied Rooms = TOTALMTD([Total Occupied Rooms], 'Date Table'[Date])
   CM Occupancy rate = TOTALMTD([Occupancy Rate], 'Date Table'[Date])
   CM ADRs = TOTALMTD([Average Daily Rate (ADR)], 'Date Table'[Date])
   Avg Week Revenue = CALCULATE(AVERAGEX(VALUES('Date Table'[Week]), [Total Revenue]))
   Avg Week Occupied Rooms = CALCULATE(AVERAGEX(VALUES('Date Table'[Week]), [Total Occupied Rooms]))
   Avg Days of Stay = AVERAGE('hotel data'[Total days])
   Average Daily Rate (ADR) = CALCULATE(AVERAGE('hotel data'[Adr]))
   ```

5. **Trend and Comparison Metrics:**
   ```DAX
   Occupancy Trend = VAR positive_icon = UNICHAR(9650)
                     var negative_icon = UNICHAR(9660)
                     var result = IF([MoM Occupancy] > 0, positive_icon, negative_icon)
                     return result

   MoM Total Occupancy Difference = [CM Occupied Rooms] - [PM Total Occupancy]
   MoM Total Occupancy % = ([CM Occupied Rooms] - [PM Total Occupancy]) / [PM Total Occupancy]
   MoM Occupancy Rate Difference = [CM Occupancy rate] - [PM Occupancy Rate]
   MoM Occupancy Cancatenated = CONCATENATE([Occupancy Trend], [MoM Total Occupancy %])
   MoM Occupancy = ([CM Occupancy rate] - [PM Occupancy Rate]) / [PM Occupancy Rate]
   MoM ADR Diff = [CM ADRs] - [PM ADR]
   MoM ADR = ([CM ADRs] - [PM ADR]) / [PM ADR]
   ADR Trend = VAR positive_icon = UNICHAR(9650)
               var negative_icon = UNICHAR(9660)
               var result = IF([MoM ADR] > 0, positive_icon, negative_icon)
               return result

   Total Occupied Room Trend = VAR positive_icon = UNICHAR(9650)
                               var negative_icon = UNICHAR(9660)
                               var result = IF([MoM Total Occupancy Difference] > 0, positive_icon, negative_icon)
                               return result
   ```

## Project Background
The dashboard's visual design was crafted using **Figma** and **Adobe Photoshop** to ensure a clean, professional, and intuitive interface. These tools were instrumental in creating the layout and visual elements that enhance the user experience and facilitate better data interpretation.
