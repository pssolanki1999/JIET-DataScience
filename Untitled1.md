```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import style
%matplotlib inline

import plotly
import plotly.express as px
import plotly.graph_objects as go
plt.rcParams['figure.figsize']=20,20
import cufflinks as cf
import plotly.offline as pyo
from plotly.offline import init_notebook_mode,plot,iplot
import folium
```


```python
pyo.init_notebook_mode(connected=True)
cf.go_offline()
```


<script type="text/javascript">
window.PlotlyConfig = {MathJaxConfig: 'local'};
if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
if (typeof require !== 'undefined') {
require.undef("plotly");
requirejs.config({
    paths: {
        'plotly': ['https://cdn.plot.ly/plotly-latest.min']
    }
});
require(['plotly'], function(Plotly) {
    window._Plotly = Plotly;
});
}
</script>




<script type="text/javascript">
window.PlotlyConfig = {MathJaxConfig: 'local'};
if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
if (typeof require !== 'undefined') {
require.undef("plotly");
requirejs.config({
    paths: {
        'plotly': ['https://cdn.plot.ly/plotly-latest.min']
    }
});
require(['plotly'], function(Plotly) {
    window._Plotly = Plotly;
});
}
</script>




```python
data = pd.read_excel(r"C:\Users\pssol\Covid cases in India.xlsx")
```


```python
data
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
      <th>S. No.</th>
      <th>Name of State / UT</th>
      <th>Total Confirmed cases (Indian National)</th>
      <th>Total Confirmed cases ( Foreign National )</th>
      <th>Cured</th>
      <th>Death</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Andhra Pradesh</td>
      <td>12</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Chhattisgarh</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Delhi</td>
      <td>38</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Gujarat</td>
      <td>43</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Haryana</td>
      <td>16</td>
      <td>14</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Himachal Pradesh</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Karnataka</td>
      <td>20</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Kerala</td>
      <td>131</td>
      <td>7</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Madhya Pradesh</td>
      <td>23</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Maharashtra</td>
      <td>144</td>
      <td>3</td>
      <td>15</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Odisha</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>Puducherry</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>Punjab</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>Rajasthan</td>
      <td>41</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Tamil Nadu</td>
      <td>32</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Telengana</td>
      <td>34</td>
      <td>11</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>Chandigarh</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>Jammu and Kashmir</td>
      <td>18</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>Ladakh</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>Uttar Pradesh</td>
      <td>42</td>
      <td>1</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21</td>
      <td>Uttarakhand</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>West Bengal</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23</td>
      <td>Bihar</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <td>24</td>
      <td>Mizoram</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>25</td>
      <td>Goa</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>26</td>
      <td>Manipur</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['Total Cases']=data['Total Confirmed cases (Indian National)']+data['Total Confirmed cases ( Foreign National )']
```


```python
data
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
      <th>S. No.</th>
      <th>Name of State / UT</th>
      <th>Total Confirmed cases (Indian National)</th>
      <th>Total Confirmed cases ( Foreign National )</th>
      <th>Cured</th>
      <th>Death</th>
      <th>Total Cases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Andhra Pradesh</td>
      <td>12</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Chhattisgarh</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Delhi</td>
      <td>38</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Gujarat</td>
      <td>43</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Haryana</td>
      <td>16</td>
      <td>14</td>
      <td>11</td>
      <td>0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Himachal Pradesh</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Karnataka</td>
      <td>20</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
      <td>20</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Kerala</td>
      <td>131</td>
      <td>7</td>
      <td>11</td>
      <td>0</td>
      <td>138</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Madhya Pradesh</td>
      <td>23</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>23</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Maharashtra</td>
      <td>144</td>
      <td>3</td>
      <td>15</td>
      <td>4</td>
      <td>147</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Odisha</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>Puducherry</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>Punjab</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>29</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>Rajasthan</td>
      <td>41</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Tamil Nadu</td>
      <td>32</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>35</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Telengana</td>
      <td>34</td>
      <td>11</td>
      <td>1</td>
      <td>0</td>
      <td>45</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>Chandigarh</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>Jammu and Kashmir</td>
      <td>18</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>18</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>Ladakh</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>Uttar Pradesh</td>
      <td>42</td>
      <td>1</td>
      <td>11</td>
      <td>0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21</td>
      <td>Uttarakhand</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>West Bengal</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>11</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23</td>
      <td>Bihar</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>7</td>
    </tr>
    <tr>
      <th>23</th>
      <td>24</td>
      <td>Mizoram</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>25</td>
      <td>Goa</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>25</th>
      <td>26</td>
      <td>Manipur</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_cases_overall=data['Total Cases'].sum()
print("the total number cases till now in india is:",total_cases_overall)
```

    the total number cases till now in india is: 729
    


```python
data['Active Cases']=data['Total Cases']-(data['Death']+data['Cured'])
```


```python
data
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
      <th>S. No.</th>
      <th>Name of State / UT</th>
      <th>Total Confirmed cases (Indian National)</th>
      <th>Total Confirmed cases ( Foreign National )</th>
      <th>Cured</th>
      <th>Death</th>
      <th>Total Cases</th>
      <th>Active Cases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Andhra Pradesh</td>
      <td>12</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>12</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Chhattisgarh</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Delhi</td>
      <td>38</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>39</td>
      <td>32</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Gujarat</td>
      <td>43</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>43</td>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Haryana</td>
      <td>16</td>
      <td>14</td>
      <td>11</td>
      <td>0</td>
      <td>30</td>
      <td>19</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Himachal Pradesh</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Karnataka</td>
      <td>20</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
      <td>20</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Kerala</td>
      <td>131</td>
      <td>7</td>
      <td>11</td>
      <td>0</td>
      <td>138</td>
      <td>127</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Madhya Pradesh</td>
      <td>23</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>23</td>
      <td>22</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Maharashtra</td>
      <td>144</td>
      <td>3</td>
      <td>15</td>
      <td>4</td>
      <td>147</td>
      <td>128</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Odisha</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>Puducherry</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>Punjab</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>29</td>
      <td>28</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>Rajasthan</td>
      <td>41</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>43</td>
      <td>40</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Tamil Nadu</td>
      <td>32</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>35</td>
      <td>33</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Telengana</td>
      <td>34</td>
      <td>11</td>
      <td>1</td>
      <td>0</td>
      <td>45</td>
      <td>44</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>Chandigarh</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>7</td>
      <td>7</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>Jammu and Kashmir</td>
      <td>18</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>18</td>
      <td>16</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>Ladakh</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>Uttar Pradesh</td>
      <td>42</td>
      <td>1</td>
      <td>11</td>
      <td>0</td>
      <td>43</td>
      <td>32</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21</td>
      <td>Uttarakhand</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>West Bengal</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>11</td>
      <td>10</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23</td>
      <td>Bihar</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>7</td>
      <td>6</td>
    </tr>
    <tr>
      <th>23</th>
      <td>24</td>
      <td>Mizoram</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>25</td>
      <td>Goa</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>25</th>
      <td>26</td>
      <td>Manipur</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.style.background_gradient(cmap='Reds')
```




<style  type="text/css" >
    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col0 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col2 {
            background-color:  #fee8de;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col4 {
            background-color:  #feeae0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col6 {
            background-color:  #fee8de;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col7 {
            background-color:  #fee8dd;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col0 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col2 {
            background-color:  #fff0e8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col6 {
            background-color:  #fff0e8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col7 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col0 {
            background-color:  #fee8dd;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col2 {
            background-color:  #fcb89e;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col3 {
            background-color:  #fee9df;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col4 {
            background-color:  #fc8a6a;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col6 {
            background-color:  #fcb89e;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col7 {
            background-color:  #fcbda4;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col0 {
            background-color:  #fee1d4;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col2 {
            background-color:  #fcad90;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col5 {
            background-color:  #ca181d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col6 {
            background-color:  #fcaf93;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col7 {
            background-color:  #fca98c;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col0 {
            background-color:  #fdd7c6;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col2 {
            background-color:  #fee4d8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col3 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col4 {
            background-color:  #d01d1f;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col6 {
            background-color:  #fdcbb6;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col7 {
            background-color:  #fedbcc;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col0 {
            background-color:  #fdcab5;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col2 {
            background-color:  #fff2eb;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col6 {
            background-color:  #fff2eb;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col7 {
            background-color:  #fff2ec;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col0 {
            background-color:  #fcbea5;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col2 {
            background-color:  #fedecf;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col4 {
            background-color:  #fdcab5;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col5 {
            background-color:  #fb694a;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col6 {
            background-color:  #fedfd0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col7 {
            background-color:  #fee3d6;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col0 {
            background-color:  #fcb296;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col2 {
            background-color:  #940b13;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col3 {
            background-color:  #fb694a;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col4 {
            background-color:  #d01d1f;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col6 {
            background-color:  #840711;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col7 {
            background-color:  #6b010e;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col0 {
            background-color:  #fca588;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col2 {
            background-color:  #fed8c7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col6 {
            background-color:  #fed9c9;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col7 {
            background-color:  #fdd4c2;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col0 {
            background-color:  #fc9777;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col2 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col3 {
            background-color:  #fdc6b0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col4 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col5 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col6 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col7 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col0 {
            background-color:  #fc8a6a;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col2 {
            background-color:  #fff3ed;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col6 {
            background-color:  #fff3ed;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col7 {
            background-color:  #fff2ec;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col0 {
            background-color:  #fb7d5d;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col2 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col6 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col7 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col0 {
            background-color:  #fb7151;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col2 {
            background-color:  #fdcbb6;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col6 {
            background-color:  #fdccb8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col7 {
            background-color:  #fdc6b0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col0 {
            background-color:  #f96245;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col2 {
            background-color:  #fcb296;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col3 {
            background-color:  #fedbcc;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col4 {
            background-color:  #fdcab5;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col6 {
            background-color:  #fcaf93;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col7 {
            background-color:  #fca98c;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col0 {
            background-color:  #f5533b;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col2 {
            background-color:  #fdc5ae;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col3 {
            background-color:  #fdc6b0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col4 {
            background-color:  #feeae0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col6 {
            background-color:  #fcc1a8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col7 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col0 {
            background-color:  #f14432;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col2 {
            background-color:  #fcc1a8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col3 {
            background-color:  #bf151b;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col4 {
            background-color:  #feeae0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col6 {
            background-color:  #fcaa8d;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col7 {
            background-color:  #fc9e80;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col0 {
            background-color:  #eb372a;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col2 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col6 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col7 {
            background-color:  #ffede5;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col0 {
            background-color:  #de2b25;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col2 {
            background-color:  #fee1d4;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col4 {
            background-color:  #feeae0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col6 {
            background-color:  #fee2d5;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col7 {
            background-color:  #fee1d4;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col0 {
            background-color:  #d32020;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col2 {
            background-color:  #fee7dc;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col6 {
            background-color:  #fee7dc;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col7 {
            background-color:  #fee5d9;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col0 {
            background-color:  #c8171c;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col2 {
            background-color:  #fcaf93;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col3 {
            background-color:  #fee9df;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col4 {
            background-color:  #d01d1f;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col6 {
            background-color:  #fcaf93;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col7 {
            background-color:  #fcbda4;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col0 {
            background-color:  #bc141a;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col2 {
            background-color:  #fff2eb;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col6 {
            background-color:  #fff2eb;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col7 {
            background-color:  #fff1ea;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col0 {
            background-color:  #af1117;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col2 {
            background-color:  #feeae0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col6 {
            background-color:  #feeae0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col7 {
            background-color:  #fee9df;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col0 {
            background-color:  #a10e15;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col2 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col5 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col6 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col7 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col0 {
            background-color:  #8e0912;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col2 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col6 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col7 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col0 {
            background-color:  #7a0510;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col2 {
            background-color:  #fff0e8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col6 {
            background-color:  #fff0e8;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col7 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col0 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col2 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col3 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col4 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col5 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col6 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col7 {
            background-color:  #fff5f0;
            color:  #000000;
        }</style><table id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >S. No.</th>        <th class="col_heading level0 col1" >Name of State / UT</th>        <th class="col_heading level0 col2" >Total Confirmed cases (Indian National)</th>        <th class="col_heading level0 col3" >Total Confirmed cases ( Foreign National )</th>        <th class="col_heading level0 col4" >Cured</th>        <th class="col_heading level0 col5" >Death</th>        <th class="col_heading level0 col6" >Total Cases</th>        <th class="col_heading level0 col7" >Active Cases</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row0" class="row_heading level0 row0" >0</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col0" class="data row0 col0" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col1" class="data row0 col1" >Andhra Pradesh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col2" class="data row0 col2" >12</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col3" class="data row0 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col4" class="data row0 col4" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col5" class="data row0 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col6" class="data row0 col6" >12</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row0_col7" class="data row0 col7" >11</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row1" class="row_heading level0 row1" >1</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col0" class="data row1 col0" >2</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col1" class="data row1 col1" >Chhattisgarh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col2" class="data row1 col2" >6</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col3" class="data row1 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col4" class="data row1 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col5" class="data row1 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col6" class="data row1 col6" >6</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row1_col7" class="data row1 col7" >6</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row2" class="row_heading level0 row2" >2</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col0" class="data row2 col0" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col1" class="data row2 col1" >Delhi</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col2" class="data row2 col2" >38</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col3" class="data row2 col3" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col4" class="data row2 col4" >6</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col5" class="data row2 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col6" class="data row2 col6" >39</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row2_col7" class="data row2 col7" >32</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row3" class="row_heading level0 row3" >3</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col0" class="data row3 col0" >4</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col1" class="data row3 col1" >Gujarat</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col2" class="data row3 col2" >43</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col3" class="data row3 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col4" class="data row3 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col5" class="data row3 col5" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col6" class="data row3 col6" >43</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row3_col7" class="data row3 col7" >40</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row4" class="row_heading level0 row4" >4</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col0" class="data row4 col0" >5</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col1" class="data row4 col1" >Haryana</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col2" class="data row4 col2" >16</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col3" class="data row4 col3" >14</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col4" class="data row4 col4" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col5" class="data row4 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col6" class="data row4 col6" >30</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row4_col7" class="data row4 col7" >19</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row5" class="row_heading level0 row5" >5</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col0" class="data row5 col0" >6</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col1" class="data row5 col1" >Himachal Pradesh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col2" class="data row5 col2" >4</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col3" class="data row5 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col4" class="data row5 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col5" class="data row5 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col6" class="data row5 col6" >4</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row5_col7" class="data row5 col7" >3</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row6" class="row_heading level0 row6" >6</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col0" class="data row6 col0" >7</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col1" class="data row6 col1" >Karnataka</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col2" class="data row6 col2" >20</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col3" class="data row6 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col4" class="data row6 col4" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col5" class="data row6 col5" >2</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col6" class="data row6 col6" >20</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row6_col7" class="data row6 col7" >15</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row7" class="row_heading level0 row7" >7</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col0" class="data row7 col0" >8</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col1" class="data row7 col1" >Kerala</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col2" class="data row7 col2" >131</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col3" class="data row7 col3" >7</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col4" class="data row7 col4" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col5" class="data row7 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col6" class="data row7 col6" >138</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row7_col7" class="data row7 col7" >127</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row8" class="row_heading level0 row8" >8</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col0" class="data row8 col0" >9</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col1" class="data row8 col1" >Madhya Pradesh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col2" class="data row8 col2" >23</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col3" class="data row8 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col4" class="data row8 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col5" class="data row8 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col6" class="data row8 col6" >23</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row8_col7" class="data row8 col7" >22</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row9" class="row_heading level0 row9" >9</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col0" class="data row9 col0" >10</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col1" class="data row9 col1" >Maharashtra</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col2" class="data row9 col2" >144</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col3" class="data row9 col3" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col4" class="data row9 col4" >15</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col5" class="data row9 col5" >4</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col6" class="data row9 col6" >147</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row9_col7" class="data row9 col7" >128</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row10" class="row_heading level0 row10" >10</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col0" class="data row10 col0" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col1" class="data row10 col1" >Odisha</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col2" class="data row10 col2" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col3" class="data row10 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col4" class="data row10 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col5" class="data row10 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col6" class="data row10 col6" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row10_col7" class="data row10 col7" >3</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row11" class="row_heading level0 row11" >11</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col0" class="data row11 col0" >12</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col1" class="data row11 col1" >Puducherry</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col2" class="data row11 col2" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col3" class="data row11 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col4" class="data row11 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col5" class="data row11 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col6" class="data row11 col6" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row11_col7" class="data row11 col7" >1</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row12" class="row_heading level0 row12" >12</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col0" class="data row12 col0" >13</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col1" class="data row12 col1" >Punjab</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col2" class="data row12 col2" >29</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col3" class="data row12 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col4" class="data row12 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col5" class="data row12 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col6" class="data row12 col6" >29</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row12_col7" class="data row12 col7" >28</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row13" class="row_heading level0 row13" >13</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col0" class="data row13 col0" >14</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col1" class="data row13 col1" >Rajasthan</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col2" class="data row13 col2" >41</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col3" class="data row13 col3" >2</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col4" class="data row13 col4" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col5" class="data row13 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col6" class="data row13 col6" >43</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row13_col7" class="data row13 col7" >40</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row14" class="row_heading level0 row14" >14</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col0" class="data row14 col0" >15</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col1" class="data row14 col1" >Tamil Nadu</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col2" class="data row14 col2" >32</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col3" class="data row14 col3" >3</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col4" class="data row14 col4" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col5" class="data row14 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col6" class="data row14 col6" >35</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row14_col7" class="data row14 col7" >33</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row15" class="row_heading level0 row15" >15</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col0" class="data row15 col0" >16</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col1" class="data row15 col1" >Telengana</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col2" class="data row15 col2" >34</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col3" class="data row15 col3" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col4" class="data row15 col4" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col5" class="data row15 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col6" class="data row15 col6" >45</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row15_col7" class="data row15 col7" >44</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row16" class="row_heading level0 row16" >16</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col0" class="data row16 col0" >17</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col1" class="data row16 col1" >Chandigarh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col2" class="data row16 col2" >7</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col3" class="data row16 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col4" class="data row16 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col5" class="data row16 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col6" class="data row16 col6" >7</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row16_col7" class="data row16 col7" >7</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row17" class="row_heading level0 row17" >17</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col0" class="data row17 col0" >18</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col1" class="data row17 col1" >Jammu and Kashmir</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col2" class="data row17 col2" >18</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col3" class="data row17 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col4" class="data row17 col4" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col5" class="data row17 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col6" class="data row17 col6" >18</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row17_col7" class="data row17 col7" >16</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row18" class="row_heading level0 row18" >18</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col0" class="data row18 col0" >19</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col1" class="data row18 col1" >Ladakh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col2" class="data row18 col2" >13</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col3" class="data row18 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col4" class="data row18 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col5" class="data row18 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col6" class="data row18 col6" >13</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row18_col7" class="data row18 col7" >13</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row19" class="row_heading level0 row19" >19</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col0" class="data row19 col0" >20</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col1" class="data row19 col1" >Uttar Pradesh</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col2" class="data row19 col2" >42</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col3" class="data row19 col3" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col4" class="data row19 col4" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col5" class="data row19 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col6" class="data row19 col6" >43</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row19_col7" class="data row19 col7" >32</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row20" class="row_heading level0 row20" >20</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col0" class="data row20 col0" >21</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col1" class="data row20 col1" >Uttarakhand</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col2" class="data row20 col2" >4</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col3" class="data row20 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col4" class="data row20 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col5" class="data row20 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col6" class="data row20 col6" >4</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row20_col7" class="data row20 col7" >4</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row21" class="row_heading level0 row21" >21</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col0" class="data row21 col0" >22</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col1" class="data row21 col1" >West Bengal</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col2" class="data row21 col2" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col3" class="data row21 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col4" class="data row21 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col5" class="data row21 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col6" class="data row21 col6" >11</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row21_col7" class="data row21 col7" >10</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row22" class="row_heading level0 row22" >22</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col0" class="data row22 col0" >23</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col1" class="data row22 col1" >Bihar</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col2" class="data row22 col2" >7</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col3" class="data row22 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col4" class="data row22 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col5" class="data row22 col5" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col6" class="data row22 col6" >7</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row22_col7" class="data row22 col7" >6</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row23" class="row_heading level0 row23" >23</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col0" class="data row23 col0" >24</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col1" class="data row23 col1" >Mizoram</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col2" class="data row23 col2" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col3" class="data row23 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col4" class="data row23 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col5" class="data row23 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col6" class="data row23 col6" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row23_col7" class="data row23 col7" >1</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row24" class="row_heading level0 row24" >24</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col0" class="data row24 col0" >25</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col1" class="data row24 col1" >Goa</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col2" class="data row24 col2" >6</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col3" class="data row24 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col4" class="data row24 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col5" class="data row24 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col6" class="data row24 col6" >6</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row24_col7" class="data row24 col7" >6</td>
            </tr>
            <tr>
                        <th id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62level0_row25" class="row_heading level0 row25" >25</th>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col0" class="data row25 col0" >26</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col1" class="data row25 col1" >Manipur</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col2" class="data row25 col2" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col3" class="data row25 col3" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col4" class="data row25 col4" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col5" class="data row25 col5" >0</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col6" class="data row25 col6" >1</td>
                        <td id="T_7953e8fa_b224_11ea_97f1_5cea1d7fee62row25_col7" class="data row25 col7" >1</td>
            </tr>
    </tbody></table>




```python
Total_Active_Cases = data.groupby('Name of State / UT')['Active Cases'].sum().sort_values(ascending=False).to_frame()
```


```python
Total_Active_Cases
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
      <th>Active Cases</th>
    </tr>
    <tr>
      <th>Name of State / UT</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Maharashtra</th>
      <td>128</td>
    </tr>
    <tr>
      <th>Kerala</th>
      <td>127</td>
    </tr>
    <tr>
      <th>Telengana</th>
      <td>44</td>
    </tr>
    <tr>
      <th>Rajasthan</th>
      <td>40</td>
    </tr>
    <tr>
      <th>Gujarat</th>
      <td>40</td>
    </tr>
    <tr>
      <th>Tamil Nadu</th>
      <td>33</td>
    </tr>
    <tr>
      <th>Uttar Pradesh</th>
      <td>32</td>
    </tr>
    <tr>
      <th>Delhi</th>
      <td>32</td>
    </tr>
    <tr>
      <th>Punjab</th>
      <td>28</td>
    </tr>
    <tr>
      <th>Madhya Pradesh</th>
      <td>22</td>
    </tr>
    <tr>
      <th>Haryana</th>
      <td>19</td>
    </tr>
    <tr>
      <th>Jammu and Kashmir</th>
      <td>16</td>
    </tr>
    <tr>
      <th>Karnataka</th>
      <td>15</td>
    </tr>
    <tr>
      <th>Ladakh</th>
      <td>13</td>
    </tr>
    <tr>
      <th>Andhra Pradesh</th>
      <td>11</td>
    </tr>
    <tr>
      <th>West Bengal</th>
      <td>10</td>
    </tr>
    <tr>
      <th>Chandigarh</th>
      <td>7</td>
    </tr>
    <tr>
      <th>Goa</th>
      <td>6</td>
    </tr>
    <tr>
      <th>Chhattisgarh</th>
      <td>6</td>
    </tr>
    <tr>
      <th>Bihar</th>
      <td>6</td>
    </tr>
    <tr>
      <th>Uttarakhand</th>
      <td>4</td>
    </tr>
    <tr>
      <th>Himachal Pradesh</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Odisha</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Manipur</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Mizoram</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Puducherry</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
Total_Active_Cases.style.background_gradient(cmap='Reds')
```




<style  type="text/css" >
    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row0_col0 {
            background-color:  #67000d;
            color:  #f1f1f1;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row1_col0 {
            background-color:  #6b010e;
            color:  #f1f1f1;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row2_col0 {
            background-color:  #fc9e80;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row3_col0 {
            background-color:  #fca98c;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row4_col0 {
            background-color:  #fca98c;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row5_col0 {
            background-color:  #fcbba1;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row6_col0 {
            background-color:  #fcbda4;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row7_col0 {
            background-color:  #fcbda4;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row8_col0 {
            background-color:  #fdc6b0;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row9_col0 {
            background-color:  #fdd4c2;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row10_col0 {
            background-color:  #fedbcc;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row11_col0 {
            background-color:  #fee1d4;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row12_col0 {
            background-color:  #fee3d6;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row13_col0 {
            background-color:  #fee5d9;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row14_col0 {
            background-color:  #fee8dd;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row15_col0 {
            background-color:  #fee9df;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row16_col0 {
            background-color:  #ffede5;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row17_col0 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row18_col0 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row19_col0 {
            background-color:  #ffeee7;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row20_col0 {
            background-color:  #fff1ea;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row21_col0 {
            background-color:  #fff2ec;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row22_col0 {
            background-color:  #fff2ec;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row23_col0 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row24_col0 {
            background-color:  #fff5f0;
            color:  #000000;
        }    #T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row25_col0 {
            background-color:  #fff5f0;
            color:  #000000;
        }</style><table id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Active Cases</th>    </tr>    <tr>        <th class="index_name level0" >Name of State / UT</th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row0" class="row_heading level0 row0" >Maharashtra</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row0_col0" class="data row0 col0" >128</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row1" class="row_heading level0 row1" >Kerala</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row1_col0" class="data row1 col0" >127</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row2" class="row_heading level0 row2" >Telengana</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row2_col0" class="data row2 col0" >44</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row3" class="row_heading level0 row3" >Rajasthan</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row3_col0" class="data row3 col0" >40</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row4" class="row_heading level0 row4" >Gujarat</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row4_col0" class="data row4 col0" >40</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row5" class="row_heading level0 row5" >Tamil Nadu</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row5_col0" class="data row5 col0" >33</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row6" class="row_heading level0 row6" >Uttar Pradesh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row6_col0" class="data row6 col0" >32</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row7" class="row_heading level0 row7" >Delhi</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row7_col0" class="data row7 col0" >32</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row8" class="row_heading level0 row8" >Punjab</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row8_col0" class="data row8 col0" >28</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row9" class="row_heading level0 row9" >Madhya Pradesh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row9_col0" class="data row9 col0" >22</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row10" class="row_heading level0 row10" >Haryana</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row10_col0" class="data row10 col0" >19</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row11" class="row_heading level0 row11" >Jammu and Kashmir</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row11_col0" class="data row11 col0" >16</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row12" class="row_heading level0 row12" >Karnataka</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row12_col0" class="data row12 col0" >15</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row13" class="row_heading level0 row13" >Ladakh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row13_col0" class="data row13 col0" >13</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row14" class="row_heading level0 row14" >Andhra Pradesh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row14_col0" class="data row14 col0" >11</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row15" class="row_heading level0 row15" >West Bengal</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row15_col0" class="data row15 col0" >10</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row16" class="row_heading level0 row16" >Chandigarh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row16_col0" class="data row16 col0" >7</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row17" class="row_heading level0 row17" >Goa</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row17_col0" class="data row17 col0" >6</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row18" class="row_heading level0 row18" >Chhattisgarh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row18_col0" class="data row18 col0" >6</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row19" class="row_heading level0 row19" >Bihar</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row19_col0" class="data row19 col0" >6</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row20" class="row_heading level0 row20" >Uttarakhand</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row20_col0" class="data row20 col0" >4</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row21" class="row_heading level0 row21" >Himachal Pradesh</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row21_col0" class="data row21 col0" >3</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row22" class="row_heading level0 row22" >Odisha</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row22_col0" class="data row22 col0" >3</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row23" class="row_heading level0 row23" >Manipur</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row23_col0" class="data row23 col0" >1</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row24" class="row_heading level0 row24" >Mizoram</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row24_col0" class="data row24 col0" >1</td>
            </tr>
            <tr>
                        <th id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62level0_row25" class="row_heading level0 row25" >Puducherry</th>
                        <td id="T_7b5363a8_b224_11ea_ab09_5cea1d7fee62row25_col0" class="data row25 col0" >1</td>
            </tr>
    </tbody></table>




```python

```


```python

```


```python

```
