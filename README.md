

```python
import pandas as pd
import numpy as np
```


```python
csv_path = "schools_complete.csv"
schools_complete = pd.read_csv(csv_path)
schools_complete.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
  </tbody>
</table>
</div>




```python
student_csv = "students_complete.csv"
student_complete = pd.read_csv(student_csv)
student_complete.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_schools = len(schools_complete)
```


```python
total_students = sum(schools_complete["size"])
```


```python
total_budget = sum(schools_complete["budget"])
```


```python
average_math_score = student_complete["math_score"].mean()
```


```python
average_reading_score = student_complete["reading_score"].mean()
```


```python
pass_math = student_complete.loc[student_complete["math_score"] >= 60]
percent_pass_math = len(pass_math)/total_students
```


```python
pass_reading = student_complete.loc[student_complete["reading_score"] >= 60]
percent_pass_reading = len(pass_reading)/total_students
```


```python
overall_passing_rate = (percent_pass_math + percent_pass_reading)/2
```


```python
district_summary_df = pd.DataFrame.from_records({"Total Schools in District": total_schools, "Number of Students in District": total_students, 
                 "Total District Budget": total_budget, "Average Math Scores for District": average_math_score, 
                 "Average Reading Score for District": average_reading_score, "Percent of Students Passing Math Testing": 
                  percent_pass_math, "Percent of Students Passing Reading Testing": percent_pass_reading, 
                  "Overall Pass Rate": overall_passing_rate}, index=[0])
district_summary = district_summary_df.iloc[:,::1]
district_summary_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Scores for District</th>
      <th>Average Reading Score for District</th>
      <th>Number of Students in District</th>
      <th>Overall Pass Rate</th>
      <th>Percent of Students Passing Math Testing</th>
      <th>Percent of Students Passing Reading Testing</th>
      <th>Total District Budget</th>
      <th>Total Schools in District</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>39170</td>
      <td>0.962229</td>
      <td>0.924457</td>
      <td>1.0</td>
      <td>24649428</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
student_complete_new = student_complete.rename(columns = {"name":"student_name", "school" : "name"})
student_complete_new.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>name</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```python
student_complete_new["reading_pass_fail"] = student_complete_new["reading_score"] >= 60
student_complete_new["math_pass_fail"] = student_complete_new["math_score"] >= 60
student_complete_new.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>name</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>reading_pass_fail</th>
      <th>math_pass_fail</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_test_totals = student_complete_new.pivot_table(index = ["name"], values = ["math_score", "reading_score"], 
                    aggfunc = np.sum) 
school_test_totals_df = school_test_totals.reset_index()
school_test_totals.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>math_score</th>
      <th>reading_score</th>
    </tr>
    <tr>
      <th>name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>383393</td>
      <td>403225</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>154329</td>
      <td>156027</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>226223</td>
      <td>239335</td>
    </tr>
  </tbody>
</table>
</div>




```python
schools_with_scores = pd.merge(schools_complete, school_test_totals_df, how = "outer", on = "name")
schools_with_scores.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>math_score</th>
      <th>reading_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>223528</td>
      <td>236810</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>226223</td>
      <td>239335</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>146796</td>
      <td>147441</td>
    </tr>
  </tbody>
</table>
</div>




```python
per_student_budget = schools_with_scores["budget"]/schools_with_scores["size"]
```


```python
average_math_school = schools_with_scores["math_score"]/schools_with_scores["size"]
```


```python
average_reading_school = schools_with_scores["reading_score"]/schools_with_scores["size"]
```


```python
school_pass_fail = student_complete_new.pivot_table(index = ["name"], values = ["reading_pass_fail" , "math_pass_fail"]) 
school_pass_fail_df = school_pass_fail.reset_index()
school_pass_fail_df["school_overall_pass"] =  (school_pass_fail_df["math_pass_fail"] + school_pass_fail_df["reading_pass_fail"])/2
```


```python
schools_with_scores["per_student_budget"] = per_student_budget
schools_with_scores["average_math_score"] = average_math_school
schools_with_scores["average_reading_score"] = average_reading_school
schools_with_scores.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>per_student_budget</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>223528</td>
      <td>236810</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>226223</td>
      <td>239335</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>146796</td>
      <td>147441</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_summary = pd.merge(schools_with_scores, school_pass_fail_df, how = "outer", on = "name")
school_summary.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>per_student_budget</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>223528</td>
      <td>236810</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>226223</td>
      <td>239335</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>146796</td>
      <td>147441</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_district_summary = school_summary.drop(["math_score", "reading_score"], axis = 1)
school_district_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>per_student_budget</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>0.895297</td>
      <td>1.0</td>
      <td>0.947649</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.893027</td>
      <td>1.0</td>
      <td>0.946513</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
schools_highest_overall = school_district_summary.nlargest(5, "school_overall_pass")
schools_highest_overall
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>per_student_budget</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
schools_lowest_overall = school_district_summary.nsmallest(5, "school_overall_pass")
schools_lowest_overall
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>per_student_budget</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_math_by_grade = student_complete_new.pivot_table(index = ["name"], values = ["math_score"], columns = "grade") 
school_math_by_grade = school_math_by_grade.reset_index()
school_math_by_grade
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>name</th>
      <th colspan="4" halign="left">math_score</th>
    </tr>
    <tr>
      <th>grade</th>
      <th></th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
      <td>76.403037</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
      <td>77.361345</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
      <td>82.044010</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
      <td>77.438495</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
      <td>83.787402</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
      <td>77.027251</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
      <td>77.187857</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
      <td>83.625455</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
      <td>76.859966</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
      <td>83.420755</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
      <td>83.590022</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
      <td>83.085578</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_reading_by_grade = student_complete_new.pivot_table(index = ["name"], values = ["reading_score"], 
                                                           columns = "grade") 
school_reading_by_grade = school_reading_by_grade.reset_index()
school_reading_by_grade
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>name</th>
      <th colspan="4" halign="left">reading_score</th>
    </tr>
    <tr>
      <th>grade</th>
      <th></th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
      <td>81.303155</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
      <td>83.676136</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
      <td>81.198598</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
      <td>80.632653</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
      <td>83.369193</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
      <td>80.866860</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
      <td>83.677165</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
      <td>81.290284</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
      <td>81.260714</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
      <td>83.807273</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
      <td>80.993127</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
      <td>84.122642</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
      <td>83.728850</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
      <td>83.939778</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
      <td>83.833333</td>
    </tr>
  </tbody>
</table>
</div>




```python
bins = [550, 600, 650, 700]
bin_names_spending = ["Low", "Medium", "High"]
school_summary["summary spending per student"] = pd.cut(school_summary["per_student_budget"], bins, labels = bin_names_spending)
school_summary_spending = school_summary.drop(["School ID","type", "size", "budget", "math_score", "reading_score", 
                                               "per_student_budget", "size by number of students"], axis=1)
school_summary_spending
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
      <th>summary spending per student</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
      <td>High</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Low</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
      <td>High</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Low</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Low</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>0.895297</td>
      <td>1.0</td>
      <td>0.947649</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Low</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Low</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.893027</td>
      <td>1.0</td>
      <td>0.946513</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
  </tbody>
</table>
</div>




```python
bins = [0, 1500, 3500, 5500]
bin_names_size = ["Small", "Medium", "Large"]
school_summary["size by number of students"] = pd.cut(school_summary["size"], bins, labels=bin_names_size)
school_summary_size = school_summary.drop(["School ID", "type", "size", "budget", "per_student_budget", "math_score",
                                          "reading_score", "summary spending per student"], axis=1)
school_summary_size
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
      <th>size by number of students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Small</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>0.895297</td>
      <td>1.0</td>
      <td>0.947649</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Small</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Small</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.893027</td>
      <td>1.0</td>
      <td>0.946513</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>Medium</td>
    </tr>
  </tbody>
</table>
</div>




```python
summary_chartered = school_summary[school_summary.type == "Charter"]
summary_chartered = summary_chartered.drop(["School ID", "size", "budget", "math_score", "reading_score", "per_student_budget"], axis = 1)
summary_chartered
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>type</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
      <th>summary spending per student</th>
      <th>size by number of students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Low</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Medium</td>
      <td>Small</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Low</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Low</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Low</td>
      <td>Small</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Medium</td>
      <td>Small</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Low</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>Medium</td>
      <td>Medium</td>
    </tr>
  </tbody>
</table>
</div>




```python
summary_district = school_summary[school_summary.type == "District"]
summary_district = summary_district.drop(["School ID", "size", "budget", "math_score", "reading_score", "per_student_budget"], axis = 1)
summary_district
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>type</th>
      <th>average_math_score</th>
      <th>average_reading_score</th>
      <th>math_pass_fail</th>
      <th>reading_pass_fail</th>
      <th>school_overall_pass</th>
      <th>summary spending per student</th>
      <th>size by number of students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.888584</td>
      <td>1.0</td>
      <td>0.944292</td>
      <td>High</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.884368</td>
      <td>1.0</td>
      <td>0.942184</td>
      <td>Medium</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>0.890831</td>
      <td>1.0</td>
      <td>0.945415</td>
      <td>High</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>0.895297</td>
      <td>1.0</td>
      <td>0.947649</td>
      <td>Medium</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.885471</td>
      <td>1.0</td>
      <td>0.942736</td>
      <td>Medium</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.891829</td>
      <td>1.0</td>
      <td>0.945915</td>
      <td>Medium</td>
      <td>Large</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.893027</td>
      <td>1.0</td>
      <td>0.946513</td>
      <td>Medium</td>
      <td>Medium</td>
    </tr>
  </tbody>
</table>
</div>


