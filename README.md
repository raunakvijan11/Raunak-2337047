**I have used Mahmud Ahad Abedin Fardin's data set on Turkiye Is Bankasi A.S. from Kaggle**

*Question 1* What is the overall trend on a monthly basis?
*Answer 1* 
SELECT
  EXTRACT(MONTH from Date) AS month,
  AVG(Open) AS avg_open
FROM `raunaks-r-class-project.Turkiyestock11.Data11`
GROUP BY month
ORDER BY month;

Result 1: https://drive.google.com/file/d/1bix_VP2slP9eW5-eeklJcOJPHvfTO07s/view?usp=sharing


*Question 2* What are the highest and lowest opening prices?
*Answer 2*
SELECT
MAX(Open) AS highest_open,
  MIN(Open) AS lowest_open
FROM `raunaks-r-class-project.Turkiyestock11.Data11` 

Result 2: https://drive.google.com/file/d/1qMfTZJvHuN2KAlaY3DkWs1d2yR3lLsbH/view?usp=sharing


*Question 3* What is the volume of stock trading of Turkiye Bank on a monthly basis?
*Answer 3*
SELECT
  Extract(MONTH from Date) AS month,
  SUM(Volume) AS total_volume
FROM `raunaks-r-class-project.Turkiyestock11.Data11`
GROUP BY month
ORDER BY total_volume DESC;

Result 3: https://drive.google.com/file/d/1QfqWDhgcaAsY05B3cHeiTpzJMDWkcI2e/view?usp=sharing


*Question 4* Find the SMA for the bank stock
*Answer 4*
SELECT
    Date,
    AVG(Open) OVER (PARTITION BY Date ORDER BY Date ASC ROWS 20 PRECEDING) AS sma_20
FROM `raunaks-r-class-project.Turkiyestock11.Data11`

Result 4: https://drive.google.com/file/d/1fBlpK2EMO5EwQPtQwlOWizohT9ze60lR/view?usp=sharing


*Question 5* What were some of the unusual trading days?
*Answer 5*
SELECT
    Date,
    Open,
    Volume,
    ABS(Open - AVG(Open) OVER (PARTITION BY Date ORDER BY Date ASC ROWS 1 PRECEDING)) AS open_deviation
FROM `raunaks-r-class-project.Turkiyestock11.Data11`
ORDER BY open_deviation DESC;

Result 5: https://drive.google.com/file/d/1rkWBS_AT5ryPF5OLUhZC_AXmdBLWn25q/view?usp=sharing


*Question 6* What were the total trading days and average volume?
*Answer 6*
SELECT
  COUNT(DISTINCT Date) AS total_days,
  AVG(Volume) AS avg_daily_volume
FROM `raunaks-r-class-project.Turkiyestock11.Data11`

Result 6: https://drive.google.com/file/d/1bmy_g7RLgy1P4fhl8zZhmEIk-y3uTtvY/view?usp=sharing


*Question 7* What are the consecutive positive/negative returns period?
*Answer 7*
SELECT
  Date,
  Open,
  CASE WHEN Open > LAG(Open, 1) OVER (ORDER BY Date) THEN 1
       WHEN Open < LAG(Open, 1) OVER (ORDER BY Date) THEN -1
       ELSE 0
  END AS daily_return
FROM `raunaks-r-class-project.Turkiyestock11.Data11`

Result 7: https://drive.google.com/file/d/1bxjqqhX9p_GTeaKL0ZjH6UAVPH4P2yW1/view?usp=sharing


*Question 8* What is the average daily volume?
*Answer 8*
SELECT 
t1.Date, AVG(t2.Volume) AS avg_daily_volume
FROM `raunaks-r-class-project.Turkiyestock11.Data11` AS t1
JOIN `raunaks-r-class-project.Turkiyestock11.Data11` AS t2
ON t1.Date = t2.Date
GROUP BY t1.Date;

Result 8: https://drive.google.com/file/d/15_L3bV5v4i6nsehaKTq6q5Yr8oWbYXzS/view?usp=sharing


*Question 9* What is the highest opening price with volume?
*Answer 9*
SELECT t1.Date, t1.Open, t2.Volume
FROM `raunaks-r-class-project.Turkiyestock11.Data11` AS t1
JOIN `raunaks-r-class-project.Turkiyestock11.Data11` AS t2
ON t1.Date = t2.Date
ORDER BY t1.Open DESC
LIMIT 5;

Result 9: https://drive.google.com/file/d/1GR3bSVY--35w5bImx6jiWPwnTG2-PuLL/view?usp=sharing


*Question 10* What is the lowest opening price with volume?
*Answer 10*
SELECT t1.Date, t1.Open, t2.Volume
FROM `raunaks-r-class-project.Turkiyestock11.Data11` AS t1
JOIN `raunaks-r-class-project.Turkiyestock11.Data11` AS t2
ON t1.Date = t2.Date

Result 10: https://drive.google.com/file/d/1rQhenBH2QZjyykRXJrVR3ZvwPk_NX_mb/view?usp=sharing
ORDER BY t1.Open ASC
LIMIT 5;
