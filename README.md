# 🎯 Data Analyst Portfolio Project 1
## 🚴‍♂️🚴‍♀️ London bike sharing dataset
![image](https://user-images.githubusercontent.com/125182638/228728985-07d64de3-508c-4bf0-801e-55f36ebe7665.png)

### About the data
The data from cycling dataset is grouped by "Start time", this represent the count of new bike shares grouped by hour. The long duration shares are not taken in the count.

***Metadata:***
- `timestamp` - timestamp field for grouping the data
- `cnt` - the count of a new bike shares
- `t1` - real temperature in C
- `t2` - temperature in C "feels like"
- `hum` - humidity in percentage
- `wind_speed` - wind speed in km/h
- `weather_code` - category of the weather
- `is_holiday` - boolean field - 1 holiday / 0 non holiday
- `is_weekend` - boolean field - 1 if the day is weekend
- `season` - category field meteorological seasons: 0-spring ; 1-summer; 2-fall; 3-winter.
- `weathe_code` category description:
1 = Clear ; mostly clear but have some values with haze/fog/patches of fog/ fog in vicinity 2 = scattered clouds / few clouds 3 = Broken clouds 4 = Cloudy 7 = Rain/ light Rain shower/ Light rain 10 = rain with thunderstorm 26 = snowfall 94 = Freezing Fog
***
## Data gathering, exploration and manipulation
### Create New Table `london_weather`

Let's construct the structure of `london_weather` table and lay out the actions to be taken.

_`*` represent new columns_

| Columns | Actions to take |
| ------- | --------------- |
|timestamp| Rename `time`
|cnt | Rename `count` 
|t1| Rename `temp_real_C` 
|t2 | Rename `temp_feels_like_C`
|hum| Divide 100 and Rename `humidity_percent`
|wind_speed| Rename `wind_speed_kph`
|weather_code| Rename `weather`
|weather_dict*| Use `CASE WHEN` and based on `weather_code`, 1 = `Clear` ; mostly clear but have some values with haze/fog/patches of fog/ fog in vicinity 2 = `Scattered Clouds` 3 = `Broken clouds` 4 = `Cloudy` 7 = `Rain` 10 = `Rain with thunderstorm` 26 = `Snowfall`
|is_holiday| No changes
|is_weekend | No changes
| season | No changes
| season_dict* | Use `CASE WHEN` and based on `season`, 0=`Spring` ; 1=`Summer`; 2=`Fall`; 3=`Winter`


**Answer:**

````sql
select
	[timestamp] as time,
	[cnt] count,
	[t1] temp_real_C,
	[t2] temp_real_like_C,
	[hum]/100 as humidity_percent,
	[wind_speed] wind_speed_kph,
	[weather_code] weather,
	case weather_code when 1 then 'Clear'
					  when 2 then 'Scattered Clouds'
					  when 3 then 'Broken Clouds'
					  when 4 then 'Cloudy'
					  when 7 then 'Rain'
					  when 10 then 'Rain with thunderstorm'
					  when 26 then 'Snowfall'
					  end weather_dict,
	[is_holiday],
	[is_weekend],
	[season],
	case season when 0 then 'Spring'
				when 1 then 'Summer'
				when 2 then 'Autumn'
				when 3 then 'Winter'
	end season_dict
into london_weather
from [dbo].[29.03.23london_merged];
````

![image](https://user-images.githubusercontent.com/125182638/228729836-8495468f-bdda-46c8-a816-7373f950b4a3.png)


***
## Tableau visualisations summary [here] 
