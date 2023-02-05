**

## Google Data Analytics Capstone Project (R Programming)

** 
### Introduction

The project is a part of Google Data Analytics Certification course capstone. Welcome to the Cyclistic bike-share analysis case study! This case study, will perform many real-world tasks to answer the key business questions.

### Business Task
How do annual members and casual riders use Cyclistic bikes differently?

### Data
**License**: The data has been made available by Motivate International Inc. under the [license](https://ride.divvybikes.com/data-license-agreement).</br> 
**Our Data Range**: October and November 2022 (2 months data).

## Tools
#### Data Cleaning Tools, Data Visualization and Data Analysis

![image](https://user-images.githubusercontent.com/119749518/216831247-d77529f1-fe35-4012-9745-7557bbc85cfa.png)

### Loading libraries to start data analyzing

      library(tidyverse)
      library(ggplot2)
      library(plyr)
      library(dplyr)
      library(hms)

### Importing Data in R

    data1 <- read.csv(file.choose())
    data2 <- read.csv(file.choose())


### Merging both data in one data frame

```{r}
data3 <- rbind(data1, data2)
```

### Now let's check if new DF is created

```{r}
dim(data3)  # No. of rows and columns in the data frame
head(data3) # showing top 6 records of all columns
summary(data3) # Information on different columns
```

![image](https://user-images.githubusercontent.com/119749518/216831475-f601338e-bf93-49de-a67f-99fc7309fee4.png)

![image](https://user-images.githubusercontent.com/119749518/216831541-17a44657-afe8-46de-a77b-080549273a06.png)

![image](https://user-images.githubusercontent.com/119749518/216831582-df9b4acd-dc70-4b9c-9375-a4c29bbb0525.png)


### Changing started_at and ended_at to date formats using Lubridate

```{r}
data3$started_at <- lubridate::dmy_hms(data3$started_at)
data3$ended_at <- lubridate::dmy_hms(data3$started_at)
```

### Creating a new column 'Tdifference' consisting the difference of end and start dates

    ```{r}
    data3 <- mutate(data3, Tdifference = c(ended_at - started_at))
    ```

![image](https://user-images.githubusercontent.com/119749518/216831768-d21d8cd9-dea7-4110-842a-f75c233210a2.png)


### Changing the time in Hours, Minutes, Seconds format
```{r}
data3$Tdifference <- as_hms(data3$Tdifference)
```
![image](https://user-images.githubusercontent.com/119749518/216831647-eebc406f-309f-4103-aaf7-99f3a309f096.png)


### Creating a new column for the name of days for the data

```{r}
data3$days <- weekdays(data3$started_at)
```
![image](https://user-images.githubusercontent.com/119749518/216831831-44140a97-fe85-4984-a5f4-bdedfdfa1fac.png)


### Finding NAs columns in the DF
```{r}
colSums(is.na(data3))
```
![image](https://user-images.githubusercontent.com/119749518/216832493-7d674543-cf31-4ecd-832f-88cc81d6bfcd.png)


## Now Let's Visualize

### Checking day wise traffic of members vs non-members

    ```{r, fig.width = 20, fig.height = 11}
    ggplot(data3, aes(x = days, y = member_casual, fill = member_casual)) 
    + geom_col() + facet_wrap(~member_casual) + theme_classic() 
    + labs(title = "Day wise Traffic", caption = "prepared by Raminder Singh", 
    x = "Days", y = "Members") + theme(axis.text.y = element_blank())
    ```
![image](https://user-images.githubusercontent.com/119749518/216831971-b24b7d6a-cb47-4b3a-93ac-17d64b38236f.png)


### Converting table to data frame and create a bar graph of 5 popular stations to get bikes

    ```{r, fig.width = 11, fig.height = 10}
    ggplot(as.data.frame(data5), aes(x = Var1, y = Freq, fill = Freq)) 
    + geom_bar(stat = 'identity') + theme_classic() 
    + labs(title = "Top 5 Bike Picking stations", x = 'Stations', y = 'Visits', 
    caption = 'prepared by Raminder Singh') + 
    geom_text(aes(label = Freq, vjust = -1))

![image](https://user-images.githubusercontent.com/119749518/216832064-cec3f8d8-6baa-49af-aa05-e41c5f2db7de.png)

### Converting table to data frame and create a bar graph of Top 5 Bike Leaving Stations

    ```{r, fig.width = 11, fig.height = 10}
    ggplot(as.data.frame(data6), aes(x = Var1, y = Freq, fill = Freq)) 
    + geom_bar(stat = 'identity') + theme_classic() 
    + labs(title = "Top 5 bike Leaving stations", x = 'Stations', y = 'Visits', 
    + caption = 'prepared by Raminder Singh') 
    + geom_text(aes(label = Freq, vjust = -1))

![image](https://user-images.githubusercontent.com/119749518/216832155-5529f3de-d1ad-425d-8da2-2129a4ab1c91.png)

### Checking day wise traffic based on Rideable type

    ```{r, fig.width = 15, fig.height = 10}
    ggplot(data3, aes(x = rideable_type, y = days, fill = days)) 
    + geom_col() + facet_wrap(~days) + theme_classic() 
    + theme(axis.text.y = element_blank()) + 
    + labs(title = "Day wise popular rideable", 
    + caption = "prepared by Raminder Singh", x = "Rideable Type", y = "Days")

![image](https://user-images.githubusercontent.com/119749518/216832229-0aeb5bca-1905-49e2-9547-ebfa2082f4f9.png)



## Conclusion

-   As per overall data the busiest days for members were  **Monday and Tuesday**.
-   As per overall data the busiest days for casuals were  **Thursday and Friday**.
-   The most popular place to get the bikes is **Streeter Dr & Grand Ave** followed by **Ellis Ave & 60th St**.
-   The most popular place to drop the bikes is **Streeter Dr & Grand Ave** followed by **Ellis Ave & 60th St**.
-   The most popular bike on daily basis is **Electruc bike** followed by **Classic bike**.

## Recommendations

-   Targetted on-ground marketing strategies should be placed to convert casual riders to members on  **Thursday and Friday**  as most casual riders traffic come on these days.
-   Discounting campaigns for new members should be initiated to lure the casual riders to enrol for membership.
