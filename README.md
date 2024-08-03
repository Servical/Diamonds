---
title: "Diamond Data"
author: "Noah James"
date: "2024-05-20"
output:
  pdf_document: default
  html_document: default
---  
##Packages Inovolved  
The tidyverse package is the main package needed for this analysis, with it's included ggplot2 also being crucial for the visualizations. The data set I'm looking at, the "diamonds" data set, is also included in the ggplot2 package.

```{r}
install.packages('tidyverse')
```

```{r}
library('tidyverse')
```

I took an initial look at the data so that I could see what sort of data was contained within the columns using the head, structure, and column name functions.

```{r}
head(diamonds)
str(diamonds)
colnames(diamonds)
```

## Data Transformation
I notice that some of the column names should be changed, specifically the carat column should be changed to carat_new and cut should be renamed to cut_new. I use the rename() function in R to acconmplish this. 

```{r}
rename(diamonds, carat_new=carat, cut_new=cut)
```

I also realize that the cut column will need to be transformed in a numeric value in order for me to figure out what the average cut of our diamonds is. The is.numeric() funciton was the ability to do this for me. 

```{r}
cut_as_numeric <- as.numeric(diamonds$cut_new)
cut_as_numeric
```


## Analysis
I want to find out what the average carat of our diamonds are, so I use the summarize and mean function to do this.

```{r}
summarize(diamonds, mean_carat= mean(carat))
```

Next, I figure out what the average cut is.

```{r}
summarize(diamonds, mean_cut = mean(cut_as_numeric))
```

As the mean cut is 3.904097, the average cut is closest to the cut that is labeled as "4". Since the quality goes from "Fair","Good","Very Good","Premium", and "Ideal", 4 corresponds to Premium, and the average cut is a Premium Cut.  

## Graph Cut&Carat with Price

```{r}
ggplot(data=diamonds,aes(x=carat,y=price,color=cut))+
  geom_point()+
  labs(title="Diamond Carat v.s. Price",color="Cut New", x="Carat New",y="Price")+
  geom_jitter()
    
```

#Insights  
It is clear that both diamond carat and diamond quality are positively correlated with price, meaning that having the highest carat diamond of ideal quality could be sold for the highest price. However, we have only three diamonds above 4 carat, indicating that it may not be currently possible to refine such an object; further analysis and research is required on that topic. However, as things are, we should prioritize production of 1 to 2.5 carat diamonds of Very Good to Ideal quality to maximize revenue. 
