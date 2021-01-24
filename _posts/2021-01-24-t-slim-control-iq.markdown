---
layout: post
title: Tandem T-Slim Control IQ
date: 2021-01-24 12:00050:00 +0000
description: 
img: time_in_range.png 
fig-caption: # Add figcaption (optional)
tags: [Diabetes]
---
When I first got my [Tandem T-Slim insulin pump]({% post_url 2020-07-04-t-slim-impressions %}) it only had Basal IQ mode - in this mode it suspends insulin if your glucose level goes too low, but if it is too high, it doesn't increase insulin - you're on your own. In October last year I got a software upgrade to Control IQ mode. In this mode, if your glucose level goes too high, it increases your insulin and is a fully closed-loop system.

Now that I have been using it for a few months in Control IQ mode, I thought I'd analyse my glucose data and see what effect the Control IQ software has had.

## Method
I exported the CGM glucose data from the Dexcom Clarity website. This was slightly cumbersome as you can only extract 90 days at a time, so I did this in batches.

I started using Google Sheets to analyse the data with pivot tables, but it got really slow as there were so many rows, so I uploaded the data to Google Big Query instead and did the analysis there. The SQL at the bottom of this post generates three tables: average glucose level, time in range, and percentage of nights when I would have been woken up.

The number of days under each regimen is as follows:

| Regimen | Days of data |
| Manual | (since 1998 really, but in this analysis) 141 |
| Basal IQ | 396 |
| Control IQ | 93 |

There are different ways of using Control IQ: you can set sleep mode only when you are sleeping, or you can set sleep mode all the time. Sleep mode tries to maintain a tighter glucose range which it does by changing basal rate only (ie, it doesn't bolus), and the theroy is that there are fewer variables when you are sleeping, so aiming for tighter control should be possible without increasing the number of lows.

For this experiment I used sleep mode all the time. In the future I'll try using sleep mode only at night, and see what difference it makes.

## Results
The average glucose level got better under Basal IQ, but actually got a little worse under Control IQ. This can be explained by the qay I used to use Basal IQ: I would intentionally set my basal insulin a little too high, so my glucose level would always be trending downwards and I would let the Low Glucose Suspend kick in to stop my glucose level from dropping too much. The end result was that my glucose level was lower than under Contol IQ, but the time I spent low was greater under Basal IQ than when manual or under Control IQ.

![Average glucose level]({{ site.url }}/assets/img/average_glucose_level.png)

The time in range steadily got better with Basal IQ and then Control IQ is much better, with glucose levels being in range 94% of the time.

![Time in range]({{ site.url }}/assets/img/time_in_range.png)

The average glucose level and time in range have important impacts on my overall health, but one of the most noticeable impacts has been on the quality of sleep. I looked at the number of nights where my glucose level was out of range, meaning that I would have been woken up. I quickly found that under Control IQ it was so good at fixing out-of-range glucose levels that I turned off glucose level alerts at night: even if it was slightly high or low, it always fixed it and I woke up with good glucose readings. For instance, I would happily go to bed with glucose levels above 10mmol/l and it would correct during the night without over-compensating. 

And so I went from being woken up approximately 18 nights in every month when on my old manual pump, to 13 nights in every month under Basal IQ, to pretty much zero nights under Control IQ. I say "pretty much", because there are a couple of occasions I still get woken up, like if I lie on a brand new sensor you get false low readings ("Compression lows") or if I get a low insulin alert. 

![Woken at night]({{ site.url }}/assets/img/woken_at_night.png)

## Conclusion
I really like the Control IQ software - the time in range is great, and the effect on quality of sleep is amazing. I had pretty much forgotten what it was like to get a good night's sleep most of the time!

I'm still getting a few high periods, so my next tasks are to try and get my average glucose level down a bit, and also to try out using sleep mode only at night.




~~~ sql
with enriched as (
    select 
        timestamp as timestamp,
        case when Glucose_Value__mmol_L_ < 3.9 then "Low" 
             when Glucose_Value__mmol_L_ > 10 then "High"
        else "In range" end as category,
        Glucose_Value__mmol_L_ as reading,
        case when timestamp < "2019-09-23" then "1 - Manual" 
             when timestamp > "2020-10-23" then "3 - Control IQ"
        else "2 - Basal IQ" end as regimen,
        extract(time from timestamp) as time,
        extract(date from timestamp) as date
    from diabetes.data_20210124
),

day_night as (
    select *,
           case when time > "23:00:00" or time < "07:00:00" then "Night" else "Day" end as zone
    from enriched
),

woken_at_night as (
    select *,
           case when zone = "Night" and (category="Low" or category="High") then 1 else 0 end as woken 
    from day_night
),

woken_summary as (
    SELECT regimen, 
        date, 
        case when sum(woken) > 0 then "Yes" else "No" end as woken
    FROM woken_at_night 
    group by regimen, date
)

-- Calcualte number of days under each regimem
select regimen,
       count(distinct date) as num_days
from enriched 
group by regimen

-- Calculate average glucose levels
select regimen,
       avg(reading) as average_reading
from enriched 
group by regimen

-- Calculate time in range
select regimen,
       countif(category="Low")*100/count(category) as low,
       countif(category="In range")*100/count(category) as in_range,
       countif(category="High")*100/count(category) as high,
from enriched 
group by regimen

-- Calculate percentage of nights where there is an out of range reading
select regimen,
       countif(woken="Yes") as num_woken,
       countif(woken="No") as num_not_woken,
       count(woken) as total,
       countif(woken="Yes")*100/count(woken)
from woken_summary 
group by regimen
~~~