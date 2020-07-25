```python

```

<h1>Analyzing US Economic Data and  Building a Dashboard  </h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some essential economic indicators from some data, you will then display these economic indicators in a Dashboard. You can then share the dashboard via an URL.
<p>
<a href="https://en.wikipedia.org/wiki/Gross_domestic_product"> Gross domestic product (GDP)</a> is a measure of the market value of all the final goods and services produced in a period. GDP is an indicator of how well the economy is doing. A drop in GDP indicates the economy is producing less; similarly an increase in GDP suggests the economy is performing better. In this lab, you will examine how changes in GDP impact the unemployment rate. You will take screen shots of every step, you will share the notebook and the URL pointing to the dashboard.</p>

<h2>Table of Contents</h2>
<div class="alert alert-block alert-info" style="margin-top: 20px">
    <ul>
        <li><a href="#Section_1"> Define a Function that Makes a Dashboard </a></li>
    <li><a href="#Section_2">Question 1: Create a dataframe that contains the GDP data and display it</a> </li>
    <li><a href="#Section_3">Question 2: Create a dataframe that contains the unemployment data and display it</a></li>
    <li><a href="#Section_4">Question 3: Display a dataframe where unemployment was greater than 8.5%</a></li>
    <li><a href="#Section_5">Question 4: Use the function make_dashboard to make a dashboard</a></li>
        <li><a href="#Section_6"> Save the dashboard on IBM cloud and display it</a></li>
    </ul>

</div>

<hr>

<h2 id="Section_1"> Define Function that Makes a Dashboard  </h2>




```python
import pandas as pd
from bokeh.plotting import figure, output_file, show,output_notebook
output_notebook()
```



<div class="bk-root">
    <a href="https://bokeh.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
    <span id="1002">Loading BokehJS ...</span>
</div>




we define the function <code>make_dashboard</code>


```python
def make_dashboard(x, gdp_change, unemployment, title, file_name):
    output_file(file_name)
    p = figure(title=title, x_axis_label='year', y_axis_label='%')
    p.line(x.squeeze(), gdp_change.squeeze(), color="firebrick", line_width=4, legend="% GDP change")
    p.line(x.squeeze(), unemployment.squeeze(), line_width=4, legend="% unemployed")
    show(p)
```

The dictionary  <code>links</code> contain the CSV files with all the data. The value for the key <code>GDP</code> is the file that contains the GDP data. The value for the key <code>unemployment</code> contains the unemployment data.


```python
links={'GDP':'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/coursera_project/clean_gdp.csv',\
       'unemployment':'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/coursera_project/clean_unemployment.csv'}
```

Create a dataframe that contains the GDP data and display the first five rows of the dataframe.</h3>






```python
import pandas as pd
csv_path_gdp=links['GDP']
df1=pd.read_csv(csv_path_gdp)
```




```python

df1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>level-current</th>
      <th>level-chained</th>
      <th>change-current</th>
      <th>change-chained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>274.8</td>
      <td>2020.0</td>
      <td>-0.7</td>
      <td>-0.6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>272.8</td>
      <td>2008.9</td>
      <td>10.0</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>300.2</td>
      <td>2184.0</td>
      <td>15.7</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>347.3</td>
      <td>2360.0</td>
      <td>5.9</td>
      <td>4.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>367.7</td>
      <td>2456.1</td>
      <td>6.0</td>
      <td>4.7</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_2"> Create a dataframe that contains the unemployment data. Display the first five rows of the dataframe. </h3>




```python
import pandas as pd
csv_path_unep=links['unemployment']
df2=pd.read_csv(csv_path_unep)
```




```python
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>3.750000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>6.050000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>5.208333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>3.283333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>3.025000</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_3">Display a dataframe where unemployment was greater than 8.5%. Take a screen-shot.</h3>


```python
df3=df1[df2['unemployment']>8.5]
df3

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>level-current</th>
      <th>level-chained</th>
      <th>change-current</th>
      <th>change-chained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>1982</td>
      <td>3345.0</td>
      <td>6491.3</td>
      <td>8.7</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1983</td>
      <td>3638.1</td>
      <td>6792.0</td>
      <td>11.1</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2009</td>
      <td>14418.7</td>
      <td>14418.7</td>
      <td>3.8</td>
      <td>2.6</td>
    </tr>
    <tr>
      <th>62</th>
      <td>2010</td>
      <td>14964.4</td>
      <td>14783.8</td>
      <td>3.7</td>
      <td>1.6</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2011</td>
      <td>15517.9</td>
      <td>15020.6</td>
      <td>4.2</td>
      <td>2.2</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_4">Use the function make_dashboard to make a dashboard</h3>






```python
x = pd.DataFrame(df1, columns=['date'])
x.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
    </tr>
  </tbody>
</table>
</div>






```python
gdp_change = pd.DataFrame(df1, columns=['change-current'])
gdp_change.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>change-current</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5.9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>






```python
unemployment = pd.DataFrame(df2, columns=['unemployment'])
unemployment.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.750000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6.050000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.208333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.283333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.025000</td>
    </tr>
  </tbody>
</table>
</div>






```python
title = "Unemployement stats according to GDP" 
```




```python
file_name = "index.html"
```




```python
make_dashboard(x=x, gdp_change=gdp_change, unemployment=unemployment, title=title, file_name=file_name)# Fill up the parameters in the following function:

```

    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead









<div class="bk-root" id="3af08d57-94f5-433e-bf2f-e652ed899dc3" data-root-id="1003"></div>












```python

```




```python

```




```python

```




```python

```




```python

```




```python

```




```python

```




```python

```




```python

```




```python

```












