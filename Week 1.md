
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

   
<div style="color:white ;text-align: right"> Tyler Lane & Caroline Gao </div>




Road to R
========================================================
* C/C++, FORTRAN, MATLAB, VB, R, Python, STATA, SAS, SPSS
* C/C++, FORTRAN, MATLAB, VB, R, Python, STATA, SAS
* C/C++, MATLAB, VB, R, Python, STATA, SAS
* C/C++, MATLAB, R, Python, STATA, SAS
* C/C++, R, Python, STATA, SAS
* C/C++, R, Python, STATA
* R, Python, STATA
* R, STATA
* R


STATA v.s.R
========================================================

<div class="footer" style="margin-top:-150px;font-size:100%;" align="left">
R may not be your most prefered tool to start with. However the more you use it, the more likely you are going to use it.</div>

<br />
STATA
* Easy to start with
* Standard applications
* Survey analysis, Multiple Imputations...

***
<br />
R
* Something new 
* Something fancy
* something pretty


Reproducibility
========================================================
* <div style="color:black ;font-size: 80% "> Reproducibility</div>
* <div style="color:black ;font-size: 90% "> Reproducibility</div>
* <div style="color:black ;font-size: 100%" > Reproducibility</div>
* <div style="color:black ;font-size: 110%" > Reproducibility</div>
* <div style="color:black ;font-size: 120%"> Reproducibility</div>
* <div style="color:black ;font-size: 130%"> Reproducibility</div>

<div class="footer" style="margin-top:-140px;font-size:120%;" align="centre">
Make sure every step of yor analysis is `reproducible'!</div>

Reproducibility
========================================================
Project management 
* Keep source data in zip file
* Store all data and analyses code on netdrive 
* Dcumentation
* ...

Related to R
* Pay attention to random number generator
* Separate data cleaning code and analysis code
* Git version control
* ...

Reproducibility
========================================================

![Alt Text](http://revolution-computing.typepad.com/.a/6a010534b1db25970b01bb0794c2fc970d-800wi) 

* Ignoring reproducibility??
* Tracking package dependencies per project


Reproducibility/Reusability
========================================================
class: small-code
My code from 10 years ago: 
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
My code now: 


```r
#Extract median, range and max PM2.5 for each SA2 areas
fire_area<-Ambo_timeseries %>%
    #exclude data during industrial action
    select(SA2_NAME11,All, pop, Date) %>% 
    na.omit() %>%
    #add full condition names
    mutate(rate=All*10000/pop) %>% 
    dplyr::select(SA2_NAME11, Date,  rate ) %>% 
    #fill 0 for those SA2 without any record for a condtion 
    group_by(SA2_NAME11) %>% 
    summarise(Median=format(round(quantile(rate, probs=0.5),1), nsmall=1),
              "Interquartile range"= paste0(format(round(quantile(rate, probs=0.25),1),nsmall=1),"-" , format(round(quantile(rate, probs=0.75),1),nsmall=1)),
              "Median "=format(round(quantile(rate[Date>=Start_date& Date<=End_date], probs=0.5),1), nsmall=1) ,
              "Interquartile range "= paste0(format(round(quantile(rate[Date>=Start_date& Date<=End_date], probs=0.25),1),nsmall=1),"-" , format(round(quantile(rate, probs=0.75),1),nsmall=1)))
```

Reusability
========================================================
* Always try to write 'pretty' code
* Naming of datasets and variables 
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





Happy coding
========================================================
$~$

![Alt Text](https://78.media.tumblr.com/61b853de39924e1bf261ff26f363a98e/tumblr_inline_o539xbgPGh1ssbz72_500.gif)
