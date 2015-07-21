# WeightTracker
R script to track and forecast weight and BMI

This script uses the Mifflin-St Jeor Equations to calculate Resting Energy Expenditure, or Basal Metabolic Rate. 

A log is created as log.txt, and that file is used as the basis for a Holt-Winters forecast of 5 days. The results of the forecast are three plotted time series, of BMI, Body Weight, and Calories above or below BMR.

Script assumes R v. 3.2.0 or greater installed, tested on a Linux system where the shell-accessible R directory is:
 #!/usr/bin/Rscript, and takes 2 variables.

Run as:

./weight_log.r X Y, where X is a numerical weight (in kg) and Y is a numerical count of calories consumed that day (in kcal or "big C" Calories)


Requires ggplot2 and forecast libraries
