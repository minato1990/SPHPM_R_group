
<style>


/* slide titles */
.reveal h3 { 
  font-size: 75px;
  color: black;
}

.small-code pre code {
  font-size: 1em;
}
.footer {
    color: red; background: #E8E8E8;
    position: fixed; top: 90%;
    text-align:left; width:100%;
}

</style>


R training
========================================================
font-family: 'Helvetica'

![Alt Text](https://78.media.tumblr.com/e1712952f6eb24f418a997a8da6ae831/tumblr_ou1znif6LW1w4t58uo1_500.gif)

   
<div style="color:white ;text-align: right"> Caroline Gao & Tyler Lane </div>


Welcome to the first SPHPM R Group Meeting!
========================================================
* Purpose: 
  - Create a community of R users
  - Provide some training
  - Tips on best practice




What stats packages do you currently use?
========================================================
* MS Excel 
  - My main stats software when I was a statistician in the UK govt!
* SPSS
* STATA
* SAS
* Python
* R
* Something else?


Why use R?
========================================================
class: small-code
* It's free!
  - Skill you can carry outside academia
* Extremely flexible
  - User-developed packages to do just about anything
* Vibrant, passionate, and supportive user community
* Built-in datasets to practice with

```r
# To see this, enter this code in your console
ls("package:datasets")
```


Built-in package: mtcars
========================================================
class:small-code

```
                     mpg cyl  disp  hp drat    wt  qsec vs am gear carb
Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2
```


Pretty graphs
========================================================
class: small-code
<div align = "center">

```r
# load necessary package
library(ggplot2) 
# convert target variable to factor with meaningful labels
mtcars$Transmission <- factor(mtcars$am, 
                       levels = c(0, 1), 
                       labels = c("Automatic", "Manual"))
# Plot
ggplot(mtcars, aes(x = mpg, fill = Transmission)) + 
  geom_density(alpha = 0.5) + 
  labs(title = "Fuel efficiency by transmission type", 
       x = "Miles per gallon", y = "Distribution") 
```

![plot of chunk my plot](Week 1-figure/my plot-1.png)



Testing transmission/fuel with simple code
========================================================
class: small-code

```r
# Is fuel efficiency normally distributed?
shapiro.test(mtcars # function for normal test(data.frame
             $mpg) # variable, denoted with '$'
```

```

	Shapiro-Wilk normality test

data:  mtcars$mpg
W = 0.94756, p-value = 0.1229
```


```r
# Not normally distributed; need nonparametric test (Mann-Whitney U)
wilcox.test(mtcars$mpg ~ mtcars$am)
```

```

	Wilcoxon rank sum test with continuity correction

data:  mtcars$mpg by mtcars$am
W = 42, p-value = 0.001871
alternative hypothesis: true location shift is not equal to 0
```



Disadvantages of R
========================================================
* Steep learning curve
* Less support than commercial software
* FRUSTRATING!
![Alt Text](https://alfahir.hu/sites/default/files/styles/szeles/public/indexfotos/2018-04/g-ucpo_0.gif?itok=zwB7bbTC)



My unsolicited advice
========================================================
* Learning R is opposite of learning a musical instrument
* Guitar: Learn scales, then Wonderwall
* R: Learn Wonderwall, then scales

![Alt Text](http://31.media.tumblr.com/tumblr_m8mm9zMnGo1qkyzquo1_500.gif)



Key points we'll talk about today
========================================================
* Reproducibility
* Readability/reusability
* Version control
  - Tracking package dependencies per project using packrat or checkpoint
![Alt Text](http://revolution-computing.typepad.com/.a/6a010534b1db25970b01bb0794c2fc970d-800wi) 



Reproducibility
========================================================
Project management 
* Keep source data in zip file
* Store all data and analyses code on netdrive 
* Documentations
* ...

Related to R
* Pay attention to random number generator
* Separate data cleaning code and analysis code
* Git version control
* ...



Reproducibility/Reusability
========================================================
class: small-code
Caroline's code from 10 years ago (???, like Finnegans Wake)
```{ r,eval=FALSE}
particlechange<-c(50)
for( g in 1:30)
{
particlenum<-c(0)
particlereach1<-c(0)
##----------------
x<-seq(0.1,3,length=30)
y<-seq(0.1,6,length=30)
tcid<-c(1:60)##0.01 dilution
for(i in 0:60)
{
   if(i<10)
   tcid[i]=10^(4.25-0.81*(10-i)/10)/dilu
   else 
   tcid[i]=10^(4.25-0.81*(i-10)/10)/dilu
}
f<-function(x,y){
r<-1-exp(-4*1*0.001386*0.48*particlesum[x*10]*tcid[y*10]*1000000*0.001/(3*(x*0.2679+0.0098)^2))
}
z<-outer(x,y,f)
```

Reproducibility/Reusability
========================================================
class: small-code
Caroline's code now (clear like Hemingway)

```r
#Extract median, range and max PM2.5 for each SA2 areas
fire_area<-Ambo_timeseries %>%
    select(SA2_NAME11,All, pop, Date) %>% 
    #exclude data during industrial action
    na.omit() %>%
    #calculate rates
    mutate(rate=All*10000/pop) %>% 
    #obtain median and interquartile range by SA2 name
    group_by(SA2_NAME11) %>% 
    summarise(Median=format(round(quantile(rate, probs=0.5),1), nsmall=1),
              "Interquartile range"= paste0(format(round(quantile(rate, probs=0.25),1),nsmall=1),"-" , format(round(quantile(rate, probs=0.75),1),nsmall=1)))
```

Reusability
========================================================
* Always try to write 'pretty' code
* Think about naming of datasets and variables 
* Try to write functions for repetitive work

Efficiency
========================================================

![Alt Text](https://csgillespie.github.io/efficientR/figures/f0_web.png)

Efficiency
========================================================

* Efficient programming
* Efficient workflow
* Efficient input/output
* Efficient data carpentry
* Efficient optimisation

House keeping
========================================================
* Install R and Rstudio
* Install package: knit, ggplot2, dplyr, tidyr
* Download Github study material from: https://github.com/CarolineXGao/SPHPM_R_group (use the Clone or download button).
* There are some additional study materials provided in Part 1 (coursea video lectures, swirl etc) feel free to get started before next week




Happy coding!
========================================================
$~$

![Alt Text](https://78.media.tumblr.com/61b853de39924e1bf261ff26f363a98e/tumblr_inline_o539xbgPGh1ssbz72_500.gif)
