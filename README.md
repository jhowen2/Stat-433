# Stat-433

---
title: "Stat 433 HW1"
author: "Jack Owen"
date: "9/21/2021"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


```{r}
#Implement packages needed for this to function properly
library(stringr)

#Read assign the url a variable while scanning it to a new one
url = "https://guide.wisc.edu/faculty"
raw_html_data = scan(url, "", sep = "\n")

#Initiate our four variables to be used when creating the data frame
name = c()
position = c()
specialty = c()
education = c()

#Sequence through the lines 132-157 where the data we need to extract can be found, loop through each element that contains its
#quantities of data in alphabetical order of last name
range = seq(from = 132, to = 157, by = 1)
for(i in range){
  #Split each person into their own element to be sorted
  abcLine = strsplit(raw_html_data[i], split = "<br/></p></li><li><p>")
 
  #Loop through each person
  for(j in abcLine[[1]]){
    #Break each person's values into 4 separate elements and remove unneeded string values
    person = strsplit(j, split = "<br/>")
    person[[1]][1] = str_remove(person[[1]][1], "<ul class=\"uw-people\"><li><p>")
   
    #Assign their elements to each respective future data frame variable
    name = append(name, person[[1]][1])
    position = append(position, person[[1]][2])
    specialty = append(specialty, person[[1]][3])
    education = append(education, person[[1]][4])
  }
}

#Apply 4 variables used to a data frame and write our .csv file
data = data.frame(name, position, specialty, education)
write.csv(data,"C:\\Users\\Jack\\Desktop\\Stat Class Work\\Stat 433\\Stat433HW1DataFrame.csv", row.names = TRUE)
str(data)
```
