# Covid in Indonesia 
It shows some statistical data about Covid-19 in Indonesia

**Author** : Nafila Cahya Andanis

## Introduction
The emergence of COVID-19 has posed a significant challenge globally, the virus has rapidly spread across continents, causing widespread illness, loss of lives, and significant disruptions to economies and daily life. In Indonesia, like many other countries, COVID-19 has posed a multifaceted threat, necessitating swift and comprehensive responses from authorities, healthcare systems, and communities.

This report provides a comprehensive overview of COVID-19 statistics in Indonesia, focusing on the total number of confirmed cases, recoveries, and fatalities. It highlights the top cities with the highest death tolls and offers a month-to-month comparison of confirmed cases versus recoveries. This data is crucial for understanding the impact of the pandemic, guiding public health measures, and allocating resources effectively.

## Dataset
Source : bigquery-public-data.covid19_open_data.compatibility_view

### Covid Statistic in Indonesia

```sql
SELECT * 
FROM `bigquery-public-data.covid19_open_data.compatibility_view` 
WHERE country_region = 'Indonesia' 
ORDER BY date;
```
