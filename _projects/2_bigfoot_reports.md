---
name: Bigfoot Reports
tools: [Python, Altair, vega-lite]
image: assets/pngs/bigfoot_seasons.png
description: Two interactive looks at Bigfoot sighting reports from the BFRO dataset.
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---

# Bigfoot Reports

For this homework I used the Bigfoot Field Researchers Organization (BFRO) reports dataset. Each row is one reported sighting with a date, state, season and a class. Class A means a clear sighting and Class B means something heard or seen from far away.

## Plot 1: Reports per year and top states

<vegachart schema-url="{{ site.baseurl }}/assets/json/bigfoot_years_states.json" style="width: 100%"></vegachart>

The top chart shows how many reports came in each year from 1960 on. The bottom chart shows the 15 states with the most reports. Year is on the x axis as an ordinal value and the number of reports is on the y axis. I used a line with points so it is easy to follow the trend year to year. The bar chart uses length to show the count for each state and the bars are sorted so the biggest state is on top. Color in the line chart shows the report class. I used the dark2 color scheme because it is a categorical scheme with strong colors that are easy to tell apart and class is a category with no order.

In the notebook I dropped rows that had no date and pulled the year out of the date column with pandas. I kept 1960 and later since earlier years only have a few reports each. I also dropped Class C since there are only 30 of them. Then I grouped the data two ways: by year and class for the line chart and by year and state for the bar chart. The rank of the states is done in Altair with a window transform so it updates after filtering.

## Plot 2: Reports by season

<vegachart schema-url="{{ site.baseurl }}/assets/json/bigfoot_seasons.json" style="width: 100%"></vegachart>

This chart shows how many reports happen in each season split by class. Season is on the x axis as a nominal value in calendar order and the number of reports is on the y axis. The bars are stacked so you can see the total for a season and how much of it is Class A versus Class B. Class C is kept here but it is so small it barely shows. I used the same dark2 colors for class as in plot 1 so the two plots match and you do not have to learn a new color key.

In the notebook I removed the 91 reports with an Unknown season. Then I counted reports by state, season and class with a groupby. I also made an extra "All states" group by adding up every state so the chart has a full view to start with.

## Interactivity

Plot 1 has a brush on the line chart. You can drag across a range of years and the bar chart below changes to show the top states for only those years. This makes it easy to see if the busy states have changed over time instead of only seeing totals for all years. Plot 2 has a dropdown menu to pick a state. The bars filter to that state so you can check if a state follows the national pattern of summer and fall being the busiest seasons. Both plots also have tooltips that show the exact counts.

<div class="left">
{% include elements/button.html link="https://github.com/UIUC-iSchool-DataViz/is445_data/blob/main/bfro_reports_fall2022.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/Sujit-Vellanki/Sujit-Vellanki.github.io/blob/main/python_notebooks/hw5_bigfoot.ipynb" text="The Analysis" %}
</div>
