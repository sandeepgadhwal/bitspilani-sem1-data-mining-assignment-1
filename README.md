# bitspilani-sem1-data-mining-assignment-1
bitspilani-sem1-data-mining-assignment-1


<div tabindex="-1" id="notebook" class="border-box-sizing">

<div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [1]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Necessary imports</span>
<span class="kn">import</span> <span class="nn">sklearn</span> <span class="k">as</span> <span class="nn">sk</span>
<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">svm</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">Normalizer</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">train_test_split</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">RandomForestClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">accuracy_score</span><span class="p">,</span><span class="n">confusion_matrix</span><span class="p">,</span><span class="n">classification_report</span>

<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">pickle</span>

<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Table of Contents[¶](#Table-of-Contents)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

*   [Problem Statement](#Problem-Statement)
*   [Exploratory Data Analysis](#Exploratory-Data-Analysis)
    *   [Read CSV](#Read-CSV)
*   [Data Pre-Processing](#Data-Pre-Processing)
    *   [Clean Data](#Clean-Data)
    *   [Reducing Dimentionality of Data](#Reducing-Dimentionality-of-Data)
    *   [Reducing Outliers from Data](#Removing-outliers-from-Data)
    *   [Get Training and Testing Set](#Get-Training-and-Testing-Set)
*   [Data Visalization](#Data-Visalization)
*   [Train a Model](#Train-a-Model)
    *   [Create a Model](#Create-a-Model)
    *   [Fit the Model](#Fit-the-Model)
    *   [Test the Model](#Test-the-Model)
*   [Save the Model](#Save-the-Model)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

# Problem Statement[¶](#Problem-Statement)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

We have collected some health vitals that can be used to predict if the patient will acquire a coronary heart disease in the next 10 years, we can call these data points as X. For the collected samples we have the ground truth stating that whether the corresponding case acquired that disease in the next 10 years or not, we can call this data pointer Y. We now want to train a model that can take in those data points (X) and predict whether that case is vulnerable to acquire a coronary Heart disease (ŷ). We can apply this model on any other patient and classify him as vulnerable to that disease or not, doing so will help us take necessary steps in advance.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Exploratory Data Analysis[¶](#Exploratory-Data-Analysis)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

In this step we would read the dataset and try to understand our data, we would usually start with checking the dataypes and data ranges.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Read CSV[¶](#Read-CSV)

We would be using pandas library to read the CSV and clean the data to be used in the next step.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [2]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'Problem2_Data.csv'</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [3]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre><class 'pandas.core.frame.DataFrame'>
RangeIndex: 34281 entries, 0 to 34280
Data columns (total 25 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   ID      34281 non-null  int64  
 1   IV      34281 non-null  int64  
 2   A1      34281 non-null  int64  
 3   A2      32538 non-null  float64
 4   A3      34281 non-null  int64  
 5   A4      34281 non-null  int64  
 6   A5      34281 non-null  int64  
 7   A6      34281 non-null  int64  
 8   A7      34281 non-null  int64  
 9   A8      34281 non-null  int64  
 10  A9      34281 non-null  int64  
 11  A10     34281 non-null  int64  
 12  A11     34281 non-null  int64  
 13  A12     34281 non-null  int64  
 14  A13     34281 non-null  int64  
 15  A14     34281 non-null  int64  
 16  A15     34281 non-null  float64
 17  A16     34281 non-null  float64
 18  A17     34281 non-null  int64  
 19  A18     34281 non-null  int64  
 20  A19     34281 non-null  int64  
 21  A20     34281 non-null  int64  
 22  A21     34281 non-null  float64
 23  A22     34281 non-null  int64  
 24  Target  34281 non-null  int64  
dtypes: float64(4), int64(21)
memory usage: 6.5 MB
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [4]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[4]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>ID</th>

<th>IV</th>

<th>A1</th>

<th>A2</th>

<th>A3</th>

<th>A4</th>

<th>A5</th>

<th>A6</th>

<th>A7</th>

<th>A8</th>

<th>...</th>

<th>A14</th>

<th>A15</th>

<th>A16</th>

<th>A17</th>

<th>A18</th>

<th>A19</th>

<th>A20</th>

<th>A21</th>

<th>A22</th>

<th>Target</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>1443894</td>

<td>2049</td>

<td>44</td>

<td>8.0</td>

<td>11</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>38</td>

<td>...</td>

<td>0</td>

<td>0.52</td>

<td>0.69</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>1</td>

<td>17.078971</td>

<td>0</td>

<td>0</td>

</tr>

<tr>

<th>1</th>

<td>1810849</td>

<td>48</td>

<td>0</td>

<td>8.0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>1</td>

<td>...</td>

<td>0</td>

<td>0.59</td>

<td>0.78</td>

<td>1</td>

<td>0</td>

<td>0</td>

<td>1</td>

<td>17.022384</td>

<td>0</td>

<td>0</td>

</tr>

<tr>

<th>2</th>

<td>2264999</td>

<td>318</td>

<td>2</td>

<td>9.0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>...</td>

<td>0</td>

<td>0.94</td>

<td>0.79</td>

<td>1</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>17.024773</td>

<td>0</td>

<td>0</td>

</tr>

<tr>

<th>3</th>

<td>1931676</td>

<td>62</td>

<td>4</td>

<td>2.0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>15</td>

<td>30</td>

<td>7</td>

<td>...</td>

<td>0</td>

<td>0.51</td>

<td>0.47</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>1</td>

<td>17.074995</td>

<td>0</td>

<td>0</td>

</tr>

<tr>

<th>4</th>

<td>2070885</td>

<td>2</td>

<td>0</td>

<td>8.0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>1</td>

<td>0</td>

<td>...</td>

<td>0</td>

<td>0.82</td>

<td>0.81</td>

<td>0</td>

<td>0</td>

<td>0</td>

<td>1</td>

<td>17.072697</td>

<td>0</td>

<td>0</td>

</tr>

</tbody>

</table>

5 rows × 25 columns

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Column 0 is ID column and can be excluded from training data,

Columns 0 to -2 or IV to A22 are vitals which will be used to train the model for the corresponding Y values in the Column -1 or Traget is column which contains the classification ground truth.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [5]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">col</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="p">):</span>
    <span class="n">opt</span> <span class="o">=</span> <span class="sa">f</span><span class="s2">"""</span>
 <span class="s2"></span> <span class="si">{1}</span><span class="s2">.</span> <span class="si">{col}</span> <span class="s2">column has a min: {df[col].min():0.2f}, mean: {df[col].mean():0.2f}, max: {df[col].max():0.2f}, std: {df[col].std():0.2f}</span> 
 <span class="s2">"""</span><span class="o">.</span><span class="n">strip</span><span class="p">()</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">opt</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>1\. ID column has a min: 1058628.00, mean: 1979837.87, max: 3274754.00, std: 638485.49
1\. IV column has a min: -2999.00, mean: 236.25, max: 366924.00, std: 3326.57
1\. A1 column has a min: 0.00, mean: 36.13, max: 50547.00, std: 427.71
1\. A2 column has a min: 0.00, mean: 7.36, max: 52.00, std: 6.17
1\. A3 column has a min: 0.00, mean: 22.54, max: 31750.00, std: 359.49
1\. A4 column has a min: 0.00, mean: 1.70, max: 2999.00, std: 36.20
1\. A5 column has a min: 0.00, mean: 151.96, max: 260660.00, std: 2274.09
1\. A6 column has a min: 0.00, mean: 274.42, max: 438020.00, std: 4065.44
1\. A7 column has a min: 0.00, mean: 387.93, max: 533540.00, std: 5443.80
1\. A8 column has a min: 0.00, mean: 36.48, max: 21071.00, std: 375.93
1\. A9 column has a min: 0.00, mean: 132.95, max: 742110.00, std: 4151.80
1\. A10 column has a min: 0.00, mean: 236.65, max: 742750.00, std: 4528.96
1\. A11 column has a min: 27.00, mean: 27.00, max: 27.00, std: 0.00
1\. A12 column has a min: 0.00, mean: 341.15, max: 743215.00, std: 5005.76
1\. A13 column has a min: 0.00, mean: 0.00, max: 1.00, std: 0.04
1\. A14 column has a min: 0.00, mean: 1.74, max: 1488.00, std: 26.08
1\. A15 column has a min: -99.00, mean: -5.74, max: 1.00, std: 24.62
1\. A16 column has a min: -99.00, mean: -5.37, max: 1.00, std: 23.94
1\. A17 column has a min: 0.00, mean: 0.21, max: 1.00, std: 0.41
1\. A18 column has a min: 0.00, mean: 0.00, max: 1.00, std: 0.02
1\. A19 column has a min: 0.00, mean: 0.13, max: 1.00, std: 0.34
1\. A20 column has a min: 0.00, mean: 0.96, max: 1.00, std: 0.19
1\. A21 column has a min: 17.00, mean: 17.05, max: 17.10, std: 0.03
1\. A22 column has a min: 0.00, mean: 0.00, max: 1.00, std: 0.01
1\. Target column has a min: 0.00, mean: 0.33, max: 1.00, std: 0.47
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [4]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[4]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>ID</th>

<th>IV</th>

<th>A1</th>

<th>A2</th>

<th>A3</th>

<th>A4</th>

<th>A5</th>

<th>A6</th>

<th>A7</th>

<th>A8</th>

<th>...</th>

<th>A14</th>

<th>A15</th>

<th>A16</th>

<th>A17</th>

<th>A18</th>

<th>A19</th>

<th>A20</th>

<th>A21</th>

<th>A22</th>

<th>Target</th>

</tr>

</thead>

<tbody>

<tr>

<th>count</th>

<td>3.428100e+04</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>32538.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>...</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

<td>34281.000000</td>

</tr>

<tr>

<th>mean</th>

<td>1.979838e+06</td>

<td>236.252005</td>

<td>36.126367</td>

<td>7.355185</td>

<td>22.543071</td>

<td>1.695371</td>

<td>151.959044</td>

<td>274.418453</td>

<td>387.933637</td>

<td>36.482746</td>

<td>...</td>

<td>1.744757</td>

<td>-5.742893</td>

<td>-5.368822</td>

<td>0.208658</td>

<td>0.000321</td>

<td>0.131939</td>

<td>0.962370</td>

<td>17.049826</td>

<td>0.000204</td>

<td>0.329424</td>

</tr>

<tr>

<th>std</th>

<td>6.384855e+05</td>

<td>3326.574620</td>

<td>427.707021</td>

<td>6.165307</td>

<td>359.486291</td>

<td>36.195759</td>

<td>2274.087109</td>

<td>4065.441226</td>

<td>5443.804648</td>

<td>375.931751</td>

<td>...</td>

<td>26.077507</td>

<td>24.618128</td>

<td>23.938095</td>

<td>0.406355</td>

<td>0.017910</td>

<td>0.338429</td>

<td>0.190303</td>

<td>0.028818</td>

<td>0.014288</td>

<td>0.470011</td>

</tr>

<tr>

<th>min</th>

<td>1.058628e+06</td>

<td>-2999.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>...</td>

<td>0.000000</td>

<td>-99.000000</td>

<td>-99.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>17.000005</td>

<td>0.000000</td>

<td>0.000000</td>

</tr>

<tr>

<th>25%</th>

<td>1.464342e+06</td>

<td>2.000000</td>

<td>0.000000</td>

<td>2.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>...</td>

<td>0.000000</td>

<td>0.590000</td>

<td>0.610000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>1.000000</td>

<td>17.024869</td>

<td>0.000000</td>

<td>0.000000</td>

</tr>

<tr>

<th>50%</th>

<td>1.841719e+06</td>

<td>8.000000</td>

<td>0.000000</td>

<td>8.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>2.000000</td>

<td>4.000000</td>

<td>1.000000</td>

<td>...</td>

<td>0.000000</td>

<td>0.810000</td>

<td>0.790000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>1.000000</td>

<td>17.049813</td>

<td>0.000000</td>

<td>0.000000</td>

</tr>

<tr>

<th>75%</th>

<td>2.254242e+06</td>

<td>40.000000</td>

<td>4.000000</td>

<td>8.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>18.000000</td>

<td>33.000000</td>

<td>48.000000</td>

<td>6.000000</td>

<td>...</td>

<td>0.000000</td>

<td>0.960000</td>

<td>0.940000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>1.000000</td>

<td>17.074796</td>

<td>0.000000</td>

<td>1.000000</td>

</tr>

<tr>

<th>max</th>

<td>3.274754e+06</td>

<td>366924.000000</td>

<td>50547.000000</td>

<td>52.000000</td>

<td>31750.000000</td>

<td>2999.000000</td>

<td>260660.000000</td>

<td>438020.000000</td>

<td>533540.000000</td>

<td>21071.000000</td>

<td>...</td>

<td>1488.000000</td>

<td>1.000000</td>

<td>1.000000</td>

<td>1.000000</td>

<td>1.000000</td>

<td>1.000000</td>

<td>1.000000</td>

<td>17.099995</td>

<td>1.000000</td>

<td>1.000000</td>

</tr>

</tbody>

</table>

8 rows × 25 columns

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Looking at the above data we got some interesting insights,

*   some columns like IV has negative values,
*   column A15 and A16 has -99 values which can be invalid values, or no data values.
*   Target column has 33% positive samples and 77% negative samples.
*   Column A13, A18 have very less STD there can be very less information in those columns

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

* * *

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

# Data Pre-Processing[¶](#Data-Pre-Processing)

In this step we would like to read the data and understand format of data and prepare it in a format that can be used to train the model. Our model is as good as our data and I am a believer of 70:30 ratio 70% of my model is data and 30% is the architecture or algorithm. Anyway, better algorithm is always good but my point is we should be very careful while preparing our dataset to avoid pitfalls.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Clean Data[¶](#Clean-Data)

At this step we would be cleaning our data by filling the invalid values with means in case of float or drop the row in case of int datatype.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### Check if there are NAs[¶](#Check-if-there-are-NAs)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [5]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span> <span class="o">|</span> <span class="n">df</span><span class="o">.</span><span class="n">isin</span><span class="p">([</span><span class="o">-</span><span class="mi">99</span><span class="p">,</span> <span class="o">-</span><span class="mi">999</span><span class="p">]))</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[5]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>6079</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

As we can see our dataset is having invalid values lets clean them up.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### Handle Invalid values in Float datatype columns[¶](#Handle-Invalid-values-in-Float-datatype-columns)

for columns with datatype float we would fill averages in place of NAs, -999, -99, ' '

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [6]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># X in column 1 to -2 and Y in column -1 and ID col 0 is not needed in model training</span>

<span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="mi">1</span><span class="p">:</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">columns</span><span class="p">:</span> 
    <span class="k">if</span> <span class="n">df</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">dtype</span> <span class="ow">in</span> <span class="p">[</span><span class="n">np</span><span class="o">.</span><span class="n">float64</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">float32</span><span class="p">]:</span>
        <span class="n">fill_idx</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span> <span class="o">|</span> <span class="n">df</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">isin</span><span class="p">([</span><span class="o">-</span><span class="mi">99</span><span class="p">,</span> <span class="o">-</span><span class="mi">999</span><span class="p">,</span> <span class="s1">' '</span><span class="p">])</span>
        <span class="n">fill_val</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="o">~</span><span class="n">fill_idx</span><span class="p">,</span> <span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
        <span class="n">df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">fill_idx</span><span class="p">,</span> <span class="n">col</span><span class="p">]</span> <span class="o">=</span> <span class="n">fill_val</span>
        <span class="n">size</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">fill_idx</span><span class="p">,</span> <span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">size</span>
        <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"-- filled</span> <span class="si">{size}</span> <span class="s2">rows in</span> <span class="si">{col}</span> <span class="s2">column with mean value</span> <span class="si">{fill_val}</span><span class="s2">"</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>-- filled 1743 rows in A2 column with mean value 7.355184707111685
-- filled 2233 rows in A15 column with mean value 0.7549572516225662
-- filled 2103 rows in A16 column with mean value 0.7504633600596681
-- filled 0 rows in A21 column with mean value 17.049825959760508
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### Handle Invalid Values in Int datatype columns[¶](#Handle-Invalid-Values-in-Int-datatype-columns)

for columns with datatype int we would simple drop the row, also we noted that none of the int columns are having invalid values we are doing this just to be safe

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [7]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">flt_idx</span> <span class="o">=</span> <span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span> <span class="mi">1</span><span class="p">:]</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span> <span class="o">|</span> <span class="n">df</span><span class="o">.</span><span class="n">isin</span><span class="p">([</span><span class="o">-</span><span class="mi">999</span><span class="p">,</span> <span class="o">-</span><span class="mi">99</span><span class="p">,</span> <span class="s1">''</span><span class="p">])</span> <span class="p">)</span><span class="o">.</span><span class="n">any</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="o">~</span><span class="n">flt_idx</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [8]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Drop index to allow dataframe to adjust the dropped the dropped rows to index</span>
<span class="n">df</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### Re Check if there are NAs[¶](#Re-Check-if-there-are-NAs)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [9]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">isna</span><span class="p">()</span> <span class="o">|</span> <span class="n">df</span><span class="o">.</span><span class="n">isin</span><span class="p">([</span><span class="o">-</span><span class="mi">99</span><span class="p">,</span> <span class="o">-</span><span class="mi">999</span><span class="p">,</span> <span class="s1">''</span><span class="p">]))</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[9]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>0</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

There are no invalid values left

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Reducing Dimentionality of Data[¶](#Reducing-Dimentionality-of-Data)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

we will check for the most important parameters and try to remove duplciates. This helps reducing redundant parameters.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [10]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="kn">from</span> <span class="nn">sklearn.feature_selection</span> <span class="kn">import</span> <span class="n">SelectKBest</span>
<span class="kn">from</span> <span class="nn">sklearn.feature_selection</span> <span class="kn">import</span> <span class="n">chi2</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="o">~</span><span class="p">(</span><span class="n">df</span> <span class="o"><</span> <span class="mi">0</span><span class="p">)]</span>
<span class="n">df</span><span class="o">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">array</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">values</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">array</span><span class="p">[:,</span><span class="mi">1</span><span class="p">:</span><span class="mi">24</span><span class="p">]</span>
<span class="n">Y</span> <span class="o">=</span> <span class="n">array</span><span class="p">[:,</span><span class="mi">24</span><span class="p">]</span>
<span class="c1"># feature extraction</span>
<span class="n">test</span> <span class="o">=</span> <span class="n">SelectKBest</span><span class="p">(</span><span class="n">score_func</span><span class="o">=</span><span class="n">chi2</span><span class="p">,</span> <span class="n">k</span><span class="o">=</span><span class="mi">4</span><span class="p">)</span>
<span class="n">fit</span> <span class="o">=</span> <span class="n">test</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">Y</span><span class="p">)</span>
<span class="c1"># summarize scores</span>
<span class="n">np</span><span class="o">.</span><span class="n">set_printoptions</span><span class="p">(</span><span class="n">precision</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">fit</span><span class="o">.</span><span class="n">scores_</span><span class="p">)</span>
<span class="n">features</span> <span class="o">=</span> <span class="n">fit</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">X</span><span class="p">)</span>
<span class="c1"># summarize selected features</span>
<span class="nb">print</span><span class="p">(</span><span class="n">features</span><span class="p">[</span><span class="mi">0</span><span class="p">:</span><span class="mi">5</span><span class="p">,:])</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>[2.915e+06 9.278e+04 2.634e+03 2.365e+05 6.657e+03 1.071e+04 1.453e+05
 3.193e+05 4.976e+04 5.045e+05 9.140e+05 0.000e+00 1.209e+06 5.942e+01
 2.293e+04 4.438e+01 4.203e+01 8.934e+01 8.819e+00 6.812e+01 2.146e-02
 4.959e-05 3.179e+00]
[[2.049e+03 1.230e+02 2.300e+02 3.300e+02]
 [4.800e+01 1.000e+00 1.000e+00 1.000e+00]
 [3.180e+02 1.000e+00 2.000e+00 2.000e+00]
 [6.200e+01 2.400e+01 4.200e+01 7.100e+01]
 [2.000e+00 0.000e+00 2.000e+00 2.000e+00]]
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [11]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df_flt</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">'IV'</span><span class="p">,</span> <span class="s1">'A9'</span><span class="p">,</span> <span class="s1">'A10'</span><span class="p">,</span> <span class="s1">'A12'</span><span class="p">,</span> <span class="s1">'Target'</span><span class="p">]]</span>
<span class="n">df_flt</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>IV</th>

<th>A9</th>

<th>A10</th>

<th>A12</th>

<th>Target</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td>2049.0</td>

<td>123</td>

<td>230</td>

<td>330</td>

<td>0</td>

</tr>

<tr>

<th>1</th>

<td>48.0</td>

<td>1</td>

<td>1</td>

<td>1</td>

<td>0</td>

</tr>

<tr>

<th>2</th>

<td>318.0</td>

<td>1</td>

<td>2</td>

<td>2</td>

<td>0</td>

</tr>

<tr>

<th>3</th>

<td>62.0</td>

<td>24</td>

<td>42</td>

<td>71</td>

<td>0</td>

</tr>

<tr>

<th>4</th>

<td>2.0</td>

<td>0</td>

<td>2</td>

<td>2</td>

<td>0</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [12]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df_flt</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre><class 'pandas.core.frame.DataFrame'>
Int64Index: 33310 entries, 0 to 34280
Data columns (total 5 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   IV      33310 non-null  float64
 1   A9      33310 non-null  int64  
 2   A10     33310 non-null  int64  
 3   A12     33310 non-null  int64  
 4   Target  33310 non-null  int64  
dtypes: float64(1), int64(4)
memory usage: 1.5 MB
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [13]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">df_flt</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[13]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>IV</th>

<th>A9</th>

<th>A10</th>

<th>A12</th>

<th>Target</th>

</tr>

</thead>

<tbody>

<tr>

<th>count</th>

<td>33310.000000</td>

<td>33310.000000</td>

<td>33310.000000</td>

<td>33310.000000</td>

<td>33310.000000</td>

</tr>

<tr>

<th>mean</th>

<td>244.590513</td>

<td>128.824437</td>

<td>229.920174</td>

<td>331.861153</td>

<td>0.312309</td>

</tr>

<tr>

<th>std</th>

<td>3374.175071</td>

<td>4208.590754</td>

<td>4585.344015</td>

<td>5063.785523</td>

<td>0.463442</td>

</tr>

<tr>

<th>min</th>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

</tr>

<tr>

<th>25%</th>

<td>2.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

<td>0.000000</td>

</tr>

<tr>

<th>50%</th>

<td>8.000000</td>

<td>3.000000</td>

<td>5.000000</td>

<td>7.000000</td>

<td>0.000000</td>

</tr>

<tr>

<th>75%</th>

<td>43.000000</td>

<td>18.000000</td>

<td>34.000000</td>

<td>49.750000</td>

<td>1.000000</td>

</tr>

<tr>

<th>max</th>

<td>366924.000000</td>

<td>742110.000000</td>

<td>742750.000000</td>

<td>743215.000000</td>

<td>1.000000</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [14]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span><span class="mi">10</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">boxplot</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">df_flt</span><span class="p">,</span><span class="n">orient</span><span class="o">=</span><span class="s2">"h"</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s2">"Set2"</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[14]:</div>

<div class="output_text output_subarea output_execute_result">

<pre><matplotlib.axes._subplots.AxesSubplot at 0x1bc2a427108></pre>

</div>

</div>

<div class="output_area">

<div class="output_png output_subarea ">![](data:image/png;base64,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GQBAMYEMAKCYQAYAUEwgAwAoJpABABQbWa2JW2s7khxI8n29988P2h5J8ookH++9/+Scvt+d5OEk1yT5oyQ/3Xv/zmrVtlx33XXXC57j2muvzYtf/OI8++yz+epXv5rTp0/njjvuyPve975s3LgxJ06cyGWXXZa3ve1teclLXpL7778/SfKa17wme/fuzVve8paMjo7mwQcfzJ49e2bHzN2eca72hSyn73LGTE5O5r777su9996bm2666ayxO3fuzP79+5d1XABYaedzHlwNq3mF7M4kH09yx5y230jy0wv0/fUk9/fevzfJiSRvWMW6Snzzm9/M5ORkvvSlL+X06dNJkocffji995w4cSJJcvr06ezduzfj4+M5evRojh49mre//e3pvee3fuu3Mj4+niNHjuTAgQNJctb2jHO1L2Q5fZczZt++fTl16lT27t274Nh9+/Yt+7gAsNLO5zy4GlYlkLXWXpRkLNPBajaQ9d4/nOSpM/q2JK9K8nuDpvcked1q1LUcK3FV7HwcO3YsH/3oR2e3p6amkiRPP/10PvKRj6T3nomJiTz++OM5ePDg7PbJkyeTTCf9hdoXspy+yxkzOTmZY8eOzb6exx9//Kyxx44dW9ZxAWClnc95cLWs1hWy1yV5pPf+hSRPttZuXaTvtUlO9t6nBttPJBldpbouCs8+++yC7c8999zsz71796b3Prs996rZQu0LWU7f5YzZt2/fvO2Zq2Rzx859TdV/KwFgbTqf8+BqWa1Admem3xOWwc87F+nbFmjrC7RNd27tja21w621w8ePH38BJV68pqamcuzYsdmrZ1NTUzl06FCS5NChQwu2L2Q5fZczZubq2Jnbc8fOfS1LOS4ArLTzOQ+ulhUPZK21azN9C/JdrbXJJL+Y5KcGtyYX8o0kG1trMx8wuCHJl881f+/9nb33rb33rZs3b17Byi8eIyMjGR0dzcjIyOz22NhYkmRsbGzB9oUsp+9yxoyOji64PXfs3NeylOMCwEo7n/PgalmNK2SvT7K/935T731L7/3GJF9M8sMLde7T1wo/OhiXJHcn+derUNdFY/369Qu2r1u3bvbn7t27M5Nx161bl9tvvz1JsmPHjgXbF7KcvssZs2vXrnnbu3fvPmvs3Ne0lOMCwEo7n/PgalmNQHZnkvEz2j6Q5K7W2seSvD/Jj7bWnmitvXqw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
)</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Reducing Outliers from Data[¶](#Reducing-Outliers-from-Data)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [15]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">def</span> <span class="nf">remove_outlier_by_mean_value</span><span class="p">(</span><span class="n">df</span><span class="p">,</span> <span class="n">col_in</span><span class="p">):</span>
    <span class="n">q1</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">col_in</span><span class="p">]</span><span class="o">.</span><span class="n">quantile</span><span class="p">(</span><span class="mf">0.25</span><span class="p">)</span>
    <span class="n">q3</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">col_in</span><span class="p">]</span><span class="o">.</span><span class="n">quantile</span><span class="p">(</span><span class="mf">0.75</span><span class="p">)</span>
    <span class="n">value</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">col_in</span><span class="p">]</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
    <span class="n">iqr</span> <span class="o">=</span> <span class="n">q3</span><span class="o">-</span><span class="n">q1</span>
    <span class="n">x</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">col_in</span><span class="p">])</span>
    <span class="n">y</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="n">fence_low</span>  <span class="o">=</span> <span class="n">q1</span><span class="o">-</span><span class="mf">1.5</span><span class="o">*</span><span class="n">iqr</span>
    <span class="n">fence_high</span> <span class="o">=</span> <span class="n">q3</span><span class="o">+</span><span class="mf">1.5</span><span class="o">*</span><span class="n">iqr</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">x</span><span class="p">:</span>
        <span class="k">if</span> <span class="p">(</span><span class="n">i</span> <span class="o"><</span> <span class="n">fence_low</span><span class="p">)</span> <span class="ow">or</span> <span class="p">(</span><span class="n">i</span> <span class="o">></span> <span class="n">fence_high</span><span class="p">):</span>
            <span class="n">i</span> <span class="o">=</span> <span class="n">value</span>
            <span class="n">y</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">i</span><span class="p">)</span>
        <span class="k">else</span><span class="p">:</span>
            <span class="n">y</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">i</span><span class="p">)</span>
    <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">col_in</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
    <span class="n">df</span><span class="p">[</span><span class="n">col_in</span><span class="p">]</span> <span class="o">=</span> <span class="n">y</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [16]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">df_flt</span><span class="o">.</span><span class="n">columns</span><span class="p">:</span>
    <span class="n">remove_outlier_by_mean_value</span><span class="p">(</span><span class="n">df_flt</span><span class="p">,</span> <span class="n">i</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stderr output_text">

<pre>C:\Users\san10428\.conda\envs\ml\lib\site-packages\pandas\core\frame.py:3997: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  errors=errors,
C:\Users\san10428\.conda\envs\ml\lib\site-packages\ipykernel_launcher.py:17: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [17]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">10</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">boxplot</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">df_flt</span><span class="p">,</span> <span class="n">orient</span><span class="o">=</span><span class="s2">"h"</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s2">"Set2"</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[17]:</div>

<div class="output_text output_subarea output_execute_result">

<pre><matplotlib.axes._subplots.AxesSubplot at 0x1bc2a3bb408></pre>

</div>

</div>

<div class="output_area">

<div class="output_png output_subarea ">![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAmQAAAI/CAYAAADZWMWIAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4xLjMsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+AADFEAAAcAUlEQVR4nO3df7Dld13f8dc7uckSCCSSxFwFepOxjIIUY2aLzOAwiI6gthJm0mmyrRdbbJyOttp2aqXtInZ11NJKB6faxpGR23ETEIhSy0QUqcJUwQUhCkIIxmMhXLNJyK9N2GR3P/3jnqTLcu/d3WTvfZ977+Mxk7n3fM/3nvPez3wXnvP9fu/ZGmMEAIA+Z3UPAACw0wkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZnPdAzwZF1988bjsssu6xwAAOKmPfOQjd40xLlntuS0dZJdddlkOHDjQPQYAwElV1WSt51yyBABoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACg2Zb+YNjNtLS0lMlkzc9zS5IsLy8nSebn5zdjpE21sLCQxcXF7jEAYFsSZKdoMpnkU7d9Juc88+lr7vPogw8kSQ7ds1lTbY5H73mgewQA2NYE2Wk455lPz0Xf+S1rPn/3ez+UJOvusxU99ucCADaGe8gAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSBbx9LSUpaWlrrHYAdy7AHsLHPdA8yyyWTSPQI7lGMPYGdxhgwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKDZXOebV9WDY4zzq+r2JK8cY3z6uOf+S5I7xhj/sW9CALaTPXv2PP79/v37GyeBLzcrZ8huTHLNYw+q6qwkVyd5W9tEAACbZFaC7IYcF2RJXprkL8cYk6Z5ANhmjj87ttpj6NR6yfIxY4xbqupYVX3TGOPjWYmzG7rnWl5ezuHDh7Nv375MJpMcydHukVoceeChTB6YZN++fd2j7BiTySS7du3qHgOATTIrZ8iS6VmyqppL8qokv77aTlV1XVUdqKoDBw8e3NQBAQA2wkycIZu6Icl7k/x+klvGGHeuttMY4/ok1yfJ7t27x0YOND8/nyTZu3dv9u3bl8/es7yRbzez5p7+1Cw8cz579+7tHmXHcDYSYGeZmTNkY4zPJrk7yc9mBi5XAgBslpkJsqkbknxDkpu6BwFgeznxYy587AWzpDXIxhjnn/D4TWOMp4wx7uuaCQBgs83SPWQAsKGcFWNWzdolSwCAHUeQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM3mugeYZQsLC90jsEM59gB2FkG2jsXFxe4R2KEcewA7i0uWAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0Gyue4Ct5NF7Hsjd7/3Qus8nWXefrejRex5InjnfPQYAbFuC7BQtLCycdJ/lR1a+zm+3eHnm/Cn9+QGAJ0aQnaLFxcXuEQCAbco9ZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBsrnuAWba0tJTJZPJl25aXl5Mk8/PzG/KeCwsLWVxc3JDXBgBmkyBbx2Qyye23firPOv+cx7c9/OCjSZJHjh064+/3+elrAwA7iyA7iWedf07+2Qu/+vHHv3DLnUnyZdvOlMdeGwDYWdxDBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM3mugeYZcvLyzn28JHuMWbK0tJSkmRxcbF5EgDYPgTZOg4fPpxjR0f3GDNlMpl0jwAA245LlgAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0m+t406p6dZJ3JXneGONT020/l+R7prvsG2O8rWM2YG179ux5/Pv9+/c3TgKwvXSdIbs2yQeTXJMkVfU9Sa5MckWSb0nyr6vqGU2zAQBsqk0Psqo6P8lLkrw20yBL8vwkvz/GODLGOJTk40leudmzAWs7/uzYao8BeOI6LlleleTmMcatVXVPVV2ZlQD7iar6+SRPTfJtST7ZMFurux4+kkcnk+zbt697lDVNJpPs2rWrewwA2FY6Lllem+TG6fc3Jrl2jPHeJO9J8n+S3JDkD5McWe2Hq+q6qjpQVQcOHjy4GfMCAGyoTT1DVlUXJXl5khdU1UhydpJRVT82xvjpJD893W9/ks+s9hpjjOuTXJ8ku3fvHpsy+Ca5+Ly5nPu1C9m7d2/3KGua5bN3ALBVbfYZsquTLI0xFsYYl40xnpPk9iQvncZaquqFSV6Y5L2bPBsAQIvNDrJrk9x0wrZ3Jvn+JB+oqk9m5ezXPxxjrHrJEuhx4sdc+NgLgDNnUy9ZjjFetsq2N2/mDAAAs6blg2GBrclZMYCN4Z9OAgBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKDZXPcAs2zXrl05duRL3WPMlIWFhe4RAGDbEWTrmJ+fzyN3HOoeY6YsLi52jwAA245LlgAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBsrnuAWff5Bx/NL9xy55c9TvJl287ke11+xl8VAJh1gmwdCwsLX7HtvOXlJMm58/Nn/P0uX+M9AYDtTZCtY3FxsXsEAGAHcA8ZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANJvrHmCWLS0tZTKZrPn88vJykmR+fn6zRnrSFhYWsri42D0GAHAcQbaOyWSSWz/z2TztGRev+vyhBw4lSY7WfZs51hN26P67ukcAAFYhyE7iac+4OC988VWrPnfLH/1Gkqz5/Kx5bF4AYLa4hwwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaDbXPcAsW15ezpceeqR7DJotLS0lSRYXF5snAWC7EmTrOHz4cI4ePdI9Bs0mk0n3CABscy5ZAgA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANNuwIKuqV1fVqKpvOG7bzVV1b1X91gn7Xl5VH6qqz1TV26rq3I2aC4DZt2fPnsf/g51gI8+QXZvkg0muOW7bG5N83yr7/lySN40xnpvki0leu4FzAQDMlA0Jsqo6P8lLshJWjwfZGON9SR44Yd9K8vIk75huemuSqzZiLgBm34lnxZwlYyeY26DXvSrJzWOMW6vqnqq6cozx0TX2vSjJvWOMI9PHn0vyrA2aa0f70qH7Mpncm3379nWPsqVMJpPs2rWrewwAtrGNumR5bZIbp9/fOH28llpl21hz56rrqupAVR04ePDgkxgRAGA2nPEzZFV1UVYuQb6gqkaSs5OMqvqxMcZqoXVXkguram56luzZSe5Y6/XHGNcnuT5Jdu/evWa48ZWe8rQL8qxLL8jevXu7R9lSnFEEYKNtxBmyq5MsjTEWxhiXjTGek+T2JN+62s7TSHv/9OeS5DVJfnMD5gIAmEkbEWTXJrnphG3vTLKnqj6Q5NeTfHtVfa6qXjF9/t8k+ZdVdVtW7in7lQ2YC4AtYP/+/es+hu3ojF+yHGO8bJVtbz7Jz/xFkhed6VkAALaCjfotSwB4wpwVY6fxTycBADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0Gyue4BZtmvXrhw5Wt1j0GxhYaF7BAC2OUG2jvn5+Xz+r+/rHoNmi4uL3SMAsM25ZAkA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANJvrHmDWHbr/rtzyR7+x5nNJ1nx+1hy6/67k0gu6xwAATiDI1rGwsLDu88vj4STJ/FaJnEsvOOmfCQDYfIJsHYuLi90jAAA7gHvIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoNlc9wCzbGlpKZPJ5JT2XV5eTpLMz89v5Egzb2FhIYuLi91jAMCWIsjWMZlMcvutn838+ReddN+HHjyUJHn42L0bPdbMWn7w7u4RAGBLEmQnMX/+RfnHL/zek+73llvenSSntO929dgaAACnxz1kAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0Gyue4BZtry8nCMPH+4eAzbV0tJSkmRxcbF5EoCdQ5Ct4/Dhwzl69Ej3GLCpJpNJ9wgAO45LlgAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM3mNuqFq+rVSd6V5HljjE9Nt92c5MVJPjjG+DvH7ftrSXYneTTJh5P84Bjj0Y2aDQAgSfbs2fP49/v372+bYyPPkF2b5INJrjlu2xuTfN8q+/5akm9I8reSnJfkBzZwLgCAmbIhQVZV5yd5SZLX5rggG2O8L8kDJ+4/xnjPmMrKGbJnb8RcAACPOf7s2GqPN9NGXbK8KsnNY4xbq+qeqrpyjPHRk/1QVZ2TlTNoP7JBc7GB7n74vhyd3Jd9+/Z1j8KTMJlMsmvXru4xAHaUjbpkeW2SG6ff3zh9fCp+MckfjDE+sNYOVXVdVR2oqgMHDx58kmMCAPQ742fIquqiJC9P8oKqGknOTjKq6semlyTX+rmfSHJJkh9c7/XHGNcnuT5Jdu/evebrsfkuOu+CnPe1F2bv3r3do/AkOMMJsPk24gzZ1UmWxhgLY4zLxhjPSXJ7km9d6weq6geSvCLJtWOMYxswEwDAzNqIILs2yU0nbHtnkj1V9YEkv57k26vqc1X1iunz/y3JpUn+sKo+VlWv34C5AAAed+LHXHR+7MUZv2Q5xnjZKtvefJKf2bDPQwMAmHVCCADYsTrPih3PP50EANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADN5roHmGW7du3KkSPdU8DmWlhY6B4BYMcRZOuYn5/Pw3fc2z0GbKrFxcXuEQB2HJcsAQCaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoNlc9wCzbvnBu/OWW9590v2+8ODdSXJK+25Xyw/enctzYfcYALDlCLJ1LCwsnPK+T13+UpLkvPmdGySX58LTWjMAYIUgW8fi4mL3CADADuAeMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGg21z3ALHvd616X+++/P/Pz81lYWMji4mL3SADANiTI1nHw4ME89PBDeeDQF7tHAQC2MZcsT2LunOQZl1gmAGDjKA0AgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoNtc9wCx75JFHcvRYcujeY1l+aLl7HABgmxJk6zh27FjGSI4+mhweh7vHAQC2KZcsAQCaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGg2t96TVXVRkvdNH84nOZrk4PTxi8YYj5zpgarqyiRfPca4+Uy/NgDALFo3yMYYdye5Ikmq6g1JHhxj/KdTffGqOnuMcfQ0Z7oyyQuSCDIAYEd4wpcsq+p/VtVHquoTVfUD021zVXVvVf1UVX04yYuq6nur6tNV9YGq+oWq+o3pvudX1a9W1Yer6k+q6u9W1XlJXp/kH1TVx6rq6jPypwQAmGHrniE7ideMMe6pqqcmOVBV70zyQJILknx0jPHvp8/dmuQlSf4qyduP+/nXJ7l5jPH9VfVVST6U5IVJ/kOSF4wxfvRJzAYAsGU8mZv6/0VVfTzJHyZ5dpKvm25/JMlN0++fn+TTY4zJGGMkueG4n//OJP+uqj6W5P1JnpLkb5zsTavquqo6UFUHDh48eLLdAQBm3hM6Q1ZV35HkpUlePMZ4uKo+mJWgSpKHp/GVJLXeyyS5aozx2RNe+6XrvfcY4/ok1yfJ7t27x3r7AgBsBU/0DNkFSe6Zxtg3Jvnba+z3iSRfX1XPqapK8vePe+63k/zzxx5U1TdPv30gydOf4FwAAFvOEw2y/5XkqdNLlq/Pyv1fX2GM8VCSH07yu0k+kOSOJPdNn/7J6Wv8aVV9Iskbptt/L8k3TW/0d1M/ALDtnfIlyzHGG477/ktJXrHGrhee8Ph3xxhfPz1D9t+THJi+xqEk/2SV9zmYZPepzgUAsNVtxif1/9PpjfufTHJekl/ehPcEANgynszHXpySMcYbk7xxo98HAGCr8m9ZAgA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAEAzQQYA0EyQAQA0E2QAAM0EGQBAM0G2jrPOOitVydnnJLt27eoeBwDYpua6B5hl5557bh45ciRPu/CsXPqM+e5xAIBtyhkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbIAACaCTIAgGaCDACgmSADAGgmyAAAmgkyAIBmggwAoJkgAwBoJsgAAJoJMgCAZoIMAKCZIAMAaCbITuLIo8n9B491jwEAbGNz3QPMsksuuST3339/5ufns7Cw0D0OALBNCbJ1/MzP/Ez3CADADuCSJQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQTJABADQTZAAAzQQZAECzGmN0z/CEVdXBJJMNfpuLk9y1we+x3Viz02O9To/1On3W7PRYr9NnzU7NwhjjktWe2NJBthmq6sAYY3f3HFuJNTs91uv0WK/TZ81Oj/U6fdbsyXPJEgCgmSADAGgmyE7u+u4BtiBrdnqs1+mxXqfPmp0e63X6rNmT5B4yAIBmzpABADQTZOuoqldW1aer6raq+vHueWZRVf1lVf1pVX2sqg5Mtz2zqn6nqj4z/fpV3XN2qqq3VNWdVfVnx21bdY1qxZunx9wtVXVl3+Q91livN1TV56fH2ceq6ruPe+510/X6dFW9omfqPlX1nKp6f1X9eVV9oqp+ZLrdMbaGddbMcbaKqnpKVX24qj4+Xa+fnG6/vKo+ND3G3lZV506375o+vm36/GWd828VgmwNVXV2kv+a5LuSPD/JtVX1/N6pZta3jTGuOO5Xnn88yfvGGM9N8r7p453sV5O88oRta63RdyV57vS/65L80ibNOEt+NV+5XknypulxdsUY4z1JMv07eU2Sb5z+zC9O/+7uJEeS/KsxxvOSvDjJD03XxTG2trXWLHGcreZwkpePMb4pyRVJXllVL07yc1lZr+cm+WKS1073f22SL44x/maSN0334yQE2dpelOS2McZfjDEeSXJjklc1z7RVvCrJW6ffvzXJVY2ztBtj/EGSe07YvNYavSrJ0ljxR0kurKqv2ZxJZ8Ma67WWVyW5cYxxeIxxe5LbsvJ3d8cYY3xhjPHR6fcPJPnzJM+KY2xN66zZWnb0cTY9Vh6cPjxn+t9I8vIk75huP/EYe+zYe0eSb6+q2qRxtyxBtrZnJfm/xz3+XNb/C7tTjSTvraqPVNV1022XjjG+kKz8D1+Sr26bbnattUaOu7X98PQS21uOuwxuvY4zvTT0zUk+FMfYKTlhzRLH2aqq6uyq+liSO5P8TpLPJrl3jHFkusvxa/L4ek2fvy/JRZs78dYjyNa2Ws37ldSv9JIxxpVZuQzyQ1X10u6BtjjH3ep+KcnXZeVyyReS/Ofpdus1VVXnJ3lnkh8dY9y/3q6rbLNmK2vmOFvDGOPoGOOKJM/OytnB56222/Trjl+vJ0KQre1zSZ5z3ONnJ7mjaZaZNca4Y/r1ziQ3ZeUv6l8/dglk+vXOvgln1lpr5LhbxRjjr6f/h3AsyS/n/18usl5JquqcrITFr40x3jXd7Bhbx2pr5jg7uTHGvUn+d1buvbuwquamTx2/Jo+v1/T5C3LqtyHsWIJsbX+c5LnT3yI5Nys3dL67eaaZUlVPq6qnP/Z9ku9M8mdZWafXTHd7TZLf7Jlwpq21Ru9Osjj9TbgXJ7nvsctOO9kJ9zi9OivHWbKyXtdMf6vr8qzcqP7hzZ6v0/TenF9J8udjjJ8/7inH2BrWWjPH2eqq6pKqunD6/XlJviMr9929P8nV091OPMYeO/auTvJ7w4eentTcyXfZmcYYR6rqh5P8dpKzk7xljPGJ5rFmzaVJbpreqzmXZP8Y4+aq+uMkb6+q1yb5qyR/r3HGdlV1Q5KXJbm4qj6X5CeS/GxWX6P3JPnurNw0/FCSf7TpAzdbY71eVlVXZOWyx18m+cEkGWN8oqrenuSTWfnNuR8aYxztmLvRS5J8X5I/nd7jkyT/No6x9ay1Ztc6zlb1NUneOv3N0rOSvH2M8VtV9ckkN1bVTyX5k6xEbqZf/0dV3ZaVM2PXdAy91fikfgCAZi5ZAgA0E2QAAM0EGQBAM0EGANBMkAEANBNkAADNBBkAQDNBBgDQ7P8Bt6sV//x/mpIAAAAASUVORK5CYII=
)</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [18]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">pairplot</span><span class="p">(</span><span class="n">df_flt</span><span class="p">,</span> <span class="n">hue</span><span class="o">=</span><span class="s1">'Target'</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[18]:</div>

<div class="output_text output_subarea output_execute_result">

<pre><seaborn.axisgrid.PairGrid at 0x1bc2a4e2188></pre>

</div>

</div>

<div class="output_area">

<div class="output_png output_subarea ">![](data:image/png;base64,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
)</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Data Normalization[¶](#Data-Normalization)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [19]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">scaler</span> <span class="o">=</span> <span class="n">Normalizer</span><span class="p">()</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">'Target'</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">))</span>
<span class="n">standarized_x</span> <span class="o">=</span> <span class="n">scaler</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">'Target'</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Get Training and Testing Set[¶](#Get-Training-and-Testing-Set)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Selection of training and testing set is done to check our model’s performance on unseen data usually the accuracy which we print for our model is derived on validation set only (I am pronouncing our testing set as validation set here). W9e would like to keep 80% of our total data as training set and remaining 20% as our validation set (testing set). We cannot simply keep aside 80% and 20% set, the validation set should reflect as a reduced or thinned down version of training set. We used sklearn’s `train_test_split()` function to split our data frame to training and testing set.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [20]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># We want to split data -> test 80% and train 20%</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">standarized_x</span><span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">Target</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.2</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [21]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">X_train</span><span class="o">.</span><span class="n">size</span><span class="o">/</span><span class="n">df</span><span class="o">.</span><span class="n">size</span><span class="p">,</span> <span class="n">X_test</span><span class="o">.</span><span class="n">size</span><span class="o">/</span><span class="n">df</span><span class="o">.</span><span class="n">size</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[21]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>(0.768, 0.192)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

* * *

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

# Train a Model[¶](#Train-a-Model)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Create a Model[¶](#Create-a-Model)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [22]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Random Forest Model</span>
<span class="n">rf_model</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [23]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Support Vector Machine model</span>
<span class="n">svm_model</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">LinearSVC</span><span class="p">(</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">2000</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [39]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [41]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>0.8937256079255479
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [42]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>[[4299  338]
 [ 370 1655]]
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [15]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Fit the Model[¶](#Fit-the-Model)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [24]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Random Forest Model</span>
<span class="n">rf_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span><span class="n">y_train</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[24]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>RandomForestClassifier(bootstrap=True, ccp_alpha=0.0, class_weight=None,
                       criterion='gini', max_depth=None, max_features='auto',
                       max_leaf_nodes=None, max_samples=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, n_estimators=100,
                       n_jobs=None, oob_score=False, random_state=None,
                       verbose=0, warm_start=False)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [25]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Support Vector Machine model</span>
<span class="n">svm_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[25]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>LinearSVC(C=1.0, class_weight=None, dual=True, fit_intercept=True,
          intercept_scaling=1, loss='squared_hinge', max_iter=2000,
          multi_class='ovr', penalty='l2', random_state=None, tol=0.0001,
          verbose=0)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Test the Model[¶](#Test-the-Model)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [26]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Random Forest Model</span>
<span class="n">rf_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[26]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>array([1, 0, 0, ..., 0, 0, 1], dtype=int64)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [27]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Support Vector Machine model</span>
<span class="n">svm_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="prompt output_prompt">Out[27]:</div>

<div class="output_text output_subarea output_execute_result">

<pre>array([0, 0, 0, ..., 0, 0, 0], dtype=int64)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### Evaluate Model Performance[¶](#Evaluate-Model-Performance)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [43]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Support Vector Machine model</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">svm_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">"Accuracy:"</span><span class="p">,</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">"</span><span class="se">\n</span><span class="s2">"</span><span class="p">,</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>Accuracy: 0.6796757730411288

 [[4528    0]
 [2134    0]]
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [44]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1"># Random Forest Model</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">rf_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">"Accuracy:"</span><span class="p">,</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">"</span><span class="se">\n</span><span class="s2">"</span><span class="p">,</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_subarea output_stream output_stdout output_text">

<pre>Accuracy: 0.8989792854998498

 [[4224  304]
 [ 369 1765]]
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Suggest ways of improving the model[¶](#Suggest-ways-of-improving-the-model)

The model can be further improved with more data and a better algorithm that can handle biased data. Also, if we apply focal loss over these types of problem, we would get better results.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Any interesting observations[¶](#Any-interesting-observations)

This problem is so simple that even without any tricks we were able to achieve 80% accuracy, these seems to be directly coming from the Bayes theory. The dataset is having a smaller number of positive samples which further makes our model bias towards predicting fewer positive samples. Even if we have a testing set, to test the robustness of our model needs to be tested with a different dataset with different number of positive over negative samples.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Challenges faced and how you mitigated the challenges[¶](#Challenges-faced-and-how-you-mitigated-the-challenges)

We initially used an SVM and did not normalize our data, we fed the data as it is inside the model, doing this we were able to get an accuracy of 80%. Then we started experimenting with the data pipeline and hyperparameters. We started with reducing the no of parameters by checking for the most important ones, then we normalized the dataset and finally we used a random forest classifier. With each of these changes we were able to improve our model accuracy to nearly 90%.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Assumptions if any[¶](#Assumptions-if-any)

No, I am not aware of.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## Save the Model[¶](#Save-the-Model)

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [46]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">model_name</span> <span class="o">=</span> <span class="s1">'trained_model_SVM.pkl'</span>
<span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="n">model_name</span><span class="p">,</span> <span class="s1">'wb'</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span>
    <span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">svm_model</span><span class="p">,</span> <span class="n">f</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [47]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">model_name</span> <span class="o">=</span> <span class="s1">'trained_model_RF.pkl'</span>
<span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="n">model_name</span><span class="p">,</span> <span class="s1">'wb'</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span>
    <span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">rf_model</span><span class="p">,</span> <span class="n">f</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span> 
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

</div>