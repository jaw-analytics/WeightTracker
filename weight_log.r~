#!/usr/bin/Rscript
# MIT License, John Williams, github @jaw-analytics
# takes 2 args, weight in kg, and calories consumed that day
# assumes user has R v.3.2.0 or greater installed and is on a unix/linux system
# usage  ./weight_log.r 90 2000, where 90 is weight and 2000 is kcal consumed
args <- commandArgs(TRUE)

day <- format(Sys.Date(), "%m/%d")
# calculate BMR via Mifflin-St Jeor Equations:
#Mifflin, M. D., S. T. St Jeor, L. A. Hill, B. J. Scott, S. A. Daugherty, and Y. O. Koh. 1990. “A New Predictive Equation for Resting Energy Expenditure in Healthy Individuals.” The American Journal of Clinical Nutrition 51 (2): 241–47.

# m = mass in kg
# h = height in cm
# a = age in years
# g = gender, (-161 if female, +5 if male)
m <- as.numeric(args[1])
# change h to be your height
h <- 171
a <- 31
g <- 5
BMR <- (10.0*m + 6.25*h - 5.0*a + g)
BMI <- m/(1.71^2)
# log estimate of calories consumed
kcal <- as.numeric(args[2])

# log caloric balance for day, must be negative
balance <- kcal - BMR
# write weight to log
cat(sprintf("%s\t%2.1f\t%2.2f\t%4.f\t%4.f\t%4.f\n", day, m, BMI, BMR, kcal, balance), file="log.txt", append=TRUE, sep="\t")
# read current log
log <- read.table(file="log.txt", header=TRUE, sep="\t")
#
#
#
#
# CREATE TIME SERIES
library(ggplot2)
library(forecast)
ts_weight <- ts(log$Weight_kg)
ts_bmi <- ts(log$BMI)
ts_balance <- ts(log$Kcal_Deficit)
ts_weight <- HoltWinters(ts_weight, beta=F,gamma=F)
ts_bmi <- HoltWinters(ts_bmi, beta=F, gamma=F)
ts_balance <- HoltWinters(ts_balance, beta=F, gamma=F)
# creates forecast. Days are set to (h=5), that can be changed for a longer forecast. If it is changed, correct the 'main' title in the plots below to reflect this.
weight_forecast <- forecast.HoltWinters(ts_weight, h=5)
bmi_forecast <- forecast.HoltWinters(ts_bmi, h=5)
balance_forecast <- forecast.HoltWinters(ts_balance, h=5)
# plot forecasts as weight_plots.svg
svg("weight_plots.svg")
par(mfrow=c(3,1))
plot.forecast(weight_forecast, main="5 Day Weight Forecast", xlab="Day", ylab="Weight (kg)")
plot.forecast(bmi_forecast, main="5 Day BMI Forecast", xlab="Day", ylab="BMI")
plot.forecast(balance_forecast, main="5 Day Caloric Deficit Forecast", xlab="Day", ylab="Energy Deficit (kcal)")
dev.off()
