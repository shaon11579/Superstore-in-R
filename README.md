Here is the code.

# Clearing variables 
rm(list = ls())

library(arules)
library(arulesViz)

# set the working directory
setwd("/Users/mhasan1/Desktop")

#read/import csv file into R
trans_mat<-read.csv("Superstore",header=TRUE,sep=",")

#convert it into a data matrix
a_matrix<-data.matrix(trans_mat)

#remove the transaction_ID column i.e., column 1
a_matrix<-a_matrix[,-1]

#use logical function to convert binary to T/F
basket2<-apply(a_matrix,2,as.logical)

#Now coerce it into a matrix
basket<-as(as.matrix(basket2),"transactions")

# Using mine association rules - Apriori Algorithm 
rules <- apriori(basket, parameter = list(support=0.03, confidence=0.8))

rules1<- apriori(basket, parameter = list(support=0.04, confidence=0.8))

inspect(head(rules, n=3 , by ="lift"))

inspect(head(rules1, n=3 , by ="lift"))

plot(rules)

#parallel Cordinates plot 
plot(rules, method = "paracoord")

plot(rules, method = "paracoord", control = list(reorder = TRUE))




