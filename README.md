# Covid in Indonesia 

**Author** : Nafila Cahya Andanis

## Introduction
The emergence of COVID-19 has posed a significant challenge globally, causing widespread illness, loss of lives, and significant disruptions to economies and daily life. In Indonesia, like many other countries, COVID-19 has posed a multifaceted threat, necessitating swift and comprehensive responses from authorities, healthcare systems, and communities. This report provides COVID-19 statistics in Indonesia, focusing on the total number of confirmed cases, recoveries, and fatalities. It highlights the top cities with the highest death tolls and offers a month-to-month comparison of confirmed cases versus recoveries. This data is crucial for understanding the impact of the pandemic and allocating resources effectively.

## Dataset
**Source** : bigquery-public-data.covid19_open_data.compatibility_view

### Covid Statistic in Indonesia

```sql
SELECT * 
FROM `bigquery-public-data.covid19_open_data.compatibility_view` 
WHERE country_region = 'Indonesia' AND date BETWEEN '2021-01-01' AND '2021-12-31'
ORDER BY date 
LIMIT 5;
```
This query will shows 5 row of the dataset for Covid cases in 2021

| province_state           | country_region | date       | latitude | longitude | sub_region1_name       | location_geom                  | confirmed | deaths | recovered | active | fips | admin_2  | combined_key |
|--------------------------|----------------|------------|----------|-----------|------------------------|--------------------------------|-----------|--------|-----------|--------|------|----------|--------------|
| Aceh                     | Indonesia      | 2021-01-01 | 2.61667  | 96.08333  | Aceh                   | POINT(96.08333 2.61667)       | 106       | 7      | 98        | 1      | 1109 | Simeulue | ID_AC_1109   |
| Central Java             | Indonesia      | 2021-01-01 | -6.76667 | 111.1     | Central Java           | POINT(111.1 -6.76667)         | 1721      | 300    | 1304      | 117    | 3318 | Pati     | ID_JT_3318   |
| Aceh                     | Indonesia      | 2021-01-01 | 5.083333 | 96.6      | Aceh                   | POINT(96.6 5.083333)          | 470       | 10     | 437       | 23     | 1111 | Bireuen  | ID_AC_1111   |
| Bangka Belitung Islands  | Indonesia      | 2021-01-01 | -1.91667 | 105.93333 | Bangka Belitung Islands| POINT(105.93333 -1.91667)    | 707       | 6      | 573       | 128    | 1901 | Bangka   | ID_BB_1901   |
| Riau Islands             | Indonesia      | 2021-01-01 | 1.067778 | 104.016667| Riau Islands           | POINT(104.016667 1.067778)   | 5069      | 130    | 4522      | 417    | 2171 | Batam    | ID_KR_2171   |

### Top 10 City With Biggest Deaths in Indonesia
```sql
SELECT admin_2 AS city, SUM(deaths) as total_deaths
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE country_region = 'Indonesia'
GROUP BY city
ORDER BY total_deaths DESC
LIMIT 10;
```
| city            | total_deaths |
|-----------------|--------------|
| Semarang        | 411857       |
| Surabaya        | 400504       |
| East Jakarta    | 280407       |
| South Jakarta   | 217342       |
| West Jakarta    | 212478       |
| Sidoarjo        | 161636       |
| Central Jakarta | 147423       |
| North Jakarta   | 145042       |
| Malang          | 144170       |
| Makassar        | 124978       |

### Top 10 City With Biggest Recovery in Indonesia
```sql
SELECT admin_2 AS city, SUM(recovered) as total_recovered
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE country_region = 'Indonesia'
GROUP BY city
ORDER BY total_recovered DESC
LIMIT 10;
```
| city            | total_recovered |
|-----------------|-----------------|
| East Jakarta    | 13777682        |
| South Jakarta   | 11078995        |
| West Jakarta    | 9680424         |
| Bekasi          | 8187727         |
| North Jakarta   | 7119350         |
| Central Jakarta | 6212339         |
| Depok           | 5248179         |
| Surabaya        | 5180878         |
| Makassar        | 4987982         |
| Semarang        | 3857741         |

### Top 5 City With Biggest Deaths in West Java
```sql
SELECT admin_2 AS city, SUM(deaths) as total_deaths
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE province_state = 'West Java'
GROUP BY city
ORDER BY total_deaths DESC
LIMIT 5;
```
| city      | total_deaths |
|-----------|--------------|
| Depok     | 68259        |
| Bekasi    | 65025        |
| Bogor     | 46854        |
| Karawang  | 39261        |
| Cirebon   | 37755        |

### Top 10 City With Biggest Recovery in West Java
```sql
SELECT admin_2 AS city, SUM(recovered) as total_recovered
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE province_state = 'West Java'
GROUP BY city
ORDER BY total_recovered DESC
LIMIT 5;
```
| City      | Total Recovered |
|-----------|-----------------|
| Bekasi    | 8187727         |
| Depok     | 5248179         |
| Bandung   | 3435789         |
| Bogor     | 3256338         |
| Karawang  | 1871781         |

### People With Actice Covid 2020 vs 2021 in West Java
```sql
SELECT admin_2 AS city, 
      SUM(CASE WHEN DATE BETWEEN '2020-01-01' AND '2020-12-31' THEN active ELSE 0 END) as Tahun_2020,
      SUM(CASE WHEN DATE BETWEEN '2021-01-01' AND '2021-12-31' THEN active ELSE 0 END) as Tahun_2021,
      SUM(active) as total_positive_covid
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE province_state = 'West Java'
GROUP BY city
ORDER BY total_positive_covid DESC;
```
| city          | Tahun_2020 | Tahun_2021 | total_positive_covid |
|---------------|------------|------------|----------------------|
| Bekasi        | 367237     | 887882     | 1255119              |
| Depok         | 210463     | 775742     | 986205               |
| Bogor         | 177897     | 654202     | 832099               |
| Bandung       | 166769     | 457885     | 624654               |
| Karawang      | 66169      | 332879     | 399048               |
| Cirebon       | 37915      | 256891     | 294806               |
| Garut         | 30822      | 181656     | 212478               |
| Indramayu     | 10866      | 197354     | 208220               |
| Sukabumi      | 34979      | 145910     | 180889               |
| Tasikmalaya   | 23479      | 152326     | 175805               |
| West Bandung  | 19856      | 152369     | 172225               |
| Subang        | 7622       | 146160     | 153782               |
| Kuningan      | 20218      | 102839     | 123057               |
| Cimahi        | 42419      | 66145      | 108564               |
| Ciamis        | 8149       | 98399      | 106548               |
| Cianjur       | 5095       | 95732      | 100827               |
| Purwakarta    | 20482      | 66508      | 86990                |
| Majalengka    | 15231      | 71245      | 86476                |
| Sumedang      | 7208       | 73578      | 80786                |
| Pangandaran   | 1428       | 69215      | 70643                |
| Banjar        | 3443       | 41192      | 44635                |

### People Deaths Because of Covid in 2021 vs 2022
```sql
SELECT admin_2 AS city, 
      SUM(CASE WHEN DATE BETWEEN '2020-01-01' AND '2020-12-31' THEN deaths ELSE 0 END) as Tahun_2020,
      SUM(CASE WHEN DATE BETWEEN '2021-01-01' AND '2021-12-31' THEN deaths ELSE 0 END) as Tahun_2021,
      SUM(deaths) as total
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE province_state = 'West Java'
GROUP BY city
ORDER BY total DESC;
```
| city          | tahun_2020 | tahun_2021 | Total |
|---------------|------------|------------|-------|
| Depok         | 22122      | 46137      | 68259 |
| Bekasi        | 25365      | 39660      | 65025 |
| Bogor         | 9483       | 37371      | 46854 |
| Karawang      | 6292       | 32969      | 39261 |
| Cirebon       | 8494       | 29261      | 37755 |
| Bandung       | 15576      | 19255      | 34831 |
| Garut         | 2039       | 18545      | 20584 |
| Tasikmalaya   | 1351       | 11875      | 13226 |
| Sukabumi      | 1974       | 10280      | 12254 |
| Purwakarta    | 1970       | 8608       | 10578 |
| Cimahi        | 1992       | 7900       | 9892  |
| Ciamis        | 970        | 7418       | 8388  |
| Majalengka    | 1843       | 5738       | 7581  |
| Indramayu     | 1308       | 5518       | 6826  |
| Sumedang      | 964        | 5602       | 6566  |
| West Bandung  | 1391       | 4579       | 5970  |
| Banjar        | 1280       | 3624       | 4904  |
| Kuningan      | 1599       | 2416       | 4015  |
| Subang        | 1743       | 2114       | 3857  |
| Cianjur       | 403        | 302        | 705   |
| Pangandaran   | 60         | 236        | 296   |


### Comparison Between Positive Covid vs Recovery per Month in West Java
```sql
SELECT admin_2 AS city, 
      SUM(CASE WHEN DATE BETWEEN '2021-01-01' AND '2021-01-31' THEN active ELSE 0 END) as active_jan,
      SUM(CASE WHEN DATE BETWEEN '2021-01-01' AND '2021-01-31' THEN recovered ELSE 0 END) as recovered_jan,
      SUM(CASE WHEN DATE BETWEEN '2021-02-01' AND '2021-02-28' THEN active ELSE 0 END) as active_feb,
      SUM(CASE WHEN DATE BETWEEN '2021-02-01' AND '2021-02-28' THEN recovered ELSE 0 END) as recovered_feb,
      SUM(CASE WHEN DATE BETWEEN '2021-03-01' AND '2021-03-31' THEN active ELSE 0 END) as active_mar,
      SUM(CASE WHEN DATE BETWEEN '2021-03-01' AND '2021-03-31' THEN recovered ELSE 0 END) as recovered_mar,
      SUM(CASE WHEN DATE BETWEEN '2021-04-01' AND '2021-04-30' THEN active ELSE 0 END) as active_apr,
      SUM(CASE WHEN DATE BETWEEN '2021-04-01' AND '2021-04-30' THEN recovered ELSE 0 END) as recovered_apr,
      SUM(CASE WHEN DATE BETWEEN '2021-05-01' AND '2021-05-31' THEN active ELSE 0 END) as active_may,
      SUM(CASE WHEN DATE BETWEEN '2021-05-01' AND '2021-05-31' THEN recovered ELSE 0 END) as recovered_may,
FROM `bigquery-public-data.covid19_open_data.compatibility_view`
WHERE province_state = 'West Java'
GROUP BY city
ORDER BY city;
```
| City          | Active Jan | Recovered Jan | Active Feb | Recovered Feb | Active Mar | Recovered Mar | Active Apr | Recovered Apr | Active May | Recovered May |
|---------------|------------|---------------|------------|---------------|------------|---------------|------------|---------------|------------|---------------|
| Bandung       | 77561      | 326273        | 81635      | 475759        | 82478      | 648850        | 86394      | 704101        | 129817     | 839390        |
| Banjar        | 3343       | 9267          | 1839       | 14727         | 2543       | 19115         | 12910      | 20376         | 20557      | 25383         |
| Bekasi        | 157807     | 733463        | 195254     | 1057657       | 297284     | 1539276       | 150506     | 1752115       | 87031      | 1979964       |
| Bogor         | 28134      | 244512        | 151992     | 379115        | 108586     | 640637        | 154403     | 703584        | 211087     | 807055        |
| Ciamis        | 13665      | 25887         | 9265       | 51889         | 10989      | 71529         | 24908      | 76361         | 39572      | 90909         |
| Cianjur       | 1756       | 7509          | 20831      | 24519         | 18625      | 53056         | 26376      | 63296         | 28144      | 82902         |
| Cimahi        | 9967       | 85763         | 6379       | 97852         | 4339       | 117168        | 14105      | 116051        | 31355      | 125249        |
| Cirebon       | 12597      | 87944         | 41451      | 176417        | 38547      | 265137        | 63033      | 285030        | 101263     | 325952        |
| Depok         | 114629     | 471447        | 130901     | 697988        | 197565     | 986125        | 194788     | 1127943       | 137859     | 1351147       |
| Garut         | 23756      | 90245         | 41539      | 142462        | 27839      | 221271        | 30402      | 239487        | 58120      | 260328        |
| Indramayu     | 4662       | 29914         | 26984      | 62817         | 42151      | 107922        | 64376      | 135173        | 59181      | 178068        |
| Karawang      | 39728      | 195063        | 31236      | 266967        | 74414      | 347547        | 113379     | 387006        | 74122      | 505640        |
| Kuningan      | 10856      | 46982         | 21863      | 69158         | 17637      | 108784        | 16081      | 119581        | 36402      | 134212        |
| Majalengka    | 4946       | 39653         | 4489       | 41802         | 8793       | 54343         | 20929      | 59460         | 32088      | 69318         |
| Pangandaran   | 1266       | 4154          | 11669      | 12416         | 2467       | 29284         | 13587      | 30720         | 40226      | 31807         |
| Purwakarta    | 4948       | 49829         | 20128      | 65068         | 7836       | 101305        | 10560      | 103916        | 23036      | 114688        |
| Subang        | 9470       | 21720         | 10426      | 44578         | 23638      | 67049         | 55938      | 80646         | 46688      | 113783        |
| Sukabumi      | 23025      | 96291         | 37307      | 138206        | 23177      | 215867        | 23783      | 228931        | 38618      | 247711        |
| Sumedang      | 7693       | 30416         | 4622       | 42782         | 5472       | 57977         | 11776      | 61132         | 44015      | 66841         |
| Tasikmalaya   | 23144      | 75275         | 20038      | 128063        | 22304      | 175634        | 34250      | 183917        | 52590      | 212568        |
| West Bandung  | 13480      | 46373         | 21486      | 71929         | 15904      | 114992        | 29541      | 123126        | 71958      | 136057        |
