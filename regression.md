## Part 1: EDA

_Insert cells as needed below to write a short EDA/data section that summarizes the data for someone who has never opened it before._ 
- Answer essential questions about the dataset (observation units, time period, sample size, many of the questions above) 
- Note any issues you have with the data (variable X has problem Y that needs to get addressed before using it in regressions or a prediction model because Z)
- Present any visual results you think are interesting or important

### Findings ###

- Unit of observation: house sales
- Time period: 2006-2008 (min & max values of v_Yr_Sold)
- Sample size: N = 1941
- Issues with the data:
    - Some variables do not have 1941 observations and have missing values (% of missing values shown in a table below)
- Continuous variables include: SalePrice, v_Lot_Frontage, v_Lot_Area, v_Garage_Area, v_Mas_Vnr_Area, v_BsmtFin_F_, v_BsmtFin_SF_2, v_Bsmt_Unf_SF, v_Total_Bsmt_SF
- Variables with discrete numbers include v_Year_built, v_Year_Remod/Add, v_Garage_Cars, V_Full_Bath, v_Bedroom, v_Kitchen
- Categorical variables include: v_Street, v_Lot_Contour, v_Lot_Config, v_Neighborhood, v_Bldg_Type, v_House_Style    
- Visually explore the relationship between `v_Sale_Price` and other variables.
  - For continuous variables - take note of whether the relationship seems linear or quadratic or polynomial
  - For categorical variables - maybe try a box plot for the various levels?
  - Take notes about what you find   


```python
import pandas as pd

housing = pd.read_csv('input_data2/housing_train.csv')
housing
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
      <th>parcel</th>
      <th>v_MS_SubClass</th>
      <th>v_MS_Zoning</th>
      <th>v_Lot_Frontage</th>
      <th>v_Lot_Area</th>
      <th>v_Street</th>
      <th>v_Alley</th>
      <th>v_Lot_Shape</th>
      <th>v_Land_Contour</th>
      <th>v_Utilities</th>
      <th>...</th>
      <th>v_Pool_Area</th>
      <th>v_Pool_QC</th>
      <th>v_Fence</th>
      <th>v_Misc_Feature</th>
      <th>v_Misc_Val</th>
      <th>v_Mo_Sold</th>
      <th>v_Yr_Sold</th>
      <th>v_Sale_Type</th>
      <th>v_Sale_Condition</th>
      <th>v_SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1056_528110080</td>
      <td>20</td>
      <td>RL</td>
      <td>107.0</td>
      <td>13891</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>2008</td>
      <td>New</td>
      <td>Partial</td>
      <td>372402</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1055_528108150</td>
      <td>20</td>
      <td>RL</td>
      <td>98.0</td>
      <td>12704</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>2008</td>
      <td>New</td>
      <td>Partial</td>
      <td>317500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1053_528104050</td>
      <td>20</td>
      <td>RL</td>
      <td>114.0</td>
      <td>14803</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2008</td>
      <td>New</td>
      <td>Partial</td>
      <td>385000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2213_909275160</td>
      <td>20</td>
      <td>RL</td>
      <td>126.0</td>
      <td>13108</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR2</td>
      <td>HLS</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>153500</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1051_528102030</td>
      <td>20</td>
      <td>RL</td>
      <td>96.0</td>
      <td>12444</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>11</td>
      <td>2008</td>
      <td>New</td>
      <td>Partial</td>
      <td>394617</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1936</th>
      <td>2524_534125210</td>
      <td>190</td>
      <td>RL</td>
      <td>79.0</td>
      <td>13110</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>MnPrv</td>
      <td>NaN</td>
      <td>0</td>
      <td>7</td>
      <td>2006</td>
      <td>WD</td>
      <td>Normal</td>
      <td>146500</td>
    </tr>
    <tr>
      <th>1937</th>
      <td>2846_909131125</td>
      <td>190</td>
      <td>RH</td>
      <td>NaN</td>
      <td>7082</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>7</td>
      <td>2006</td>
      <td>WD</td>
      <td>Normal</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>1938</th>
      <td>2605_535382020</td>
      <td>190</td>
      <td>RL</td>
      <td>60.0</td>
      <td>10800</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2006</td>
      <td>ConLD</td>
      <td>Normal</td>
      <td>160000</td>
    </tr>
    <tr>
      <th>1939</th>
      <td>1516_909101180</td>
      <td>190</td>
      <td>RL</td>
      <td>55.0</td>
      <td>5687</td>
      <td>Pave</td>
      <td>Grvl</td>
      <td>Reg</td>
      <td>Bnk</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>135900</td>
    </tr>
    <tr>
      <th>1940</th>
      <td>1387_905200100</td>
      <td>190</td>
      <td>RL</td>
      <td>60.0</td>
      <td>12900</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>2008</td>
      <td>WD</td>
      <td>Alloca</td>
      <td>95541</td>
    </tr>
  </tbody>
</table>
<p>1941 rows × 81 columns</p>
</div>




```python
housing.describe().T.style.format('{:,.2f}') # by transposing it, I can see more variables
```




<style type="text/css">
</style>
<table id="T_45205_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >count</th>
      <th class="col_heading level0 col1" >mean</th>
      <th class="col_heading level0 col2" >std</th>
      <th class="col_heading level0 col3" >min</th>
      <th class="col_heading level0 col4" >25%</th>
      <th class="col_heading level0 col5" >50%</th>
      <th class="col_heading level0 col6" >75%</th>
      <th class="col_heading level0 col7" >max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_45205_level0_row0" class="row_heading level0 row0" >v_MS_SubClass</th>
      <td id="T_45205_row0_col0" class="data row0 col0" >1,941.00</td>
      <td id="T_45205_row0_col1" class="data row0 col1" >58.09</td>
      <td id="T_45205_row0_col2" class="data row0 col2" >42.95</td>
      <td id="T_45205_row0_col3" class="data row0 col3" >20.00</td>
      <td id="T_45205_row0_col4" class="data row0 col4" >20.00</td>
      <td id="T_45205_row0_col5" class="data row0 col5" >50.00</td>
      <td id="T_45205_row0_col6" class="data row0 col6" >70.00</td>
      <td id="T_45205_row0_col7" class="data row0 col7" >190.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row1" class="row_heading level0 row1" >v_Lot_Frontage</th>
      <td id="T_45205_row1_col0" class="data row1 col0" >1,620.00</td>
      <td id="T_45205_row1_col1" class="data row1 col1" >69.30</td>
      <td id="T_45205_row1_col2" class="data row1 col2" >23.98</td>
      <td id="T_45205_row1_col3" class="data row1 col3" >21.00</td>
      <td id="T_45205_row1_col4" class="data row1 col4" >58.00</td>
      <td id="T_45205_row1_col5" class="data row1 col5" >68.00</td>
      <td id="T_45205_row1_col6" class="data row1 col6" >80.00</td>
      <td id="T_45205_row1_col7" class="data row1 col7" >313.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row2" class="row_heading level0 row2" >v_Lot_Area</th>
      <td id="T_45205_row2_col0" class="data row2 col0" >1,941.00</td>
      <td id="T_45205_row2_col1" class="data row2 col1" >10,284.77</td>
      <td id="T_45205_row2_col2" class="data row2 col2" >7,832.30</td>
      <td id="T_45205_row2_col3" class="data row2 col3" >1,470.00</td>
      <td id="T_45205_row2_col4" class="data row2 col4" >7,420.00</td>
      <td id="T_45205_row2_col5" class="data row2 col5" >9,450.00</td>
      <td id="T_45205_row2_col6" class="data row2 col6" >11,631.00</td>
      <td id="T_45205_row2_col7" class="data row2 col7" >164,660.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row3" class="row_heading level0 row3" >v_Overall_Qual</th>
      <td id="T_45205_row3_col0" class="data row3 col0" >1,941.00</td>
      <td id="T_45205_row3_col1" class="data row3 col1" >6.11</td>
      <td id="T_45205_row3_col2" class="data row3 col2" >1.40</td>
      <td id="T_45205_row3_col3" class="data row3 col3" >1.00</td>
      <td id="T_45205_row3_col4" class="data row3 col4" >5.00</td>
      <td id="T_45205_row3_col5" class="data row3 col5" >6.00</td>
      <td id="T_45205_row3_col6" class="data row3 col6" >7.00</td>
      <td id="T_45205_row3_col7" class="data row3 col7" >10.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row4" class="row_heading level0 row4" >v_Overall_Cond</th>
      <td id="T_45205_row4_col0" class="data row4 col0" >1,941.00</td>
      <td id="T_45205_row4_col1" class="data row4 col1" >5.57</td>
      <td id="T_45205_row4_col2" class="data row4 col2" >1.09</td>
      <td id="T_45205_row4_col3" class="data row4 col3" >1.00</td>
      <td id="T_45205_row4_col4" class="data row4 col4" >5.00</td>
      <td id="T_45205_row4_col5" class="data row4 col5" >5.00</td>
      <td id="T_45205_row4_col6" class="data row4 col6" >6.00</td>
      <td id="T_45205_row4_col7" class="data row4 col7" >9.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row5" class="row_heading level0 row5" >v_Year_Built</th>
      <td id="T_45205_row5_col0" class="data row5 col0" >1,941.00</td>
      <td id="T_45205_row5_col1" class="data row5 col1" >1,971.32</td>
      <td id="T_45205_row5_col2" class="data row5 col2" >30.21</td>
      <td id="T_45205_row5_col3" class="data row5 col3" >1,872.00</td>
      <td id="T_45205_row5_col4" class="data row5 col4" >1,953.00</td>
      <td id="T_45205_row5_col5" class="data row5 col5" >1,973.00</td>
      <td id="T_45205_row5_col6" class="data row5 col6" >2,001.00</td>
      <td id="T_45205_row5_col7" class="data row5 col7" >2,008.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row6" class="row_heading level0 row6" >v_Year_Remod/Add</th>
      <td id="T_45205_row6_col0" class="data row6 col0" >1,941.00</td>
      <td id="T_45205_row6_col1" class="data row6 col1" >1,984.07</td>
      <td id="T_45205_row6_col2" class="data row6 col2" >20.84</td>
      <td id="T_45205_row6_col3" class="data row6 col3" >1,950.00</td>
      <td id="T_45205_row6_col4" class="data row6 col4" >1,965.00</td>
      <td id="T_45205_row6_col5" class="data row6 col5" >1,993.00</td>
      <td id="T_45205_row6_col6" class="data row6 col6" >2,004.00</td>
      <td id="T_45205_row6_col7" class="data row6 col7" >2,009.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row7" class="row_heading level0 row7" >v_Mas_Vnr_Area</th>
      <td id="T_45205_row7_col0" class="data row7 col0" >1,923.00</td>
      <td id="T_45205_row7_col1" class="data row7 col1" >104.85</td>
      <td id="T_45205_row7_col2" class="data row7 col2" >184.98</td>
      <td id="T_45205_row7_col3" class="data row7 col3" >0.00</td>
      <td id="T_45205_row7_col4" class="data row7 col4" >0.00</td>
      <td id="T_45205_row7_col5" class="data row7 col5" >0.00</td>
      <td id="T_45205_row7_col6" class="data row7 col6" >168.00</td>
      <td id="T_45205_row7_col7" class="data row7 col7" >1,600.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row8" class="row_heading level0 row8" >v_BsmtFin_SF_1</th>
      <td id="T_45205_row8_col0" class="data row8 col0" >1,940.00</td>
      <td id="T_45205_row8_col1" class="data row8 col1" >436.99</td>
      <td id="T_45205_row8_col2" class="data row8 col2" >457.82</td>
      <td id="T_45205_row8_col3" class="data row8 col3" >0.00</td>
      <td id="T_45205_row8_col4" class="data row8 col4" >0.00</td>
      <td id="T_45205_row8_col5" class="data row8 col5" >361.50</td>
      <td id="T_45205_row8_col6" class="data row8 col6" >735.25</td>
      <td id="T_45205_row8_col7" class="data row8 col7" >5,644.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row9" class="row_heading level0 row9" >v_BsmtFin_SF_2</th>
      <td id="T_45205_row9_col0" class="data row9 col0" >1,940.00</td>
      <td id="T_45205_row9_col1" class="data row9 col1" >49.25</td>
      <td id="T_45205_row9_col2" class="data row9 col2" >169.56</td>
      <td id="T_45205_row9_col3" class="data row9 col3" >0.00</td>
      <td id="T_45205_row9_col4" class="data row9 col4" >0.00</td>
      <td id="T_45205_row9_col5" class="data row9 col5" >0.00</td>
      <td id="T_45205_row9_col6" class="data row9 col6" >0.00</td>
      <td id="T_45205_row9_col7" class="data row9 col7" >1,474.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row10" class="row_heading level0 row10" >v_Bsmt_Unf_SF</th>
      <td id="T_45205_row10_col0" class="data row10 col0" >1,940.00</td>
      <td id="T_45205_row10_col1" class="data row10 col1" >567.44</td>
      <td id="T_45205_row10_col2" class="data row10 col2" >439.60</td>
      <td id="T_45205_row10_col3" class="data row10 col3" >0.00</td>
      <td id="T_45205_row10_col4" class="data row10 col4" >225.75</td>
      <td id="T_45205_row10_col5" class="data row10 col5" >474.00</td>
      <td id="T_45205_row10_col6" class="data row10 col6" >815.00</td>
      <td id="T_45205_row10_col7" class="data row10 col7" >2,153.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row11" class="row_heading level0 row11" >v_Total_Bsmt_SF</th>
      <td id="T_45205_row11_col0" class="data row11 col0" >1,940.00</td>
      <td id="T_45205_row11_col1" class="data row11 col1" >1,053.67</td>
      <td id="T_45205_row11_col2" class="data row11 col2" >438.66</td>
      <td id="T_45205_row11_col3" class="data row11 col3" >0.00</td>
      <td id="T_45205_row11_col4" class="data row11 col4" >796.75</td>
      <td id="T_45205_row11_col5" class="data row11 col5" >989.50</td>
      <td id="T_45205_row11_col6" class="data row11 col6" >1,295.25</td>
      <td id="T_45205_row11_col7" class="data row11 col7" >6,110.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row12" class="row_heading level0 row12" >v_1st_Flr_SF</th>
      <td id="T_45205_row12_col0" class="data row12 col0" >1,941.00</td>
      <td id="T_45205_row12_col1" class="data row12 col1" >1,161.07</td>
      <td id="T_45205_row12_col2" class="data row12 col2" >396.95</td>
      <td id="T_45205_row12_col3" class="data row12 col3" >334.00</td>
      <td id="T_45205_row12_col4" class="data row12 col4" >886.00</td>
      <td id="T_45205_row12_col5" class="data row12 col5" >1,085.00</td>
      <td id="T_45205_row12_col6" class="data row12 col6" >1,383.00</td>
      <td id="T_45205_row12_col7" class="data row12 col7" >5,095.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row13" class="row_heading level0 row13" >v_2nd_Flr_SF</th>
      <td id="T_45205_row13_col0" class="data row13 col0" >1,941.00</td>
      <td id="T_45205_row13_col1" class="data row13 col1" >340.96</td>
      <td id="T_45205_row13_col2" class="data row13 col2" >434.24</td>
      <td id="T_45205_row13_col3" class="data row13 col3" >0.00</td>
      <td id="T_45205_row13_col4" class="data row13 col4" >0.00</td>
      <td id="T_45205_row13_col5" class="data row13 col5" >0.00</td>
      <td id="T_45205_row13_col6" class="data row13 col6" >717.00</td>
      <td id="T_45205_row13_col7" class="data row13 col7" >2,065.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row14" class="row_heading level0 row14" >v_Low_Qual_Fin_SF</th>
      <td id="T_45205_row14_col0" class="data row14 col0" >1,941.00</td>
      <td id="T_45205_row14_col1" class="data row14 col1" >4.28</td>
      <td id="T_45205_row14_col2" class="data row14 col2" >42.94</td>
      <td id="T_45205_row14_col3" class="data row14 col3" >0.00</td>
      <td id="T_45205_row14_col4" class="data row14 col4" >0.00</td>
      <td id="T_45205_row14_col5" class="data row14 col5" >0.00</td>
      <td id="T_45205_row14_col6" class="data row14 col6" >0.00</td>
      <td id="T_45205_row14_col7" class="data row14 col7" >697.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row15" class="row_heading level0 row15" >v_Gr_Liv_Area</th>
      <td id="T_45205_row15_col0" class="data row15 col0" >1,941.00</td>
      <td id="T_45205_row15_col1" class="data row15 col1" >1,506.31</td>
      <td id="T_45205_row15_col2" class="data row15 col2" >524.77</td>
      <td id="T_45205_row15_col3" class="data row15 col3" >334.00</td>
      <td id="T_45205_row15_col4" class="data row15 col4" >1,118.00</td>
      <td id="T_45205_row15_col5" class="data row15 col5" >1,436.00</td>
      <td id="T_45205_row15_col6" class="data row15 col6" >1,755.00</td>
      <td id="T_45205_row15_col7" class="data row15 col7" >5,642.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row16" class="row_heading level0 row16" >v_Bsmt_Full_Bath</th>
      <td id="T_45205_row16_col0" class="data row16 col0" >1,939.00</td>
      <td id="T_45205_row16_col1" class="data row16 col1" >0.42</td>
      <td id="T_45205_row16_col2" class="data row16 col2" >0.52</td>
      <td id="T_45205_row16_col3" class="data row16 col3" >0.00</td>
      <td id="T_45205_row16_col4" class="data row16 col4" >0.00</td>
      <td id="T_45205_row16_col5" class="data row16 col5" >0.00</td>
      <td id="T_45205_row16_col6" class="data row16 col6" >1.00</td>
      <td id="T_45205_row16_col7" class="data row16 col7" >2.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row17" class="row_heading level0 row17" >v_Bsmt_Half_Bath</th>
      <td id="T_45205_row17_col0" class="data row17 col0" >1,939.00</td>
      <td id="T_45205_row17_col1" class="data row17 col1" >0.06</td>
      <td id="T_45205_row17_col2" class="data row17 col2" >0.25</td>
      <td id="T_45205_row17_col3" class="data row17 col3" >0.00</td>
      <td id="T_45205_row17_col4" class="data row17 col4" >0.00</td>
      <td id="T_45205_row17_col5" class="data row17 col5" >0.00</td>
      <td id="T_45205_row17_col6" class="data row17 col6" >0.00</td>
      <td id="T_45205_row17_col7" class="data row17 col7" >2.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row18" class="row_heading level0 row18" >v_Full_Bath</th>
      <td id="T_45205_row18_col0" class="data row18 col0" >1,941.00</td>
      <td id="T_45205_row18_col1" class="data row18 col1" >1.57</td>
      <td id="T_45205_row18_col2" class="data row18 col2" >0.55</td>
      <td id="T_45205_row18_col3" class="data row18 col3" >0.00</td>
      <td id="T_45205_row18_col4" class="data row18 col4" >1.00</td>
      <td id="T_45205_row18_col5" class="data row18 col5" >2.00</td>
      <td id="T_45205_row18_col6" class="data row18 col6" >2.00</td>
      <td id="T_45205_row18_col7" class="data row18 col7" >3.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row19" class="row_heading level0 row19" >v_Half_Bath</th>
      <td id="T_45205_row19_col0" class="data row19 col0" >1,941.00</td>
      <td id="T_45205_row19_col1" class="data row19 col1" >0.38</td>
      <td id="T_45205_row19_col2" class="data row19 col2" >0.50</td>
      <td id="T_45205_row19_col3" class="data row19 col3" >0.00</td>
      <td id="T_45205_row19_col4" class="data row19 col4" >0.00</td>
      <td id="T_45205_row19_col5" class="data row19 col5" >0.00</td>
      <td id="T_45205_row19_col6" class="data row19 col6" >1.00</td>
      <td id="T_45205_row19_col7" class="data row19 col7" >2.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row20" class="row_heading level0 row20" >v_Bedroom_AbvGr</th>
      <td id="T_45205_row20_col0" class="data row20 col0" >1,941.00</td>
      <td id="T_45205_row20_col1" class="data row20 col1" >2.87</td>
      <td id="T_45205_row20_col2" class="data row20 col2" >0.83</td>
      <td id="T_45205_row20_col3" class="data row20 col3" >0.00</td>
      <td id="T_45205_row20_col4" class="data row20 col4" >2.00</td>
      <td id="T_45205_row20_col5" class="data row20 col5" >3.00</td>
      <td id="T_45205_row20_col6" class="data row20 col6" >3.00</td>
      <td id="T_45205_row20_col7" class="data row20 col7" >8.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row21" class="row_heading level0 row21" >v_Kitchen_AbvGr</th>
      <td id="T_45205_row21_col0" class="data row21 col0" >1,941.00</td>
      <td id="T_45205_row21_col1" class="data row21 col1" >1.04</td>
      <td id="T_45205_row21_col2" class="data row21 col2" >0.20</td>
      <td id="T_45205_row21_col3" class="data row21 col3" >0.00</td>
      <td id="T_45205_row21_col4" class="data row21 col4" >1.00</td>
      <td id="T_45205_row21_col5" class="data row21 col5" >1.00</td>
      <td id="T_45205_row21_col6" class="data row21 col6" >1.00</td>
      <td id="T_45205_row21_col7" class="data row21 col7" >2.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row22" class="row_heading level0 row22" >v_TotRms_AbvGrd</th>
      <td id="T_45205_row22_col0" class="data row22 col0" >1,941.00</td>
      <td id="T_45205_row22_col1" class="data row22 col1" >6.47</td>
      <td id="T_45205_row22_col2" class="data row22 col2" >1.58</td>
      <td id="T_45205_row22_col3" class="data row22 col3" >2.00</td>
      <td id="T_45205_row22_col4" class="data row22 col4" >5.00</td>
      <td id="T_45205_row22_col5" class="data row22 col5" >6.00</td>
      <td id="T_45205_row22_col6" class="data row22 col6" >7.00</td>
      <td id="T_45205_row22_col7" class="data row22 col7" >15.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row23" class="row_heading level0 row23" >v_Fireplaces</th>
      <td id="T_45205_row23_col0" class="data row23 col0" >1,941.00</td>
      <td id="T_45205_row23_col1" class="data row23 col1" >0.60</td>
      <td id="T_45205_row23_col2" class="data row23 col2" >0.64</td>
      <td id="T_45205_row23_col3" class="data row23 col3" >0.00</td>
      <td id="T_45205_row23_col4" class="data row23 col4" >0.00</td>
      <td id="T_45205_row23_col5" class="data row23 col5" >1.00</td>
      <td id="T_45205_row23_col6" class="data row23 col6" >1.00</td>
      <td id="T_45205_row23_col7" class="data row23 col7" >4.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row24" class="row_heading level0 row24" >v_Garage_Yr_Blt</th>
      <td id="T_45205_row24_col0" class="data row24 col0" >1,834.00</td>
      <td id="T_45205_row24_col1" class="data row24 col1" >1,978.19</td>
      <td id="T_45205_row24_col2" class="data row24 col2" >25.73</td>
      <td id="T_45205_row24_col3" class="data row24 col3" >1,895.00</td>
      <td id="T_45205_row24_col4" class="data row24 col4" >1,960.00</td>
      <td id="T_45205_row24_col5" class="data row24 col5" >1,980.00</td>
      <td id="T_45205_row24_col6" class="data row24 col6" >2,002.00</td>
      <td id="T_45205_row24_col7" class="data row24 col7" >2,207.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row25" class="row_heading level0 row25" >v_Garage_Cars</th>
      <td id="T_45205_row25_col0" class="data row25 col0" >1,940.00</td>
      <td id="T_45205_row25_col1" class="data row25 col1" >1.77</td>
      <td id="T_45205_row25_col2" class="data row25 col2" >0.76</td>
      <td id="T_45205_row25_col3" class="data row25 col3" >0.00</td>
      <td id="T_45205_row25_col4" class="data row25 col4" >1.00</td>
      <td id="T_45205_row25_col5" class="data row25 col5" >2.00</td>
      <td id="T_45205_row25_col6" class="data row25 col6" >2.00</td>
      <td id="T_45205_row25_col7" class="data row25 col7" >4.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row26" class="row_heading level0 row26" >v_Garage_Area</th>
      <td id="T_45205_row26_col0" class="data row26 col0" >1,940.00</td>
      <td id="T_45205_row26_col1" class="data row26 col1" >472.77</td>
      <td id="T_45205_row26_col2" class="data row26 col2" >217.09</td>
      <td id="T_45205_row26_col3" class="data row26 col3" >0.00</td>
      <td id="T_45205_row26_col4" class="data row26 col4" >318.75</td>
      <td id="T_45205_row26_col5" class="data row26 col5" >478.00</td>
      <td id="T_45205_row26_col6" class="data row26 col6" >576.00</td>
      <td id="T_45205_row26_col7" class="data row26 col7" >1,488.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row27" class="row_heading level0 row27" >v_Wood_Deck_SF</th>
      <td id="T_45205_row27_col0" class="data row27 col0" >1,941.00</td>
      <td id="T_45205_row27_col1" class="data row27 col1" >92.46</td>
      <td id="T_45205_row27_col2" class="data row27 col2" >127.02</td>
      <td id="T_45205_row27_col3" class="data row27 col3" >0.00</td>
      <td id="T_45205_row27_col4" class="data row27 col4" >0.00</td>
      <td id="T_45205_row27_col5" class="data row27 col5" >0.00</td>
      <td id="T_45205_row27_col6" class="data row27 col6" >168.00</td>
      <td id="T_45205_row27_col7" class="data row27 col7" >1,424.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row28" class="row_heading level0 row28" >v_Open_Porch_SF</th>
      <td id="T_45205_row28_col0" class="data row28 col0" >1,941.00</td>
      <td id="T_45205_row28_col1" class="data row28 col1" >49.16</td>
      <td id="T_45205_row28_col2" class="data row28 col2" >70.30</td>
      <td id="T_45205_row28_col3" class="data row28 col3" >0.00</td>
      <td id="T_45205_row28_col4" class="data row28 col4" >0.00</td>
      <td id="T_45205_row28_col5" class="data row28 col5" >28.00</td>
      <td id="T_45205_row28_col6" class="data row28 col6" >72.00</td>
      <td id="T_45205_row28_col7" class="data row28 col7" >742.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row29" class="row_heading level0 row29" >v_Enclosed_Porch</th>
      <td id="T_45205_row29_col0" class="data row29 col0" >1,941.00</td>
      <td id="T_45205_row29_col1" class="data row29 col1" >22.95</td>
      <td id="T_45205_row29_col2" class="data row29 col2" >65.25</td>
      <td id="T_45205_row29_col3" class="data row29 col3" >0.00</td>
      <td id="T_45205_row29_col4" class="data row29 col4" >0.00</td>
      <td id="T_45205_row29_col5" class="data row29 col5" >0.00</td>
      <td id="T_45205_row29_col6" class="data row29 col6" >0.00</td>
      <td id="T_45205_row29_col7" class="data row29 col7" >1,012.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row30" class="row_heading level0 row30" >v_3Ssn_Porch</th>
      <td id="T_45205_row30_col0" class="data row30 col0" >1,941.00</td>
      <td id="T_45205_row30_col1" class="data row30 col1" >2.25</td>
      <td id="T_45205_row30_col2" class="data row30 col2" >22.42</td>
      <td id="T_45205_row30_col3" class="data row30 col3" >0.00</td>
      <td id="T_45205_row30_col4" class="data row30 col4" >0.00</td>
      <td id="T_45205_row30_col5" class="data row30 col5" >0.00</td>
      <td id="T_45205_row30_col6" class="data row30 col6" >0.00</td>
      <td id="T_45205_row30_col7" class="data row30 col7" >407.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row31" class="row_heading level0 row31" >v_Screen_Porch</th>
      <td id="T_45205_row31_col0" class="data row31 col0" >1,941.00</td>
      <td id="T_45205_row31_col1" class="data row31 col1" >16.25</td>
      <td id="T_45205_row31_col2" class="data row31 col2" >56.75</td>
      <td id="T_45205_row31_col3" class="data row31 col3" >0.00</td>
      <td id="T_45205_row31_col4" class="data row31 col4" >0.00</td>
      <td id="T_45205_row31_col5" class="data row31 col5" >0.00</td>
      <td id="T_45205_row31_col6" class="data row31 col6" >0.00</td>
      <td id="T_45205_row31_col7" class="data row31 col7" >576.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row32" class="row_heading level0 row32" >v_Pool_Area</th>
      <td id="T_45205_row32_col0" class="data row32 col0" >1,941.00</td>
      <td id="T_45205_row32_col1" class="data row32 col1" >3.39</td>
      <td id="T_45205_row32_col2" class="data row32 col2" >43.70</td>
      <td id="T_45205_row32_col3" class="data row32 col3" >0.00</td>
      <td id="T_45205_row32_col4" class="data row32 col4" >0.00</td>
      <td id="T_45205_row32_col5" class="data row32 col5" >0.00</td>
      <td id="T_45205_row32_col6" class="data row32 col6" >0.00</td>
      <td id="T_45205_row32_col7" class="data row32 col7" >800.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row33" class="row_heading level0 row33" >v_Misc_Val</th>
      <td id="T_45205_row33_col0" class="data row33 col0" >1,941.00</td>
      <td id="T_45205_row33_col1" class="data row33 col1" >52.55</td>
      <td id="T_45205_row33_col2" class="data row33 col2" >616.06</td>
      <td id="T_45205_row33_col3" class="data row33 col3" >0.00</td>
      <td id="T_45205_row33_col4" class="data row33 col4" >0.00</td>
      <td id="T_45205_row33_col5" class="data row33 col5" >0.00</td>
      <td id="T_45205_row33_col6" class="data row33 col6" >0.00</td>
      <td id="T_45205_row33_col7" class="data row33 col7" >17,000.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row34" class="row_heading level0 row34" >v_Mo_Sold</th>
      <td id="T_45205_row34_col0" class="data row34 col0" >1,941.00</td>
      <td id="T_45205_row34_col1" class="data row34 col1" >6.43</td>
      <td id="T_45205_row34_col2" class="data row34 col2" >2.75</td>
      <td id="T_45205_row34_col3" class="data row34 col3" >1.00</td>
      <td id="T_45205_row34_col4" class="data row34 col4" >5.00</td>
      <td id="T_45205_row34_col5" class="data row34 col5" >6.00</td>
      <td id="T_45205_row34_col6" class="data row34 col6" >8.00</td>
      <td id="T_45205_row34_col7" class="data row34 col7" >12.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row35" class="row_heading level0 row35" >v_Yr_Sold</th>
      <td id="T_45205_row35_col0" class="data row35 col0" >1,941.00</td>
      <td id="T_45205_row35_col1" class="data row35 col1" >2,007.00</td>
      <td id="T_45205_row35_col2" class="data row35 col2" >0.80</td>
      <td id="T_45205_row35_col3" class="data row35 col3" >2,006.00</td>
      <td id="T_45205_row35_col4" class="data row35 col4" >2,006.00</td>
      <td id="T_45205_row35_col5" class="data row35 col5" >2,007.00</td>
      <td id="T_45205_row35_col6" class="data row35 col6" >2,008.00</td>
      <td id="T_45205_row35_col7" class="data row35 col7" >2,008.00</td>
    </tr>
    <tr>
      <th id="T_45205_level0_row36" class="row_heading level0 row36" >v_SalePrice</th>
      <td id="T_45205_row36_col0" class="data row36 col0" >1,941.00</td>
      <td id="T_45205_row36_col1" class="data row36 col1" >182,033.24</td>
      <td id="T_45205_row36_col2" class="data row36 col2" >80,407.10</td>
      <td id="T_45205_row36_col3" class="data row36 col3" >13,100.00</td>
      <td id="T_45205_row36_col4" class="data row36 col4" >130,000.00</td>
      <td id="T_45205_row36_col5" class="data row36 col5" >161,900.00</td>
      <td id="T_45205_row36_col6" class="data row36 col6" >215,000.00</td>
      <td id="T_45205_row36_col7" class="data row36 col7" >755,000.00</td>
    </tr>
  </tbody>
</table>





```python
# Outliers
housing.describe(percentiles=[.01,.05,.95,.99]).T.style.format('{:,.2f}')

#for example, in v_Lot_Area, the max of 164,660 is an outlier.
```




<style type="text/css">
</style>
<table id="T_2dd4b_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >count</th>
      <th class="col_heading level0 col1" >mean</th>
      <th class="col_heading level0 col2" >std</th>
      <th class="col_heading level0 col3" >min</th>
      <th class="col_heading level0 col4" >1%</th>
      <th class="col_heading level0 col5" >5%</th>
      <th class="col_heading level0 col6" >50%</th>
      <th class="col_heading level0 col7" >95%</th>
      <th class="col_heading level0 col8" >99%</th>
      <th class="col_heading level0 col9" >max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_2dd4b_level0_row0" class="row_heading level0 row0" >v_MS_SubClass</th>
      <td id="T_2dd4b_row0_col0" class="data row0 col0" >1,941.00</td>
      <td id="T_2dd4b_row0_col1" class="data row0 col1" >58.09</td>
      <td id="T_2dd4b_row0_col2" class="data row0 col2" >42.95</td>
      <td id="T_2dd4b_row0_col3" class="data row0 col3" >20.00</td>
      <td id="T_2dd4b_row0_col4" class="data row0 col4" >20.00</td>
      <td id="T_2dd4b_row0_col5" class="data row0 col5" >20.00</td>
      <td id="T_2dd4b_row0_col6" class="data row0 col6" >50.00</td>
      <td id="T_2dd4b_row0_col7" class="data row0 col7" >160.00</td>
      <td id="T_2dd4b_row0_col8" class="data row0 col8" >190.00</td>
      <td id="T_2dd4b_row0_col9" class="data row0 col9" >190.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row1" class="row_heading level0 row1" >v_Lot_Frontage</th>
      <td id="T_2dd4b_row1_col0" class="data row1 col0" >1,620.00</td>
      <td id="T_2dd4b_row1_col1" class="data row1 col1" >69.30</td>
      <td id="T_2dd4b_row1_col2" class="data row1 col2" >23.98</td>
      <td id="T_2dd4b_row1_col3" class="data row1 col3" >21.00</td>
      <td id="T_2dd4b_row1_col4" class="data row1 col4" >21.00</td>
      <td id="T_2dd4b_row1_col5" class="data row1 col5" >34.00</td>
      <td id="T_2dd4b_row1_col6" class="data row1 col6" >68.00</td>
      <td id="T_2dd4b_row1_col7" class="data row1 col7" >107.05</td>
      <td id="T_2dd4b_row1_col8" class="data row1 col8" >135.81</td>
      <td id="T_2dd4b_row1_col9" class="data row1 col9" >313.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row2" class="row_heading level0 row2" >v_Lot_Area</th>
      <td id="T_2dd4b_row2_col0" class="data row2 col0" >1,941.00</td>
      <td id="T_2dd4b_row2_col1" class="data row2 col1" >10,284.77</td>
      <td id="T_2dd4b_row2_col2" class="data row2 col2" >7,832.30</td>
      <td id="T_2dd4b_row2_col3" class="data row2 col3" >1,470.00</td>
      <td id="T_2dd4b_row2_col4" class="data row2 col4" >1,688.00</td>
      <td id="T_2dd4b_row2_col5" class="data row2 col5" >3,523.00</td>
      <td id="T_2dd4b_row2_col6" class="data row2 col6" >9,450.00</td>
      <td id="T_2dd4b_row2_col7" class="data row2 col7" >17,778.00</td>
      <td id="T_2dd4b_row2_col8" class="data row2 col8" >38,062.40</td>
      <td id="T_2dd4b_row2_col9" class="data row2 col9" >164,660.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row3" class="row_heading level0 row3" >v_Overall_Qual</th>
      <td id="T_2dd4b_row3_col0" class="data row3 col0" >1,941.00</td>
      <td id="T_2dd4b_row3_col1" class="data row3 col1" >6.11</td>
      <td id="T_2dd4b_row3_col2" class="data row3 col2" >1.40</td>
      <td id="T_2dd4b_row3_col3" class="data row3 col3" >1.00</td>
      <td id="T_2dd4b_row3_col4" class="data row3 col4" >3.00</td>
      <td id="T_2dd4b_row3_col5" class="data row3 col5" >4.00</td>
      <td id="T_2dd4b_row3_col6" class="data row3 col6" >6.00</td>
      <td id="T_2dd4b_row3_col7" class="data row3 col7" >8.00</td>
      <td id="T_2dd4b_row3_col8" class="data row3 col8" >10.00</td>
      <td id="T_2dd4b_row3_col9" class="data row3 col9" >10.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row4" class="row_heading level0 row4" >v_Overall_Cond</th>
      <td id="T_2dd4b_row4_col0" class="data row4 col0" >1,941.00</td>
      <td id="T_2dd4b_row4_col1" class="data row4 col1" >5.57</td>
      <td id="T_2dd4b_row4_col2" class="data row4 col2" >1.09</td>
      <td id="T_2dd4b_row4_col3" class="data row4 col3" >1.00</td>
      <td id="T_2dd4b_row4_col4" class="data row4 col4" >3.00</td>
      <td id="T_2dd4b_row4_col5" class="data row4 col5" >4.00</td>
      <td id="T_2dd4b_row4_col6" class="data row4 col6" >5.00</td>
      <td id="T_2dd4b_row4_col7" class="data row4 col7" >8.00</td>
      <td id="T_2dd4b_row4_col8" class="data row4 col8" >9.00</td>
      <td id="T_2dd4b_row4_col9" class="data row4 col9" >9.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row5" class="row_heading level0 row5" >v_Year_Built</th>
      <td id="T_2dd4b_row5_col0" class="data row5 col0" >1,941.00</td>
      <td id="T_2dd4b_row5_col1" class="data row5 col1" >1,971.32</td>
      <td id="T_2dd4b_row5_col2" class="data row5 col2" >30.21</td>
      <td id="T_2dd4b_row5_col3" class="data row5 col3" >1,872.00</td>
      <td id="T_2dd4b_row5_col4" class="data row5 col4" >1,900.00</td>
      <td id="T_2dd4b_row5_col5" class="data row5 col5" >1,916.00</td>
      <td id="T_2dd4b_row5_col6" class="data row5 col6" >1,973.00</td>
      <td id="T_2dd4b_row5_col7" class="data row5 col7" >2,006.00</td>
      <td id="T_2dd4b_row5_col8" class="data row5 col8" >2,007.00</td>
      <td id="T_2dd4b_row5_col9" class="data row5 col9" >2,008.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row6" class="row_heading level0 row6" >v_Year_Remod/Add</th>
      <td id="T_2dd4b_row6_col0" class="data row6 col0" >1,941.00</td>
      <td id="T_2dd4b_row6_col1" class="data row6 col1" >1,984.07</td>
      <td id="T_2dd4b_row6_col2" class="data row6 col2" >20.84</td>
      <td id="T_2dd4b_row6_col3" class="data row6 col3" >1,950.00</td>
      <td id="T_2dd4b_row6_col4" class="data row6 col4" >1,950.00</td>
      <td id="T_2dd4b_row6_col5" class="data row6 col5" >1,950.00</td>
      <td id="T_2dd4b_row6_col6" class="data row6 col6" >1,993.00</td>
      <td id="T_2dd4b_row6_col7" class="data row6 col7" >2,007.00</td>
      <td id="T_2dd4b_row6_col8" class="data row6 col8" >2,008.00</td>
      <td id="T_2dd4b_row6_col9" class="data row6 col9" >2,009.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row7" class="row_heading level0 row7" >v_Mas_Vnr_Area</th>
      <td id="T_2dd4b_row7_col0" class="data row7 col0" >1,923.00</td>
      <td id="T_2dd4b_row7_col1" class="data row7 col1" >104.85</td>
      <td id="T_2dd4b_row7_col2" class="data row7 col2" >184.98</td>
      <td id="T_2dd4b_row7_col3" class="data row7 col3" >0.00</td>
      <td id="T_2dd4b_row7_col4" class="data row7 col4" >0.00</td>
      <td id="T_2dd4b_row7_col5" class="data row7 col5" >0.00</td>
      <td id="T_2dd4b_row7_col6" class="data row7 col6" >0.00</td>
      <td id="T_2dd4b_row7_col7" class="data row7 col7" >472.90</td>
      <td id="T_2dd4b_row7_col8" class="data row7 col8" >794.24</td>
      <td id="T_2dd4b_row7_col9" class="data row7 col9" >1,600.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row8" class="row_heading level0 row8" >v_BsmtFin_SF_1</th>
      <td id="T_2dd4b_row8_col0" class="data row8 col0" >1,940.00</td>
      <td id="T_2dd4b_row8_col1" class="data row8 col1" >436.99</td>
      <td id="T_2dd4b_row8_col2" class="data row8 col2" >457.82</td>
      <td id="T_2dd4b_row8_col3" class="data row8 col3" >0.00</td>
      <td id="T_2dd4b_row8_col4" class="data row8 col4" >0.00</td>
      <td id="T_2dd4b_row8_col5" class="data row8 col5" >0.00</td>
      <td id="T_2dd4b_row8_col6" class="data row8 col6" >361.50</td>
      <td id="T_2dd4b_row8_col7" class="data row8 col7" >1,249.00</td>
      <td id="T_2dd4b_row8_col8" class="data row8 col8" >1,600.93</td>
      <td id="T_2dd4b_row8_col9" class="data row8 col9" >5,644.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row9" class="row_heading level0 row9" >v_BsmtFin_SF_2</th>
      <td id="T_2dd4b_row9_col0" class="data row9 col0" >1,940.00</td>
      <td id="T_2dd4b_row9_col1" class="data row9 col1" >49.25</td>
      <td id="T_2dd4b_row9_col2" class="data row9 col2" >169.56</td>
      <td id="T_2dd4b_row9_col3" class="data row9 col3" >0.00</td>
      <td id="T_2dd4b_row9_col4" class="data row9 col4" >0.00</td>
      <td id="T_2dd4b_row9_col5" class="data row9 col5" >0.00</td>
      <td id="T_2dd4b_row9_col6" class="data row9 col6" >0.00</td>
      <td id="T_2dd4b_row9_col7" class="data row9 col7" >435.00</td>
      <td id="T_2dd4b_row9_col8" class="data row9 col8" >883.98</td>
      <td id="T_2dd4b_row9_col9" class="data row9 col9" >1,474.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row10" class="row_heading level0 row10" >v_Bsmt_Unf_SF</th>
      <td id="T_2dd4b_row10_col0" class="data row10 col0" >1,940.00</td>
      <td id="T_2dd4b_row10_col1" class="data row10 col1" >567.44</td>
      <td id="T_2dd4b_row10_col2" class="data row10 col2" >439.60</td>
      <td id="T_2dd4b_row10_col3" class="data row10 col3" >0.00</td>
      <td id="T_2dd4b_row10_col4" class="data row10 col4" >0.00</td>
      <td id="T_2dd4b_row10_col5" class="data row10 col5" >0.00</td>
      <td id="T_2dd4b_row10_col6" class="data row10 col6" >474.00</td>
      <td id="T_2dd4b_row10_col7" class="data row10 col7" >1,488.05</td>
      <td id="T_2dd4b_row10_col8" class="data row10 col8" >1,775.83</td>
      <td id="T_2dd4b_row10_col9" class="data row10 col9" >2,153.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row11" class="row_heading level0 row11" >v_Total_Bsmt_SF</th>
      <td id="T_2dd4b_row11_col0" class="data row11 col0" >1,940.00</td>
      <td id="T_2dd4b_row11_col1" class="data row11 col1" >1,053.67</td>
      <td id="T_2dd4b_row11_col2" class="data row11 col2" >438.66</td>
      <td id="T_2dd4b_row11_col3" class="data row11 col3" >0.00</td>
      <td id="T_2dd4b_row11_col4" class="data row11 col4" >0.00</td>
      <td id="T_2dd4b_row11_col5" class="data row11 col5" >483.00</td>
      <td id="T_2dd4b_row11_col6" class="data row11 col6" >989.50</td>
      <td id="T_2dd4b_row11_col7" class="data row11 col7" >1,776.05</td>
      <td id="T_2dd4b_row11_col8" class="data row11 col8" >2,138.44</td>
      <td id="T_2dd4b_row11_col9" class="data row11 col9" >6,110.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row12" class="row_heading level0 row12" >v_1st_Flr_SF</th>
      <td id="T_2dd4b_row12_col0" class="data row12 col0" >1,941.00</td>
      <td id="T_2dd4b_row12_col1" class="data row12 col1" >1,161.07</td>
      <td id="T_2dd4b_row12_col2" class="data row12 col2" >396.95</td>
      <td id="T_2dd4b_row12_col3" class="data row12 col3" >334.00</td>
      <td id="T_2dd4b_row12_col4" class="data row12 col4" >507.60</td>
      <td id="T_2dd4b_row12_col5" class="data row12 col5" >672.00</td>
      <td id="T_2dd4b_row12_col6" class="data row12 col6" >1,085.00</td>
      <td id="T_2dd4b_row12_col7" class="data row12 col7" >1,828.00</td>
      <td id="T_2dd4b_row12_col8" class="data row12 col8" >2,277.80</td>
      <td id="T_2dd4b_row12_col9" class="data row12 col9" >5,095.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row13" class="row_heading level0 row13" >v_2nd_Flr_SF</th>
      <td id="T_2dd4b_row13_col0" class="data row13 col0" >1,941.00</td>
      <td id="T_2dd4b_row13_col1" class="data row13 col1" >340.96</td>
      <td id="T_2dd4b_row13_col2" class="data row13 col2" >434.24</td>
      <td id="T_2dd4b_row13_col3" class="data row13 col3" >0.00</td>
      <td id="T_2dd4b_row13_col4" class="data row13 col4" >0.00</td>
      <td id="T_2dd4b_row13_col5" class="data row13 col5" >0.00</td>
      <td id="T_2dd4b_row13_col6" class="data row13 col6" >0.00</td>
      <td id="T_2dd4b_row13_col7" class="data row13 col7" >1,142.00</td>
      <td id="T_2dd4b_row13_col8" class="data row13 col8" >1,406.20</td>
      <td id="T_2dd4b_row13_col9" class="data row13 col9" >2,065.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row14" class="row_heading level0 row14" >v_Low_Qual_Fin_SF</th>
      <td id="T_2dd4b_row14_col0" class="data row14 col0" >1,941.00</td>
      <td id="T_2dd4b_row14_col1" class="data row14 col1" >4.28</td>
      <td id="T_2dd4b_row14_col2" class="data row14 col2" >42.94</td>
      <td id="T_2dd4b_row14_col3" class="data row14 col3" >0.00</td>
      <td id="T_2dd4b_row14_col4" class="data row14 col4" >0.00</td>
      <td id="T_2dd4b_row14_col5" class="data row14 col5" >0.00</td>
      <td id="T_2dd4b_row14_col6" class="data row14 col6" >0.00</td>
      <td id="T_2dd4b_row14_col7" class="data row14 col7" >0.00</td>
      <td id="T_2dd4b_row14_col8" class="data row14 col8" >111.60</td>
      <td id="T_2dd4b_row14_col9" class="data row14 col9" >697.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row15" class="row_heading level0 row15" >v_Gr_Liv_Area</th>
      <td id="T_2dd4b_row15_col0" class="data row15 col0" >1,941.00</td>
      <td id="T_2dd4b_row15_col1" class="data row15 col1" >1,506.31</td>
      <td id="T_2dd4b_row15_col2" class="data row15 col2" >524.77</td>
      <td id="T_2dd4b_row15_col3" class="data row15 col3" >334.00</td>
      <td id="T_2dd4b_row15_col4" class="data row15 col4" >691.80</td>
      <td id="T_2dd4b_row15_col5" class="data row15 col5" >864.00</td>
      <td id="T_2dd4b_row15_col6" class="data row15 col6" >1,436.00</td>
      <td id="T_2dd4b_row15_col7" class="data row15 col7" >2,500.00</td>
      <td id="T_2dd4b_row15_col8" class="data row15 col8" >3,029.20</td>
      <td id="T_2dd4b_row15_col9" class="data row15 col9" >5,642.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row16" class="row_heading level0 row16" >v_Bsmt_Full_Bath</th>
      <td id="T_2dd4b_row16_col0" class="data row16 col0" >1,939.00</td>
      <td id="T_2dd4b_row16_col1" class="data row16 col1" >0.42</td>
      <td id="T_2dd4b_row16_col2" class="data row16 col2" >0.52</td>
      <td id="T_2dd4b_row16_col3" class="data row16 col3" >0.00</td>
      <td id="T_2dd4b_row16_col4" class="data row16 col4" >0.00</td>
      <td id="T_2dd4b_row16_col5" class="data row16 col5" >0.00</td>
      <td id="T_2dd4b_row16_col6" class="data row16 col6" >0.00</td>
      <td id="T_2dd4b_row16_col7" class="data row16 col7" >1.00</td>
      <td id="T_2dd4b_row16_col8" class="data row16 col8" >2.00</td>
      <td id="T_2dd4b_row16_col9" class="data row16 col9" >2.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row17" class="row_heading level0 row17" >v_Bsmt_Half_Bath</th>
      <td id="T_2dd4b_row17_col0" class="data row17 col0" >1,939.00</td>
      <td id="T_2dd4b_row17_col1" class="data row17 col1" >0.06</td>
      <td id="T_2dd4b_row17_col2" class="data row17 col2" >0.25</td>
      <td id="T_2dd4b_row17_col3" class="data row17 col3" >0.00</td>
      <td id="T_2dd4b_row17_col4" class="data row17 col4" >0.00</td>
      <td id="T_2dd4b_row17_col5" class="data row17 col5" >0.00</td>
      <td id="T_2dd4b_row17_col6" class="data row17 col6" >0.00</td>
      <td id="T_2dd4b_row17_col7" class="data row17 col7" >1.00</td>
      <td id="T_2dd4b_row17_col8" class="data row17 col8" >1.00</td>
      <td id="T_2dd4b_row17_col9" class="data row17 col9" >2.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row18" class="row_heading level0 row18" >v_Full_Bath</th>
      <td id="T_2dd4b_row18_col0" class="data row18 col0" >1,941.00</td>
      <td id="T_2dd4b_row18_col1" class="data row18 col1" >1.57</td>
      <td id="T_2dd4b_row18_col2" class="data row18 col2" >0.55</td>
      <td id="T_2dd4b_row18_col3" class="data row18 col3" >0.00</td>
      <td id="T_2dd4b_row18_col4" class="data row18 col4" >1.00</td>
      <td id="T_2dd4b_row18_col5" class="data row18 col5" >1.00</td>
      <td id="T_2dd4b_row18_col6" class="data row18 col6" >2.00</td>
      <td id="T_2dd4b_row18_col7" class="data row18 col7" >2.00</td>
      <td id="T_2dd4b_row18_col8" class="data row18 col8" >3.00</td>
      <td id="T_2dd4b_row18_col9" class="data row18 col9" >3.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row19" class="row_heading level0 row19" >v_Half_Bath</th>
      <td id="T_2dd4b_row19_col0" class="data row19 col0" >1,941.00</td>
      <td id="T_2dd4b_row19_col1" class="data row19 col1" >0.38</td>
      <td id="T_2dd4b_row19_col2" class="data row19 col2" >0.50</td>
      <td id="T_2dd4b_row19_col3" class="data row19 col3" >0.00</td>
      <td id="T_2dd4b_row19_col4" class="data row19 col4" >0.00</td>
      <td id="T_2dd4b_row19_col5" class="data row19 col5" >0.00</td>
      <td id="T_2dd4b_row19_col6" class="data row19 col6" >0.00</td>
      <td id="T_2dd4b_row19_col7" class="data row19 col7" >1.00</td>
      <td id="T_2dd4b_row19_col8" class="data row19 col8" >1.00</td>
      <td id="T_2dd4b_row19_col9" class="data row19 col9" >2.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row20" class="row_heading level0 row20" >v_Bedroom_AbvGr</th>
      <td id="T_2dd4b_row20_col0" class="data row20 col0" >1,941.00</td>
      <td id="T_2dd4b_row20_col1" class="data row20 col1" >2.87</td>
      <td id="T_2dd4b_row20_col2" class="data row20 col2" >0.83</td>
      <td id="T_2dd4b_row20_col3" class="data row20 col3" >0.00</td>
      <td id="T_2dd4b_row20_col4" class="data row20 col4" >1.00</td>
      <td id="T_2dd4b_row20_col5" class="data row20 col5" >2.00</td>
      <td id="T_2dd4b_row20_col6" class="data row20 col6" >3.00</td>
      <td id="T_2dd4b_row20_col7" class="data row20 col7" >4.00</td>
      <td id="T_2dd4b_row20_col8" class="data row20 col8" >5.00</td>
      <td id="T_2dd4b_row20_col9" class="data row20 col9" >8.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row21" class="row_heading level0 row21" >v_Kitchen_AbvGr</th>
      <td id="T_2dd4b_row21_col0" class="data row21 col0" >1,941.00</td>
      <td id="T_2dd4b_row21_col1" class="data row21 col1" >1.04</td>
      <td id="T_2dd4b_row21_col2" class="data row21 col2" >0.20</td>
      <td id="T_2dd4b_row21_col3" class="data row21 col3" >0.00</td>
      <td id="T_2dd4b_row21_col4" class="data row21 col4" >1.00</td>
      <td id="T_2dd4b_row21_col5" class="data row21 col5" >1.00</td>
      <td id="T_2dd4b_row21_col6" class="data row21 col6" >1.00</td>
      <td id="T_2dd4b_row21_col7" class="data row21 col7" >1.00</td>
      <td id="T_2dd4b_row21_col8" class="data row21 col8" >2.00</td>
      <td id="T_2dd4b_row21_col9" class="data row21 col9" >2.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row22" class="row_heading level0 row22" >v_TotRms_AbvGrd</th>
      <td id="T_2dd4b_row22_col0" class="data row22 col0" >1,941.00</td>
      <td id="T_2dd4b_row22_col1" class="data row22 col1" >6.47</td>
      <td id="T_2dd4b_row22_col2" class="data row22 col2" >1.58</td>
      <td id="T_2dd4b_row22_col3" class="data row22 col3" >2.00</td>
      <td id="T_2dd4b_row22_col4" class="data row22 col4" >4.00</td>
      <td id="T_2dd4b_row22_col5" class="data row22 col5" >4.00</td>
      <td id="T_2dd4b_row22_col6" class="data row22 col6" >6.00</td>
      <td id="T_2dd4b_row22_col7" class="data row22 col7" >9.00</td>
      <td id="T_2dd4b_row22_col8" class="data row22 col8" >11.00</td>
      <td id="T_2dd4b_row22_col9" class="data row22 col9" >15.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row23" class="row_heading level0 row23" >v_Fireplaces</th>
      <td id="T_2dd4b_row23_col0" class="data row23 col0" >1,941.00</td>
      <td id="T_2dd4b_row23_col1" class="data row23 col1" >0.60</td>
      <td id="T_2dd4b_row23_col2" class="data row23 col2" >0.64</td>
      <td id="T_2dd4b_row23_col3" class="data row23 col3" >0.00</td>
      <td id="T_2dd4b_row23_col4" class="data row23 col4" >0.00</td>
      <td id="T_2dd4b_row23_col5" class="data row23 col5" >0.00</td>
      <td id="T_2dd4b_row23_col6" class="data row23 col6" >1.00</td>
      <td id="T_2dd4b_row23_col7" class="data row23 col7" >2.00</td>
      <td id="T_2dd4b_row23_col8" class="data row23 col8" >2.00</td>
      <td id="T_2dd4b_row23_col9" class="data row23 col9" >4.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row24" class="row_heading level0 row24" >v_Garage_Yr_Blt</th>
      <td id="T_2dd4b_row24_col0" class="data row24 col0" >1,834.00</td>
      <td id="T_2dd4b_row24_col1" class="data row24 col1" >1,978.19</td>
      <td id="T_2dd4b_row24_col2" class="data row24 col2" >25.73</td>
      <td id="T_2dd4b_row24_col3" class="data row24 col3" >1,895.00</td>
      <td id="T_2dd4b_row24_col4" class="data row24 col4" >1,916.00</td>
      <td id="T_2dd4b_row24_col5" class="data row24 col5" >1,928.65</td>
      <td id="T_2dd4b_row24_col6" class="data row24 col6" >1,980.00</td>
      <td id="T_2dd4b_row24_col7" class="data row24 col7" >2,007.00</td>
      <td id="T_2dd4b_row24_col8" class="data row24 col8" >2,008.00</td>
      <td id="T_2dd4b_row24_col9" class="data row24 col9" >2,207.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row25" class="row_heading level0 row25" >v_Garage_Cars</th>
      <td id="T_2dd4b_row25_col0" class="data row25 col0" >1,940.00</td>
      <td id="T_2dd4b_row25_col1" class="data row25 col1" >1.77</td>
      <td id="T_2dd4b_row25_col2" class="data row25 col2" >0.76</td>
      <td id="T_2dd4b_row25_col3" class="data row25 col3" >0.00</td>
      <td id="T_2dd4b_row25_col4" class="data row25 col4" >0.00</td>
      <td id="T_2dd4b_row25_col5" class="data row25 col5" >0.00</td>
      <td id="T_2dd4b_row25_col6" class="data row25 col6" >2.00</td>
      <td id="T_2dd4b_row25_col7" class="data row25 col7" >3.00</td>
      <td id="T_2dd4b_row25_col8" class="data row25 col8" >3.00</td>
      <td id="T_2dd4b_row25_col9" class="data row25 col9" >4.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row26" class="row_heading level0 row26" >v_Garage_Area</th>
      <td id="T_2dd4b_row26_col0" class="data row26 col0" >1,940.00</td>
      <td id="T_2dd4b_row26_col1" class="data row26 col1" >472.77</td>
      <td id="T_2dd4b_row26_col2" class="data row26 col2" >217.09</td>
      <td id="T_2dd4b_row26_col3" class="data row26 col3" >0.00</td>
      <td id="T_2dd4b_row26_col4" class="data row26 col4" >0.00</td>
      <td id="T_2dd4b_row26_col5" class="data row26 col5" >0.00</td>
      <td id="T_2dd4b_row26_col6" class="data row26 col6" >478.00</td>
      <td id="T_2dd4b_row26_col7" class="data row26 col7" >859.25</td>
      <td id="T_2dd4b_row26_col8" class="data row26 col8" >1,040.61</td>
      <td id="T_2dd4b_row26_col9" class="data row26 col9" >1,488.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row27" class="row_heading level0 row27" >v_Wood_Deck_SF</th>
      <td id="T_2dd4b_row27_col0" class="data row27 col0" >1,941.00</td>
      <td id="T_2dd4b_row27_col1" class="data row27 col1" >92.46</td>
      <td id="T_2dd4b_row27_col2" class="data row27 col2" >127.02</td>
      <td id="T_2dd4b_row27_col3" class="data row27 col3" >0.00</td>
      <td id="T_2dd4b_row27_col4" class="data row27 col4" >0.00</td>
      <td id="T_2dd4b_row27_col5" class="data row27 col5" >0.00</td>
      <td id="T_2dd4b_row27_col6" class="data row27 col6" >0.00</td>
      <td id="T_2dd4b_row27_col7" class="data row27 col7" >320.00</td>
      <td id="T_2dd4b_row27_col8" class="data row27 col8" >515.80</td>
      <td id="T_2dd4b_row27_col9" class="data row27 col9" >1,424.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row28" class="row_heading level0 row28" >v_Open_Porch_SF</th>
      <td id="T_2dd4b_row28_col0" class="data row28 col0" >1,941.00</td>
      <td id="T_2dd4b_row28_col1" class="data row28 col1" >49.16</td>
      <td id="T_2dd4b_row28_col2" class="data row28 col2" >70.30</td>
      <td id="T_2dd4b_row28_col3" class="data row28 col3" >0.00</td>
      <td id="T_2dd4b_row28_col4" class="data row28 col4" >0.00</td>
      <td id="T_2dd4b_row28_col5" class="data row28 col5" >0.00</td>
      <td id="T_2dd4b_row28_col6" class="data row28 col6" >28.00</td>
      <td id="T_2dd4b_row28_col7" class="data row28 col7" >189.00</td>
      <td id="T_2dd4b_row28_col8" class="data row28 col8" >296.20</td>
      <td id="T_2dd4b_row28_col9" class="data row28 col9" >742.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row29" class="row_heading level0 row29" >v_Enclosed_Porch</th>
      <td id="T_2dd4b_row29_col0" class="data row29 col0" >1,941.00</td>
      <td id="T_2dd4b_row29_col1" class="data row29 col1" >22.95</td>
      <td id="T_2dd4b_row29_col2" class="data row29 col2" >65.25</td>
      <td id="T_2dd4b_row29_col3" class="data row29 col3" >0.00</td>
      <td id="T_2dd4b_row29_col4" class="data row29 col4" >0.00</td>
      <td id="T_2dd4b_row29_col5" class="data row29 col5" >0.00</td>
      <td id="T_2dd4b_row29_col6" class="data row29 col6" >0.00</td>
      <td id="T_2dd4b_row29_col7" class="data row29 col7" >180.00</td>
      <td id="T_2dd4b_row29_col8" class="data row29 col8" >262.00</td>
      <td id="T_2dd4b_row29_col9" class="data row29 col9" >1,012.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row30" class="row_heading level0 row30" >v_3Ssn_Porch</th>
      <td id="T_2dd4b_row30_col0" class="data row30 col0" >1,941.00</td>
      <td id="T_2dd4b_row30_col1" class="data row30 col1" >2.25</td>
      <td id="T_2dd4b_row30_col2" class="data row30 col2" >22.42</td>
      <td id="T_2dd4b_row30_col3" class="data row30 col3" >0.00</td>
      <td id="T_2dd4b_row30_col4" class="data row30 col4" >0.00</td>
      <td id="T_2dd4b_row30_col5" class="data row30 col5" >0.00</td>
      <td id="T_2dd4b_row30_col6" class="data row30 col6" >0.00</td>
      <td id="T_2dd4b_row30_col7" class="data row30 col7" >0.00</td>
      <td id="T_2dd4b_row30_col8" class="data row30 col8" >110.40</td>
      <td id="T_2dd4b_row30_col9" class="data row30 col9" >407.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row31" class="row_heading level0 row31" >v_Screen_Porch</th>
      <td id="T_2dd4b_row31_col0" class="data row31 col0" >1,941.00</td>
      <td id="T_2dd4b_row31_col1" class="data row31 col1" >16.25</td>
      <td id="T_2dd4b_row31_col2" class="data row31 col2" >56.75</td>
      <td id="T_2dd4b_row31_col3" class="data row31 col3" >0.00</td>
      <td id="T_2dd4b_row31_col4" class="data row31 col4" >0.00</td>
      <td id="T_2dd4b_row31_col5" class="data row31 col5" >0.00</td>
      <td id="T_2dd4b_row31_col6" class="data row31 col6" >0.00</td>
      <td id="T_2dd4b_row31_col7" class="data row31 col7" >162.00</td>
      <td id="T_2dd4b_row31_col8" class="data row31 col8" >263.60</td>
      <td id="T_2dd4b_row31_col9" class="data row31 col9" >576.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row32" class="row_heading level0 row32" >v_Pool_Area</th>
      <td id="T_2dd4b_row32_col0" class="data row32 col0" >1,941.00</td>
      <td id="T_2dd4b_row32_col1" class="data row32 col1" >3.39</td>
      <td id="T_2dd4b_row32_col2" class="data row32 col2" >43.70</td>
      <td id="T_2dd4b_row32_col3" class="data row32 col3" >0.00</td>
      <td id="T_2dd4b_row32_col4" class="data row32 col4" >0.00</td>
      <td id="T_2dd4b_row32_col5" class="data row32 col5" >0.00</td>
      <td id="T_2dd4b_row32_col6" class="data row32 col6" >0.00</td>
      <td id="T_2dd4b_row32_col7" class="data row32 col7" >0.00</td>
      <td id="T_2dd4b_row32_col8" class="data row32 col8" >0.00</td>
      <td id="T_2dd4b_row32_col9" class="data row32 col9" >800.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row33" class="row_heading level0 row33" >v_Misc_Val</th>
      <td id="T_2dd4b_row33_col0" class="data row33 col0" >1,941.00</td>
      <td id="T_2dd4b_row33_col1" class="data row33 col1" >52.55</td>
      <td id="T_2dd4b_row33_col2" class="data row33 col2" >616.06</td>
      <td id="T_2dd4b_row33_col3" class="data row33 col3" >0.00</td>
      <td id="T_2dd4b_row33_col4" class="data row33 col4" >0.00</td>
      <td id="T_2dd4b_row33_col5" class="data row33 col5" >0.00</td>
      <td id="T_2dd4b_row33_col6" class="data row33 col6" >0.00</td>
      <td id="T_2dd4b_row33_col7" class="data row33 col7" >0.00</td>
      <td id="T_2dd4b_row33_col8" class="data row33 col8" >900.00</td>
      <td id="T_2dd4b_row33_col9" class="data row33 col9" >17,000.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row34" class="row_heading level0 row34" >v_Mo_Sold</th>
      <td id="T_2dd4b_row34_col0" class="data row34 col0" >1,941.00</td>
      <td id="T_2dd4b_row34_col1" class="data row34 col1" >6.43</td>
      <td id="T_2dd4b_row34_col2" class="data row34 col2" >2.75</td>
      <td id="T_2dd4b_row34_col3" class="data row34 col3" >1.00</td>
      <td id="T_2dd4b_row34_col4" class="data row34 col4" >1.00</td>
      <td id="T_2dd4b_row34_col5" class="data row34 col5" >2.00</td>
      <td id="T_2dd4b_row34_col6" class="data row34 col6" >6.00</td>
      <td id="T_2dd4b_row34_col7" class="data row34 col7" >11.00</td>
      <td id="T_2dd4b_row34_col8" class="data row34 col8" >12.00</td>
      <td id="T_2dd4b_row34_col9" class="data row34 col9" >12.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row35" class="row_heading level0 row35" >v_Yr_Sold</th>
      <td id="T_2dd4b_row35_col0" class="data row35 col0" >1,941.00</td>
      <td id="T_2dd4b_row35_col1" class="data row35 col1" >2,007.00</td>
      <td id="T_2dd4b_row35_col2" class="data row35 col2" >0.80</td>
      <td id="T_2dd4b_row35_col3" class="data row35 col3" >2,006.00</td>
      <td id="T_2dd4b_row35_col4" class="data row35 col4" >2,006.00</td>
      <td id="T_2dd4b_row35_col5" class="data row35 col5" >2,006.00</td>
      <td id="T_2dd4b_row35_col6" class="data row35 col6" >2,007.00</td>
      <td id="T_2dd4b_row35_col7" class="data row35 col7" >2,008.00</td>
      <td id="T_2dd4b_row35_col8" class="data row35 col8" >2,008.00</td>
      <td id="T_2dd4b_row35_col9" class="data row35 col9" >2,008.00</td>
    </tr>
    <tr>
      <th id="T_2dd4b_level0_row36" class="row_heading level0 row36" >v_SalePrice</th>
      <td id="T_2dd4b_row36_col0" class="data row36 col0" >1,941.00</td>
      <td id="T_2dd4b_row36_col1" class="data row36 col1" >182,033.24</td>
      <td id="T_2dd4b_row36_col2" class="data row36 col2" >80,407.10</td>
      <td id="T_2dd4b_row36_col3" class="data row36 col3" >13,100.00</td>
      <td id="T_2dd4b_row36_col4" class="data row36 col4" >64,700.00</td>
      <td id="T_2dd4b_row36_col5" class="data row36 col5" >89,500.00</td>
      <td id="T_2dd4b_row36_col6" class="data row36 col6" >161,900.00</td>
      <td id="T_2dd4b_row36_col7" class="data row36 col7" >339,750.00</td>
      <td id="T_2dd4b_row36_col8" class="data row36 col8" >453,000.00</td>
      <td id="T_2dd4b_row36_col9" class="data row36 col9" >755,000.00</td>
    </tr>
  </tbody>
</table>





```python
# % of Missing variables

# Caveat: a variable like v_Pool_QC with "missing" value just means no pool, so no data doesn't necessarily mean missing.

(
    ( # these lines do the calculation - what % of missing values are there for each var
        housing.isna()      # ccm.isna() TURNS every obs/variable = 1 when its missing and 0 else
       .sum(axis=0)     # count the number of na for each variable (now data is 1 obs per column = # missing)
        /len(housing)       # convert # missing to % missing 
        *100            # report as percentage
    ) 
    # you can stop here and report this...
    # but I wanted to format it a bit...
    .sort_values(ascending=False)[:13]
    .to_frame(name='% missing or NA') # the next line only works on a frame, and because pandas sees only 1 variable at this pt
    .style.format("{:.1f}")     # in the code, it calls this a "series" type object, so convert it to dataframe type object
)
```




<style type="text/css">
</style>
<table id="T_3f0cd_">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" >% missing or NA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_3f0cd_level0_row0" class="row_heading level0 row0" >v_Pool_QC</th>
      <td id="T_3f0cd_row0_col0" class="data row0 col0" >99.3</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row1" class="row_heading level0 row1" >v_Misc_Feature</th>
      <td id="T_3f0cd_row1_col0" class="data row1 col0" >96.8</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row2" class="row_heading level0 row2" >v_Alley</th>
      <td id="T_3f0cd_row2_col0" class="data row2 col0" >93.0</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row3" class="row_heading level0 row3" >v_Fence</th>
      <td id="T_3f0cd_row3_col0" class="data row3 col0" >81.2</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row4" class="row_heading level0 row4" >v_Fireplace_Qu</th>
      <td id="T_3f0cd_row4_col0" class="data row4 col0" >48.4</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row5" class="row_heading level0 row5" >v_Lot_Frontage</th>
      <td id="T_3f0cd_row5_col0" class="data row5 col0" >16.5</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row6" class="row_heading level0 row6" >v_Garage_Cond</th>
      <td id="T_3f0cd_row6_col0" class="data row6 col0" >5.5</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row7" class="row_heading level0 row7" >v_Garage_Finish</th>
      <td id="T_3f0cd_row7_col0" class="data row7 col0" >5.5</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row8" class="row_heading level0 row8" >v_Garage_Yr_Blt</th>
      <td id="T_3f0cd_row8_col0" class="data row8 col0" >5.5</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row9" class="row_heading level0 row9" >v_Garage_Qual</th>
      <td id="T_3f0cd_row9_col0" class="data row9 col0" >5.5</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row10" class="row_heading level0 row10" >v_Garage_Type</th>
      <td id="T_3f0cd_row10_col0" class="data row10 col0" >5.4</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row11" class="row_heading level0 row11" >v_Bsmt_Exposure</th>
      <td id="T_3f0cd_row11_col0" class="data row11 col0" >2.7</td>
    </tr>
    <tr>
      <th id="T_3f0cd_level0_row12" class="row_heading level0 row12" >v_Bsmt_Qual</th>
      <td id="T_3f0cd_row12_col0" class="data row12 col0" >2.6</td>
    </tr>
  </tbody>
</table>





```python
# dont plot identifying type info or categorical vars
import seaborn as sns
import numpy as np
import matplotlib.pyplot as plt
corr = housing.drop(columns=['v_MS_SubClass','v_MS_Zoning','v_Street','v_Alley','v_Lot_Shape', 'v_Land_Contour', 'v_Utilities', 'v_Lot_Config', 'v_Land_Slope', 'v_Neighborhood', 'v_Condition_1', 'v_Condition_2', 'v_Bldg_Type', 'v_House_Style', 'v_Roof_Style', 'v_Roof_Matl', 'v_Exterior_1st', 'v_Exterior_2nd', 'v_Mas_Vnr_Type', 'v_Exter_Qual', 'v_Exter_Cond', 'v_Foundation', 'v_Bsmt_Qual', 'v_Bsmt_Cond', 'v_Bsmt_Exposure', 'v_BsmtFin_Type_1', 'v_Heating', 'v_Heating_QC', 'v_Central_Air', 'v_Electrical', 'v_Kitchen_Qual', 'v_Functional', 'v_Fireplace_Qu', 'v_Garage_Type', 'v_Garage_Finish', 'v_Garage_Qual', 'v_Garage_Cond', 'v_Paved_Drive', 'v_Pool_QC', 'v_Fence', 'v_Misc_Feature', 'v_Sale_Type', 'v_Sale_Condition']).corr()

fig, ax = plt.subplots(figsize=(9,9)) # make a big space for the figure
ax = sns.heatmap(corr,
                 # cmap for the colors, 
                 center=0,square=True,
                 cmap=sns.diverging_palette(230, 20, as_cmap=True),
                 # mask to hide the upper diag (redundant)
                 mask=np.triu(np.ones_like(corr, dtype=bool)),
                 # shrink the heat legend
                 cbar_kws={"shrink": .5},
                 #optional: vmax and vmin will "cap" the color range
                )

# example of strong correlation is between v_SalePrice and v_Gr_Liv_Area
```


    
![png](output_6_0.png)
    



```python
sns.regplot(x="v_Lot_Area", y="v_SalePrice", data=housing, scatter_kws={'s':5}, color='blue')

#positive relationship
```




    <AxesSubplot:xlabel='v_Lot_Area', ylabel='v_SalePrice'>




    
![png](output_7_1.png)
    



```python
sns.regplot(x="v_Total_Bsmt_SF", y="v_SalePrice", data=housing, scatter_kws={'s':5}, color='green')

#positive relationship
```




    <AxesSubplot:xlabel='v_Total_Bsmt_SF', ylabel='v_SalePrice'>




    
![png](output_8_1.png)
    



```python
sns.regplot(x="v_Gr_Liv_Area", y="v_SalePrice", data=housing, scatter_kws={'s':5}, color='purple')

#strong positive linear relationship (strong confirmed by heatmap)
```




    <AxesSubplot:xlabel='v_Gr_Liv_Area', ylabel='v_SalePrice'>




    
![png](output_9_1.png)
    



```python
sns.boxplot(y=housing['v_Overall_Qual'])

#There's an outlier on the lower end of v_Overall_qual
```




    <AxesSubplot:ylabel='v_Overall_Qual'>




    
![png](output_10_1.png)
    



```python
sns.boxplot(y=housing['v_Overall_Cond'])

#There are several outliers both on the low and high ends of v_Overall_Cond
```




    <AxesSubplot:ylabel='v_Overall_Cond'>




    
![png](output_11_1.png)
    



```python
ax = sns.boxplot(x='v_Yr_Sold', y='v_SalePrice', data=housing)

#numerous outliers on the upper end in each of the 3 years
```


    
![png](output_12_0.png)
    


## Part 2: Running Regressions

**Run these regressions on the RAW data, even if you found data issues that you think should be addressed.**

_Insert cells as needed below to run these regressions. Note that $i$ is indexing a given house, and $t$ indexes the year of sale._ 

1. $\text{Sale Price}_{i,t} = \alpha + \beta_1 * \text{v_Lot_Area}$
1. $\text{Sale Price}_{i,t} = \alpha + \beta_1 * log(\text{v_Lot_Area})$
1. $log(\text{Sale Price}_{i,t}) = \alpha + \beta_1 * \text{v_Lot_Area}$
1. $log(\text{Sale Price}_{i,t}) = \alpha + \beta_1 * log(\text{v_Lot_Area})$
1. $log(\text{Sale Price}_{i,t}) = \alpha + \beta_1 * \text{v_Yr_Sold}$
1. $log(\text{Sale Price}_{i,t}) = \alpha + \beta_1 * (\text{v_Yr_Sold==2007})+ \beta_2 * (\text{v_Yr_Sold==2008})$
1. Choose your own adventure: Pick any five variables from the dataset that you think will generate good R2. Use them in a regression of $log(\text{Sale Price}_{i,t})$ 
    - Tip: You can transform/create these five variables however you want, even if it creates extra variables. For example: I'd count Model 6 above as only using one variable: `v_Yr_Sold`.
    - I got an R2 of 0.877 with just "5" variables. How close can you get? I won't be shocked if someone beats that!
    

**Bonus formatting trick:** Instead of reporting all regressions separately, report all seven regressions in a _single_ table using `summary_col`.



```python
from statsmodels.formula.api import ols as sm_ols
from statsmodels.iolib.summary2 import summary_col # nicer tables
```


```python
housing = housing.assign(l_vLotArea=np.log(housing['v_Lot_Area']),
                         l_SalePrice=np.log(housing['v_SalePrice']),
                        OverallTotal= housing['v_Overall_Qual']+ housing['v_Overall_Cond'])
```


```python
reg_1 = sm_ols ('v_SalePrice ~ v_Lot_Area', data = housing).fit()

reg_2 = sm_ols ('v_SalePrice ~ l_vLotArea', data = housing).fit()
                
reg_3 = sm_ols('l_SalePrice ~ v_Lot_Area', data = housing).fit()
                
reg_4 = sm_ols('l_SalePrice ~ l_vLotArea', data = housing).fit()
                
reg_5 = sm_ols('l_SalePrice ~ v_Yr_Sold', data = housing).fit()
                
reg_6 = sm_ols('l_SalePrice ~ C(v_Yr_Sold==2007) + C(v_Yr_Sold==2008)', data = housing).fit()
                
reg_7 = sm_ols('l_SalePrice ~ C(OverallTotal==10) + v_1st_Flr_SF + v_2nd_Flr_SF + v_Garage_Area + v_Year_Built', data = housing).fit()
```


```python
# now I'll format an output table
# I'd like to include extra info in the table (not just coefficients)
info_dict={'R-squared' : lambda x: f"{x.rsquared:.5f}",
           'Adj R-squared' : lambda x: f"{x.rsquared_adj:.5f}",
           'No. observations' : lambda x: f"{int(x.nobs):d}"}

# This summary col function combines a bunch of regressions into one nice table
print(summary_col(results=[reg_1,reg_2,reg_3, reg_4, reg_5, reg_6, reg_7], # list the result obj here
                  float_format='%0.5f',
                  stars = True, # stars are easy way to see if anything is statistically significant
                  model_names=['reg_1','reg_2','reg_3','reg_4','reg_5','reg_6', 'reg_7'],
                  info_dict=info_dict,
                  regressor_order=[ 'Intercept','v_Lot_Area', 'l_vLotArea', 'v_Yr_Sold', 'C(v_Yr_Sold==2007', 'C(v_Yr_Sold==2008']
                  )
     )
```

    
    ========================================================================================================================
                                       reg_1           reg_2          reg_3      reg_4      reg_5       reg_6       reg_7   
    ------------------------------------------------------------------------------------------------------------------------
    Intercept                     154789.55021*** -327915.80232*** 11.89407*** 9.40505*** 22.29321   12.02287*** 2.03452*** 
                                  (2911.59058)    (30221.34714)    (0.01463)   (0.15108)  (22.93682) (0.01614)   (0.34196)  
    v_Lot_Area                    2.64894***                       0.00001***                                               
                                  (0.22525)                        (0.00000)                                                
    l_vLotArea                                    56028.16996***               0.28826***                                   
                                                  (3315.13919)                 (0.01657)                                    
    v_Yr_Sold                                                                             -0.00511                          
                                                                                          (0.01143)                         
    C(OverallTotal == 10)[T.True]                                                                                -0.09135***
                                                                                                                 (0.01449)  
    C(v_Yr_Sold == 2007)[T.True]                                                                     0.02559                
                                                                                                     (0.02225)              
    C(v_Yr_Sold == 2008)[T.True]                                                                     -0.01028               
                                                                                                     (0.02285)              
    v_1st_Flr_SF                                                                                                 0.00048*** 
                                                                                                                 (0.00001)  
    v_2nd_Flr_SF                                                                                                 0.00034*** 
                                                                                                                 (0.00001)  
    v_Garage_Area                                                                                                0.00035*** 
                                                                                                                 (0.00003)  
    v_Year_Built                                                                                                 0.00465*** 
                                                                                                                 (0.00018)  
    R-squared                     0.06658         0.12840          0.06459     0.13497    0.00010    0.00144     0.74050    
    R-squared Adj.                0.06610         0.12795          0.06411     0.13453    -0.00041   0.00041     0.73983    
    R-squared                     0.06658         0.12840          0.06459     0.13497    0.00010    0.00144     0.74050    
    Adj R-squared                 0.06610         0.12795          0.06411     0.13453    -0.00041   0.00041     0.73983    
    No. observations              1941            1941             1941        1941       1941       1941        1940       
    ========================================================================================================================
    Standard errors in parentheses.
    * p<.1, ** p<.05, ***p<.01
    

## Part 3: Regression interpretation

_Insert cells as needed below to answer these questions. Note that $i$ is indexing a given house, and $t$ indexes the year of sale._ 

1. If you didn't use the `summary_col` trick, list $\beta_1$ for Models 1-6 to make it easier on your graders.
1. Interpret $\beta_1$ in Model 2. 
1. Interpret $\beta_1$ in Model 3. 
    - HINT: You might need to print out more decimal places. Show at least 2 non-zero digits. 
1. Of models 1-4, which do you think best explains the data and why?
1. Interpret $\beta_1$ In Model 5
1. Interpret $\alpha$ in Model 6
1. Interpret $\beta_1$ in Model 6
1. Why is the R2 of Model 6 higher than the R2 of Model 5?
1. What variables did you include in Model 7?
1. What is the R2 of your Model 7?
1. Speculate (not graded): Could you use the specification of Model 6 in a predictive regression? 
1. Speculate (not graded): Could you use the specification of Model 5 in a predictive regression? 


1.) $\beta_1$ for Models 1-6:

    - Model 1: 2.64894
    - Model 2: 56028.16996
    - Model 3: 0.00001
    - Model 4: 0.28826
    - Model 5: -0.00511
    - Model 6: 0.02559

2.) Interpret $\beta_1$ in Model 2. ($\beta_1$/100)
- A 1% increase in lot size square footage is associated with sales prices that are $560.28 higher, holding all else constant.

3.) Interpret $\beta_1$ in Model 3. (about 100∗$\beta_1$%)
- A 1 square foot increase in lot size square footage is associated with a 0.001% increase in sales price, holding all else constant.

4.) Of models 1-4, which do you think best explains the data and why?
- Model 4 best explains the data because it has the highest R2 and adjusted R2.

5.) Interpret $\beta_1$ In Model 5 ((about 100∗$\beta_1$%)
- A 1 unit increase in year is associated with a 0.511% decrease in sales price, holding all else constant.

6.) Interpret $\alpha$ in Model 6
- The intercept of 12.02 means that is the average log price in 2006.

7.) Interpret $\beta_1$ in Model 6
- In 2006 (year 0), the average log price is 12.02.

8.) Why is the R2 of Model 6 higher than the R2 of Model 5?
- Model 5 treats v_Yr_Sold as a continuous number, whereas Model 6 puts v_Yr_Sold inside of "C()", which tells statsmodels that the variable should be treated as a categorical variable even if it is a number.

9.) What variables did you include in Model 7?
- C(OverallTotal==10) -> OverallTotal = v_Overall_Qual + v_Overall_Cond
- v_1st_Flr_SF
- v_2nd_Flr_SF
- v_Garage_Area
- v_Year_Built

10.) What is the R2 of your Model 7?
- R2 = 0.74050

11.) Speculate (not graded): Could you use the specification of Model 6 in a predictive regression?
- No, because it is only focusing on data in 2007-2008 and does not have data in 2009.

12.) Speculate (not graded): Could you use the specification of Model 5 in a predictive regression?
- Yes, becuase it does not specify years in Model 5, unlike Model 6.
