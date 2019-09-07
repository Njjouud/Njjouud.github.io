---
layout: page
title: WomenTechWomenYes
---

<div class="page">
  <h1 class="page-title">WomenTechWomenYes Gala</h1>
  <h2 class="lead">Overview</h2>
  <p>
    This analysis is for (WTWY), to help their street teams to gain more signups for their gala that will take place on the first of June.As a Data scientist team, we conducted an EDA on New York Subway data.
  </p>
  <h2 class="lead">Work Stages</h2>
  <h3 class="lead">Data Cleaning</h3>
  <p>
    Firstly we striped out the white spaces from the dataset columns and parse date and time columns to timestamp., secondly we assured that there is no NaN values and negative values, thirdly we extracted the actual entries and exits values and stored them into inflow and outflow columns, fourthly we got rid of the outliers by setting a limit for the entries and exits values.
  </p>
  <h3 class="lead">Data Visulaization</h3>
We started by getting the most crowded stations we are avoiding torist by excluding airport stations but luckly airport stations weren't part of the most crowded stations in New York.   

  ![stations]({{ site.url }}/images/stations.png)  As the graph telling us that there's a huge differance between the 1st crowded statios and the 10th so as a result we recommend to focus on the top 5 stations.

After that we looked for the most crowded days in a week.   ![days]({{ site.url }}/images/days.png)

And then we looked for the most crowded time in a day.

![time]({{ site.url }}/images/time.png)

 Last but not least, we looked for the most crowded turnstiles from the top five crowded stations.  

![turnstiles]({{ site.url }}/images/turnstiles.png)

## Conclusion

We recommend the client to depoly street teams in these stations 34-ST_PENN STA, GRD CNTRL, 34- ST HERALED, 14 ST_UNION and TIMES SW-42 ST. On weekdays from 8am till 11am. And target the mentioned turnstiles.


Have questions or suggestions? Feel free to [email me](mailto:njoud.algifari@gmail.com).

Thanks for reading!
