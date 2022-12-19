# Enterococci bacteria levels in the water of Sydney Northern Beaches during the year 2018
The University of Sydney

SID: 490185362


# 1 Executive Summary

This report aims to investigate differences in Enterococci levels at
Sydney's Northern Beaches. We determined which site had the highest and
lowest Enterococci levels and its variation throughout 2018 by comparing
the box plot's medians and IQR's. Next, we examined the impact of
seasonal changes on the Enterococci levels.

The report's discoveries showed that the lowest Enterococci level was at
Avalon and Mona Vale beaches and the highest at Birdwood Park. We found
high fecal contamination during summer and autumn, whereas low fecal
contamination was during winter and spring. However, by carrying out a
hypothesis T-Test, we proved no significant impact of seasonal variation
on Enterococci levels.



# 2 Full Report

## 2.1 Initial Data Analysis (IDA)

### 2.1.1 Source of Data

```
data = read.csv("beaches.csv",na.strings = c("-9"), header = TRUE) Table= read.csv("Table_of_variables.csv", header = TRUE)
```
### 2.1.2 Complexity of Data

``` 
head(data, n=3 )  #Returns the first three rows of the data 
dim(data)  #Returns the dimension of data as rows and columns 
class(data) #Represent the type or style of data 
names(data)  #Returns the names of columns or variables 
data$Region=as.factor(data$Region)  #Changing all the character arguments to factors 
data$BeachId=as.integer(data$BeachId)
data$Council=as.factor(data$Council)
data$Site=as.factor(data$Site)
data$Date=as.factor(data$Date)
data$Enterococci..cfu.100ml.=as.integer(as.factor(data$Enterococci..cfu.100ml.))
data$Month=as.factor(data$Month)
data$Day.of.Week=as.factor(data$Day.of.Week)
str(data) #Returns the internal structure of the data
```

### 2.1.3 Classification of Variables

``` 
library(formattable) #A table of the variables in the data with their description and classification 
formattable(Table, 
            align =c("l","l","c","c"), 
            list(`Indicator Name` = formatter(
            "span", style = ~ style(color = "grey",font.weight = "bold"))))
```

### 2.1.4 Summary

#### 2.1.4.1 Source of Data :

The Enterococci bacteria data of Sydney Northern Beaches were collected
under the Beachwatch Water Quality Program and recorded by the NSW
Government Office of Environment and Heritage \[1\]. The data provides
an assessment of Enterococci bacterial level in the water and how
suitable each site is for swimming during 2018. The data set analysis
will help individuals make their decisions about when and where to swim.
It will also help to investigate community concerns surrounding
potential fecal or other sewage contamination in polluted water.

Enterococci bacteria are rarely present in clean water, and it mostly
appears due to the presence of fecal material by humans or animals
\[2\]. This type of bacteria has been linked to several diseases
affecting humans' overall health \[2\]. Moreover, It is negatively
affecting sports lovers and the economic values of the aquatic
resources. Therefore, possible stakeholders may include other
governments and scientists who could be interested in doing future
research on the Enterococci and its impact on society. This data set
could also be used to develop or implement programs by private sewage
disposal companies in order to reduce and solve the issue of
contamination in beaches due to the Enterococci level in the water.


#### 2.1.4.2 Classification of Variables :

The data set contains a 1276 set of observations and 10 variables. The
variables R classification is shown in the table above. Variables are X,
Beach ID, Region, Council, Site, Longitude, Latitude, Date, Month and
Enterococci level. The X variable is just a numerical marker for the
number of observations recorded in the data. Beach ID refers to the
site's identification number by the NSW Government Office of Environment
and Heritage. The region and council of which the data was taken in the
Northern Beaches Council in Northern Sydney. The longitude and latitude
were approximately measured to be 151.33 and 33.6, respectively \[1\].
The data includes the swimming site, the month and the exact date on
which the sample was obtained. Lastly, the Enterococci bacteria level
was measured in colony-forming units per 100mL \[CFU/100mL\] for each
sample \[3\]. 

#### 2.1.4.3 Reliability and Limitations:

This data set is reliable since it does not contain any missing data,
and it has a large sample size of 1276 throughout 22 different beaches
in the region. Hence, this data set is very suitable for monthly
analysis to distinguish any Enterococci level difference throughout the
seasons. However, the data set has limitations since there might be
other factors that affect the Enterococci level, such as climate, the
geography of the site, industrial presence, population and the area of
each beach. Also, the data is not appropriate for long term analysis as
it just includes sample taken during the year 2018. Other factors that
might affect scientists' analysis are a precise hourly timed measurement
and the method used in the laboratory to test the Enterococci level in
the samples. 

## 2.2 Research Question 1

Which swimming site of The Northern Beaches Council area in the Northern
Beaches region of Sydney has the highest Enterococci bacteria level? And
is there a particular month(s) where the Enterococci bacteria level was
high across most beaches? 

### 2.2.1 Graphical summary

``` 
Enterococci <- data[c("Site","Month","Enterococci..cfu.100ml.")] # Creating subsets of the data 
 # Isolating the level of Enterococci Bacteria at each swimming site
E_1 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Avalon Beach"]
E_2 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Bilarong Reserve (Narrabeen Lagoon)"] 
E_3 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Bilgola Beach"] 
E_4 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Birdwood Park (Narrabeen Lagoon)"] 
E_5 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Bungan Beach"] 
E_6 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Collaroy Beach"] 
E_7 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Dee Why Beach"] 
E_8 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Freshwater Beach"] 
E_9 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Long Reef Beach"] 
E_10 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Mona Vale Beach"] 
E_11 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Newport Beach"] 
E_12 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="North Curl Curl Beach"] 
E_13 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="North Narrabeen Beach"] 
E_14 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="North Steyne Beach"] 
E_15 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Palm Beach"] 
E_16 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Queenscliff Beach"] 
E_17 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Shelly Beach (Manly)"] 
E_18 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="South Curl Curl Beach"] 
E_19 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="South Steyne Beach"] 
E_20 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Turimetta Beach"] 
E_21 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Warriewood Beach"] 
E_22 = Enterococci$Enterococci..cfu.100ml.[Enterococci$Site =="Whale Beach"] 
#names of each swimming site
Beaches = c(" Avalon Beach","Bilarong Reserve","Bilgola Beach","Birdwood Park","Bungan Beach","Collaroy Beach","Dee Why Beach","Freshwater Beach","Long Reef Beach","Mona Vale Beach","Newport Beach","North Curl Beach","North Narrabeen Beach","North Steyne Beach","Palm Beach","Queenscliff Beach","Shelly Beach","South Curl Beach","South Steyne Beach","Turimetta Beach","Warriewood Beach","Whale Beach")
Beache= c(" Avalon","Bilarong","Bilgola","Birdwood Park","Bungan","Collaroy","Dee Why","Freshwater","Long Reef","Mona Vale","Newport","NO. Curl Curl","NO. Narrabeen","NO. Steyne","Palm","Queenscliff","Shelly","SO. Curl Curl","SO. Steyne","Turimetta","Warriewood","Whale")
#Box plot comparing the  Enterococci Bacteria level at each beach in the Northern Beaches region of Sydney
boxplot(E_1,E_2,E_3,E_4,E_5,E_6,E_7,E_8,E_9,E_10,E_11,E_12,E_13,E_14,E_15,E_16,E_17,E_18,E_19,E_20,E_21,E_22,
       ylim=c(0,110),names=Beache,las=2,horizontal =F,col="#D41C1C",cex.axis=0.7,
       ylab="Enterococci Bacteria Level [CFU/100ml]",
       main="Enterococci levels for all swimming sites in the Northern Beaches region")
```

``` 
 # Isolating the level of Enterococci Bacteria at of each month of 2018
one_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="January"] 
two_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="February"] 
three_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="March"] 
four_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="April"] 
five_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="May"] 
six_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="June"] 
seven_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="July"] 
eight_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="August"] 
nine_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="September"] 
ten_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="October"] 
eleven_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="November"] 
twelve_M = Enterococci$Enterococci..cfu.100ml.[Enterococci$Month =="December"] 
Month_name=c("January","February","March","April","May","June","July","August","September","October","November","December") 
#Box plot comparing the Enterococci Bacteria level across all months of 2018 in the Northern Beaches region of Sydney
boxplot(one_M,two_M,three_M,four_M,five_M,six_M,seven_M,eight_M,nine_M,ten_M,eleven_M,twelve_M,
       names=Month_name,las=2,horizontal = F,col="#7715BF",cex.axis=0.8,
       ylab="Enterococci Bacteria Level [CFU/100ml]",
       main="Enterococci levels during the months of 2018 in the Northern Beaches")
```
![](/images/image1.png)
![](/images/image2.png)

### 2.2.2 Numerical summary

``` 
# summary(Enterococci)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 1
median(E_1) 
IQR(E_1)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 2
median(E_2)
IQR(E_2)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 3
median(E_3) 
IQR(E_3) 
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 4
median(E_4) 
IQR(E_4) 
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 5
median(E_5)
IQR(E_5) 
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 6
median(E_6)  
IQR(E_6)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 7
median(E_7) 
IQR(E_7)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 8
median(E_8)
IQR(E_8)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 9
median(E_9)
IQR(E_9)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 10
median(E_10)
IQR(E_10)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 11
median(E_11)
IQR(E_11)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 12
median(E_12)
IQR(E_12)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 13
median(E_13)
IQR(E_13)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 14
median(E_14)
IQR(E_14)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 15
median(E_15)
IQR(E_15)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 16
median(E_16)
IQR(E_16)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 17
median(E_17)
IQR(E_17)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 18
median(E_18)
IQR(E_18)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 19
median(E_19)
IQR(E_19)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 20
median(E_20)
IQR(E_20)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 21
median(E_21)
IQR(E_21)
# Median and interquartile range (IQR) of Enterococci Bacteria level at  swimming site 22
median(E_22)
IQR(E_22)
All_sites= c( median(E_1),median(E_2),median(E_3),median(E_4),median(E_5),median(E_6),median(E_7),median(E_8),median(E_9),median(E_10),median(E_11),median(E_12),median(E_13),median(E_14),median(E_15),median(E_16),median(E_17),median(E_18),median(E_19),median(E_20),median(E_21),median(E_22))
max_1=max(All_sites)
```

``` 
# Median and interquartile range (IQR) of Enterococci Bacteria level during JAN of 2018 for all swimming site
median(one_M)
IQR(one_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during FEB of 2018 for all swimming site
median(two_M)
IQR(two_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during MAR of 2018 for all swimming site
median(three_M)
IQR(three_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during APR of 2018 for all swimming site
median(four_M)
IQR(four_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during MAY of 2018 for all swimming site
median(five_M)
IQR(five_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during JUN of 2018 for all swimming site
median(six_M)
IQR(six_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during JUL of 2018 for all swimming site
median(seven_M)
IQR(seven_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during AUG of 2018 for all swimming site
median(eight_M)
IQR(eight_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during SEP of 2018 for all swimming site
median(nine_M)
IQR(nine_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during OCT of 2018 for all swimming site
median(ten_M)
IQR(ten_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during NOV of 2018 for all swimming site
median(eleven_M)
IQR(eleven_M)
# Median and interquartile range (IQR) of Enterococci Bacteria level during DEC of 2018 for all swimming site
median(twelve_M)
IQR(twelve_M)
All_months= c(median(one_M),median(two_M),median(three_M),median(four_M),median(five_M),median(six_M),median(seven_M),median(eight_M),median(nine_M),median(ten_M),median(eleven_M),median(twelve_M))
max_2=max(All_months) #22
```

### 2.2.3 Graphical summary Analysis

The first box plot represents a comparison of Enterococci levels for all
swimming sites. The second box plot represents a comparison of
Enterococci levels for all months in 2018. We noticed strong outliers
for both plots and a wide spread of data in the first plot. Other very
large outliers in the first plot have been eliminated for clarity.


### 2.2.4 Numerical summary analysis

Median and interquartile range (IQR) were used in place of mean and
standard deviation (SD), as our data is skewed and due to the presence
of many strong outliers.


**Data reported as (median, IQR)** 

**---Enterococci bacteria level for each swimming site---**


Avalon and Mona Vale beaches have the lowest median and IQR. Hence, they
were suitable for swimming 

Palm, Turimetta, Bilgola, and North Narrabeen beaches also have a low
median, but the middle 50% (Q2 and Q3) values are much more spread,
which is displayed by the wider box length and higher IQR values.


Birdwood Park has the highest median and IQR. Hence, the water is very
polluted, and it is not safe for swimming.

**---Enterococci bacteria level for each month---** 

The medians and IQR are low and almost equal, with similar ranges from
July to December. Hence, it is safest to swim during winter and spring.


In contrast, the medians and IQR are very high and almost equal, with
similar ranges from January to June due to the high fecal contamination.
The highest Enterococci level was observed in March, where the lowest
was observed to be August. 

### 2.2.5 Summary:

To summarize, we found that Avalon and Mona Vale beaches have the lowest
Enterococci level. The water at Birdwood Park is most polluted, and the
site not safe for swimming. Next, we found a high level of fecal
contamination in the water in all sites in the Northern Beaches region
of Sydney during summer and autumn. It is safest to swim during winter
and spring. 

Researchers directly linked the high concentration of Enterococci in
polluted water and increased risk of illness for swimmers, particularly
those with lower immune function \[4\]. It has been suggested that other
factors lead to higher concentrations of Enterococci, such as rainfall
seasons and tides, which supports the large variations we found in
Enterococci level between summer and winter \[4\]. Researchers also
suggest a measuring Enterococci on hands and skin will help understand
post-collection stored water contamination and water contamination in
general. However, a limitation is that there are no current regulations
or standard methods for measuring Enterococci on the skin. However,
further work needs to be done to prove this idea \[4\]. 

## 2.3 Research Question 2

Does the change in season affect the Enterococci level in a swimming
site? 

### 2.3.1 Comparative Boxplots

``` 
summer=Enterococci[(Enterococci$Month=="December"|Enterococci$Month=="January"|Enterococci$Month=="February"),]   # summer months in Sydeny
winter=Enterococci[(Enterococci$Month=="June"|Enterococci$Month=="July"|Enterococci$Month=="August"),]  # winter months in Sydeny
boxplot(summer$Enterococci..cfu.100ml.,winter$Enterococci..cfu.100ml.,names=c("Summer","Winter"),las = 2,horizontal=T
,main="Enterococci levels during summer and winter of 2018")
```

![](/images/image3.png)


### 2.3.2 Levene's Test (Variance Test)

```
library(car) 
# Levene's Test for equality of variances
leveneTest( c(winter$Enterococci..cfu.100ml., summer$Enterococci..cfu.100ml.),
  factor(c(rep("winter",length(winter$Enterococci..cfu.100ml.)),              
           rep("summer",length(summer$Enterococci..cfu.100ml.)))))
```

### 2.2.3 Welch 2-Sample T-Test

We will use the Welch 2-Sample T-Test to test for the difference in
means of Enterococci levels during summer and winter of 2018 in the
Northern Beaches region of Sydney since the 2 samples have unequal
variance by the Levene's Test.

``` 
mu1=mean(summer$Enterococci..cfu.100ml.) # Mean of sample 1 
mu2=mean(winter$Enterococci..cfu.100ml.)  # Mean of sample 2 
n1=length(summer$Enterococci..cfu.100ml.) # Size of sample 1
n2=length(winter$Enterococci..cfu.100ml.) # Size of sample 2
sd1=sd(summer$Enterococci..cfu.100ml.) # Sample 1 standard deviation 
sd2=sd(winter$Enterococci..cfu.100ml.) # Sample 2 standard deviation 
se = sqrt(((sd1)^2/n1 + (sd2)^2/n2))  # Standard error
TestStat=(mu1-mu2-0)/se  # Test Statistic
numerator= (((sd1)^2/n1)+((sd2)^2/n2))^2
denominator1=(((sd1)^2/n1)^2) /(n1-1)
denominator2=(((sd2)^2/n2)^2) /(n2-1)
df= numerator/(denominator1+denominator2) # Degree of freedom
Pvalue =2*pt(abs(TestStat),608.16,lower.tail=F) # P-value
c(TestStat, Pvalue, df) 
```

``` 
t.test(summer$Enterococci..cfu.100ml.,winter$Enterococci..cfu.100ml.,var.equal=F) #speedy way in R
```



### 2.3.4 Analysis

#### 2.3.4.1 Hypotheses $H_0 vs H_1$

**---Null Hypotheses---** 

$H_0$: The mean of Enterococci levels in all swimming site is equal in both summer and winter seasons such that $\mu_1 = \mu_2$. 

**---Alternative Hypotheses---** 

$H_1$: The mean of Enterococci levels in all swimming site is not equal in summer compared to winter season $\mu_1 \neq \mu_2$. 

#### 2.3.4.2 Assumptions

**A1.** Both seasons are independent samples of each other. Hence, the
first assumption is satisfied. 

**A2.** Although the sample mean (sample sum) does not follow a normal
distribution, the sample size is big enough for the central limit
theorem to apply. Hence, the second assumption is satisfied.


**A3.** Using the Levene's Test (Variance Test) to compare the two
variances of winter and summer, we found the p-value to be
$7.068 \times 10^{-5}$, which is less than the significance level of
$0.05$. Hence, there is a significant difference between the two
variances(spread). However, This assumption is satisfied by using the
Welch 2-Sample T-Test. 

#### 2.3.4.3 Test statistic

We will use the Test Statistic to measure the difference between summer
and winter and what is expected based on $H_{0}$ : Test Statistic =
$\frac{OV-EV}{\hat{SE}}$, 

where the standard error is
${SE}=\sqrt{(\frac{S_1^2}{n_1}+\frac{S_2^2}{n_2})}$

and sample standard deviation is $S_{k}=\hat{SD_k}$ , $k=1,2$.


We substitute the values into the equations :  Observed
value = $\bar{x_1}-\bar{x_2}= 25.8-16.7=9.06$ 

Expected value = $0$ since our null hypothesis is that there is no
difference in population means. 

The sample size for both populations is equal such that $n_1=n_2=308$.
The sample standard deviation is $SD_1= 29.5$ and $SD_2= 26.8$. We
calculated the standard error to be ${SE}=2.27$. We substituted all the
values and calculated the Test Statistic to be $3.99$. We obtained the
degree of freedom using
$\nu=\frac{(\frac{S_1^2}{n_1}+\frac{S_2^2}{n_2})^2}{\frac{ (\frac{S_1^2}{n_1})^2}{n_1-1}+\frac{(\frac{S_2^2}{n_2})^2}{n_2-1}}$
= $608.16$ . 

Finally, we used the `t.test`function in R and obtained the exact values
for the Test Statistic and degree of freedom.

#### 2.3.4.4 P-value

We found the p-value, which is the probability of $H_{0}$ being true
equal to $7.343 \times 10^{-5}$ using both`pt` and `t.test` function in
R. 

$p = P(T > |$ Test Statistic
$|)= 2 \times P(T > | 3.992|)= 7.343 \times 10^{-5} < 0.05$.


The convention is to reject the null hypothesis if $p<0.05$. Since the
p-value is less than $0.05$, we do have enough evidence to reject the
null hypothesis, and so the data does provide evidence that
$\mu_1 \neq \mu_2$. 

#### 2.3.4.5 Conclusion

**---Statistical Conclusion:---** 

Mean values are statically different for winter and summer, which means
that the Enterococci level increases in summer and decreases in winter.
As the p-value \< 0.05, we reject the null hypothesis. We also have the
$95$% Confidence Interval for the mean difference $(4.60, 13.52)$, which
does not contain the null hypothesis value of zero. 

**---Scientific Conclusion:---**

Using the Welch 2-Sample T-Test, the data does not provide evidence that
the Enterococci level is not affected by the change in seasons. This
could be explained by the increase of Enterococci in the rainfall
seasons(during summer) and the decrease in drier weather (during
winter). 

# 3 References

\[1\] Enterococci data download. (n.d.). Retrieved February 07, 2021,
from https://www.environment.nsw.gov.au/beachapp/report_enterococci.aspx


\[2\] Indicators: Enterococci. (2016, August 16). Retrieved February 09,
2021, from
https://www.epa.gov/national-aquatic-resource-surveys/indicators-enterococci


\[3\] State of the beaches 2018-2019 \[PDF\]. (n.d.). DEPARTMENT OF
PLANNING, INDUSTRY & ENVIRONMENT.
https://www.environment.nsw.gov.au/beachwatch 

\[4\] Boehm AB, Sassoubre LM. Enterococci as Indicators of Environmental
Fecal Contamination. 2014 Feb 5. In: Gilmore MS, Clewell DB, Ike Y, et
al., editors. Enterococci: From Commensals to Leading Causes of Drug
Resistant Infection \[Internet\]. Boston: Massachusetts Eye and Ear
Infirmary; 2014-. Available from:
https://www.ncbi.nlm.nih.gov/books/NBK190421/
