# Violin Plot

## Overview
This function (`processViolin()`) allows you to create a violin chart using [Highcharts](https://www.highcharts.com/): 

*Check [codePen demo](https://codepen.io/mushigh/pen/eYJXjVe)*


![violin](img/violin-demo.png)


## Installation
You can either add the function direclty in your code (see [violin-plot.js](violin-plot.js)) or use the following [link](https://marketing-demo.s3-eu-west-1.amazonaws.com/violinFunction/processViolin.js) (see below):
````
<script src="https://marketing-demo.s3-eu-west-1.amazonaws.com/violinFunction/processViolin.js"></script>
````

## Description
Here is the description of the function’s parameters:
* **step** is the minimum data set unit. The step is used to sample the data set and create the KDE.
* **precision** is used to refine the violin plot at the extremities and in the thin spots, the smallest this parameter is the more points you get on the extremities and the thin spots on the chart.
* **densityWidth** is used to widen the violin. This parameter should be equal to 1 to reflect the result of the KDE values. Nevertheless, for visibility purposes, you are free to change the densityWidth to get a wider and visible shape. 
* **arg**s is one or many arrays that represent the data set. In our case, args is four arrays of weight athletes, one array for each discipline.

The function `processViolin()` returns a set of three arrays:
* **xiData** is the xAxis data generated using the step and the range of the athletes’ weights data.
* **results** includes all the violin charts data.
* **stat** is the array with all the descriptive statistical coefficients.  

## Example
Check [codePen demo](https://codepen.io/mushigh/pen/eYJXjVe)

```
let arr1 = [1,2,2,2,5,8,9,9], arr2=[3,4,5], arr3=[1,2,2,3];
let step = 1,
    precision = 0.00000000001,
    width = 3;
let data = processViolin(step,precision,width,arr1, arr2,arr3);
let violin1 = data.results[0],
      violin2 = data.results[1],
      violin3 = data.results[2];
Highcharts.chart("container", {
...
series: [
        {
          name: "Violin 1",
          color: "#ffa8d4",
          data: violin1
        },
        {
          name: "Violin 2",
          color: "#a8d4ff",
          data: violin2
        },
        {
          name: "Violin 3",
          color: "#ffa956",
          data: violin3
        }
      ]
});
```

## Remark
The function is built around the [kernel density estimation (KDE)](https://www.highcharts.com/blog/tutorials/data-science-and-highcharts-kernel-density-estimation/).
