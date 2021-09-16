---
layout: docwithnav-trendz
assignees:
- vparomskiy
title: Calculated Fields
description: Trendz Calculated Fields
---

* TOC
{:toc}

Calculated fields are one of the most powerful features for KPI monitoring and prediction. 
Based on the input data, calculated fields allow you to run statistical functions and create new data items by applying calculations. 
As Trendz Analytics processes the calculations on the fly, no data from ThingsBoard database will be damage.
 And no additional load will be applied.


## Simple calculation

Let's assume that sensor submit boiler temperature in Celsius and we want convert it to Fahrenheit:

* Drop **Calculated** field from left navigation to the **Y axis** section
* Open field configration and write transformation function

{% highlight javascript %}
    var celsius = avg(Machine.boilerTemp);
    var fahrenheit = celsius*1.8 + 32;
    return fahrenheit;
{% endhighlight %}   

![image](/images/trendz/calculated-simple.png)

## Multiple fields for calculation

In this example we have Apartment asset that has 2 sensors installed - HeatMeter and EnergyMeter. Both sensors submit how much energy was consumed.
Also Apartment has area attribute that contains apartment size. We want calculate total energy consumed by HeatMeter and EnergyMeter 
in Apartment per square meter. Let's break it to subtasks:

* Get amount of energy consumed by HeatMeter - **heatConsumption** telemetry 
* Get amount of energy consumed by EnergyMeter - **energyConsumption** telemetry 
* Get Appartment size - **area** attribute
* Sum **heatConsumption** and **energyConsumption**
* Devide it by **area**
  
For implementing this we need to:
* Drop **Calculated** field from left navigation to the **Y axis** section
* Open field configration and write transformation function  
  
{% highlight javascript %}
    var energy = sum(energyMeter.energyConsumption);
    var heat = sum(heatMeter.heatConsumption);
    var size = uniq(apartment.area);
    
    return (energy + heat) / size;
{% endhighlight %}   

![image](/images/trendz/calculated-complex-config.png)

![image](/images/trendz/calculated-complex-result.png)

## Get original field value

Before applying transformation you need to get a reference to the original field value. Here is an example how to do this:

```
var temp = avg(Machine.temperature);
```

* avg() - aggregation function
* Machine - Entity Name (it can be Asset Type or Device Type)
* temperature - Field Name

**All 3 parts are required**, you can not access original field value without aggregation function. 

If original field value is an attribute, entity name or owner name - you should use **uniq()** aggregation function.

## Supported Aggregation Functions

JSEditor for calculated fields supports following aggregation functions:

* avg()
* sum()
* min()
* max()
* count()
* latest()
* uniq()
* delta() 

Each function allows only 1 argument - reference to the filed on format EntityName.fieldName. For example:

```
sum(Machine.temperature)
```

Aggregation function applied to a grouped dataset. Find more details about [Grouping and Aggregation in this article](/docs/trendz/data-grouping-aggregation/)

## Language

Calculated Fields use Javascript as a language for writing transformation function. Inner Engine provide 100% support
of ECMAScript 5.1

## Next Steps

{% assign currentGuide = "CalculatedFields" %}{% include templates/trndz-guides-banner.md %}