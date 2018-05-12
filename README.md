

```python
import os
import csv
import pandas as pd
```


```python
schools_csv = os.path.join("schools_complete.csv")
students_csv = os.path.join("students_complete.csv")
```


```python
schools_df = pd.read_csv(schools_csv)
students_df = pd.read_csv(students_csv)
```


```python
schools_df.head()
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
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
students_df.head()
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
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_students = len(students_df["Student ID"])
print(total_students)
```

    39170



```python
total_schools = len(schools_df["School ID"])
print(total_schools)
```

    15



```python
total_budget = schools_df["budget"].sum()
print(total_budget)
```

    24649428



```python
avg_math_score = students_df["math_score"].mean()
print(avg_math_score)
```

    78.98537145774827



```python
avg_reading_score = students_df["reading_score"].mean()
print(avg_reading_score)
```

    81.87784018381414



```python
pass_math = students_df.loc[students_df["math_score"]>=60]
percent_pass_math = (len(pass_math["math_score"])/total_students)*100
print(percent_pass_math)
```

    92.4457492979321



```python
pass_reading = students_df.loc[students_df["reading_score"]>=60]
percent_pass_reading = (len(pass_reading["reading_score"])/total_students)*100
print(percent_pass_reading)
```

    100.0



```python
overall_pass = (percent_pass_math+percent_pass_reading)/2
print(overall_pass)
```

    96.22287464896604



```python
district_summary_df = pd.DataFrame({"Total Schools": [total_schools],
                          "Total Students": [total_students],
                          "Total Budget": [total_budget],
                          "Average Math Score": [avg_math_score],
                          "Average Reading Score": [avg_reading_score],
                          "Percent Passing Math": [percent_pass_math],
                           "Percent Passing Reading": [percent_pass_reading],
                           "Overall Passing Rate": [overall_pass]})
district_summary_df.head()
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
      <th>Total Budget</th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>96.222875</td>
      <td>92.445749</td>
      <td>100.0</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_df = students_df.groupby(["school"])
grouped_df.head()
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
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
    <tr>
      <th>2917</th>
      <td>2917</td>
      <td>Amy Jacobs</td>
      <td>F</td>
      <td>10th</td>
      <td>Figueroa High School</td>
      <td>85</td>
      <td>87</td>
    </tr>
    <tr>
      <th>2918</th>
      <td>2918</td>
      <td>Nathan Campbell</td>
      <td>M</td>
      <td>12th</td>
      <td>Figueroa High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
    <tr>
      <th>2919</th>
      <td>2919</td>
      <td>Randall Stewart</td>
      <td>M</td>
      <td>12th</td>
      <td>Figueroa High School</td>
      <td>67</td>
      <td>77</td>
    </tr>
    <tr>
      <th>2920</th>
      <td>2920</td>
      <td>Jennifer Brown</td>
      <td>F</td>
      <td>9th</td>
      <td>Figueroa High School</td>
      <td>97</td>
      <td>64</td>
    </tr>
    <tr>
      <th>2921</th>
      <td>2921</td>
      <td>Denise Lopez</td>
      <td>F</td>
      <td>10th</td>
      <td>Figueroa High School</td>
      <td>79</td>
      <td>64</td>
    </tr>
    <tr>
      <th>5866</th>
      <td>5866</td>
      <td>Jamie Montgomery</td>
      <td>F</td>
      <td>12th</td>
      <td>Shelton High School</td>
      <td>70</td>
      <td>91</td>
    </tr>
    <tr>
      <th>5867</th>
      <td>5867</td>
      <td>Shannon Phillips</td>
      <td>F</td>
      <td>10th</td>
      <td>Shelton High School</td>
      <td>84</td>
      <td>71</td>
    </tr>
    <tr>
      <th>5868</th>
      <td>5868</td>
      <td>Todd Barber</td>
      <td>M</td>
      <td>11th</td>
      <td>Shelton High School</td>
      <td>95</td>
      <td>99</td>
    </tr>
    <tr>
      <th>5869</th>
      <td>5869</td>
      <td>Desiree King</td>
      <td>F</td>
      <td>12th</td>
      <td>Shelton High School</td>
      <td>76</td>
      <td>95</td>
    </tr>
    <tr>
      <th>5870</th>
      <td>5870</td>
      <td>Melissa Roberts</td>
      <td>F</td>
      <td>10th</td>
      <td>Shelton High School</td>
      <td>71</td>
      <td>82</td>
    </tr>
    <tr>
      <th>7627</th>
      <td>7627</td>
      <td>Russell Davis</td>
      <td>M</td>
      <td>10th</td>
      <td>Hernandez High School</td>
      <td>70</td>
      <td>88</td>
    </tr>
    <tr>
      <th>7628</th>
      <td>7628</td>
      <td>Timothy Walker</td>
      <td>M</td>
      <td>12th</td>
      <td>Hernandez High School</td>
      <td>97</td>
      <td>93</td>
    </tr>
    <tr>
      <th>7629</th>
      <td>7629</td>
      <td>Katie Johnston</td>
      <td>F</td>
      <td>12th</td>
      <td>Hernandez High School</td>
      <td>83</td>
      <td>81</td>
    </tr>
    <tr>
      <th>7630</th>
      <td>7630</td>
      <td>Joann Oconnell</td>
      <td>F</td>
      <td>12th</td>
      <td>Hernandez High School</td>
      <td>77</td>
      <td>91</td>
    </tr>
    <tr>
      <th>7631</th>
      <td>7631</td>
      <td>Sarah Alexander</td>
      <td>F</td>
      <td>10th</td>
      <td>Hernandez High School</td>
      <td>84</td>
      <td>93</td>
    </tr>
    <tr>
      <th>12262</th>
      <td>12262</td>
      <td>Heather Wright</td>
      <td>F</td>
      <td>11th</td>
      <td>Griffin High School</td>
      <td>79</td>
      <td>68</td>
    </tr>
    <tr>
      <th>12263</th>
      <td>12263</td>
      <td>Elizabeth Goodwin</td>
      <td>F</td>
      <td>10th</td>
      <td>Griffin High School</td>
      <td>91</td>
      <td>81</td>
    </tr>
    <tr>
      <th>12264</th>
      <td>12264</td>
      <td>Michelle Wong</td>
      <td>F</td>
      <td>9th</td>
      <td>Griffin High School</td>
      <td>78</td>
      <td>89</td>
    </tr>
    <tr>
      <th>12265</th>
      <td>12265</td>
      <td>Scott Roth MD</td>
      <td>M</td>
      <td>11th</td>
      <td>Griffin High School</td>
      <td>91</td>
      <td>85</td>
    </tr>
    <tr>
      <th>12266</th>
      <td>12266</td>
      <td>Billy Wilson</td>
      <td>M</td>
      <td>12th</td>
      <td>Griffin High School</td>
      <td>76</td>
      <td>83</td>
    </tr>
    <tr>
      <th>13730</th>
      <td>13730</td>
      <td>Kelli Anderson</td>
      <td>F</td>
      <td>10th</td>
      <td>Wilson High School</td>
      <td>84</td>
      <td>71</td>
    </tr>
    <tr>
      <th>13731</th>
      <td>13731</td>
      <td>Russell Ramirez</td>
      <td>M</td>
      <td>10th</td>
      <td>Wilson High School</td>
      <td>72</td>
      <td>87</td>
    </tr>
    <tr>
      <th>13732</th>
      <td>13732</td>
      <td>Eric Butler</td>
      <td>M</td>
      <td>10th</td>
      <td>Wilson High School</td>
      <td>97</td>
      <td>82</td>
    </tr>
    <tr>
      <th>13733</th>
      <td>13733</td>
      <td>Warren Kerr</td>
      <td>M</td>
      <td>11th</td>
      <td>Wilson High School</td>
      <td>93</td>
      <td>68</td>
    </tr>
    <tr>
      <th>13734</th>
      <td>13734</td>
      <td>Gail Hall</td>
      <td>F</td>
      <td>9th</td>
      <td>Wilson High School</td>
      <td>79</td>
      <td>72</td>
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
    </tr>
    <tr>
      <th>23274</th>
      <td>23274</td>
      <td>Alec Davis</td>
      <td>M</td>
      <td>9th</td>
      <td>Pena High School</td>
      <td>91</td>
      <td>75</td>
    </tr>
    <tr>
      <th>23275</th>
      <td>23275</td>
      <td>Michael Meyer</td>
      <td>M</td>
      <td>10th</td>
      <td>Pena High School</td>
      <td>94</td>
      <td>76</td>
    </tr>
    <tr>
      <th>23276</th>
      <td>23276</td>
      <td>Donald Gutierrez</td>
      <td>M</td>
      <td>11th</td>
      <td>Pena High School</td>
      <td>98</td>
      <td>91</td>
    </tr>
    <tr>
      <th>23277</th>
      <td>23277</td>
      <td>Travis Chavez</td>
      <td>M</td>
      <td>11th</td>
      <td>Pena High School</td>
      <td>78</td>
      <td>71</td>
    </tr>
    <tr>
      <th>23278</th>
      <td>23278</td>
      <td>Sheena Ball</td>
      <td>F</td>
      <td>12th</td>
      <td>Pena High School</td>
      <td>87</td>
      <td>92</td>
    </tr>
    <tr>
      <th>24236</th>
      <td>24236</td>
      <td>Aaron Johnson</td>
      <td>M</td>
      <td>10th</td>
      <td>Wright High School</td>
      <td>89</td>
      <td>72</td>
    </tr>
    <tr>
      <th>24237</th>
      <td>24237</td>
      <td>Kimberly Hamilton</td>
      <td>F</td>
      <td>10th</td>
      <td>Wright High School</td>
      <td>84</td>
      <td>93</td>
    </tr>
    <tr>
      <th>24238</th>
      <td>24238</td>
      <td>Ashley Johns</td>
      <td>F</td>
      <td>10th</td>
      <td>Wright High School</td>
      <td>88</td>
      <td>88</td>
    </tr>
    <tr>
      <th>24239</th>
      <td>24239</td>
      <td>Stephanie Donovan</td>
      <td>F</td>
      <td>10th</td>
      <td>Wright High School</td>
      <td>75</td>
      <td>84</td>
    </tr>
    <tr>
      <th>24240</th>
      <td>24240</td>
      <td>Cynthia Guzman</td>
      <td>F</td>
      <td>11th</td>
      <td>Wright High School</td>
      <td>93</td>
      <td>82</td>
    </tr>
    <tr>
      <th>26036</th>
      <td>26036</td>
      <td>Sherry Jenkins</td>
      <td>F</td>
      <td>11th</td>
      <td>Rodriguez High School</td>
      <td>74</td>
      <td>81</td>
    </tr>
    <tr>
      <th>26037</th>
      <td>26037</td>
      <td>Kimberly Calderon</td>
      <td>F</td>
      <td>10th</td>
      <td>Rodriguez High School</td>
      <td>80</td>
      <td>86</td>
    </tr>
    <tr>
      <th>26038</th>
      <td>26038</td>
      <td>William Brady</td>
      <td>M</td>
      <td>11th</td>
      <td>Rodriguez High School</td>
      <td>97</td>
      <td>62</td>
    </tr>
    <tr>
      <th>26039</th>
      <td>26039</td>
      <td>Jacob Padilla</td>
      <td>M</td>
      <td>11th</td>
      <td>Rodriguez High School</td>
      <td>79</td>
      <td>73</td>
    </tr>
    <tr>
      <th>26040</th>
      <td>26040</td>
      <td>Paula Maldonado</td>
      <td>F</td>
      <td>10th</td>
      <td>Rodriguez High School</td>
      <td>96</td>
      <td>92</td>
    </tr>
    <tr>
      <th>30035</th>
      <td>30035</td>
      <td>Lisa Casey</td>
      <td>F</td>
      <td>12th</td>
      <td>Johnson High School</td>
      <td>87</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30036</th>
      <td>30036</td>
      <td>Jessica Lopez</td>
      <td>F</td>
      <td>9th</td>
      <td>Johnson High School</td>
      <td>98</td>
      <td>62</td>
    </tr>
    <tr>
      <th>30037</th>
      <td>30037</td>
      <td>Anna Wilkins</td>
      <td>F</td>
      <td>11th</td>
      <td>Johnson High School</td>
      <td>89</td>
      <td>77</td>
    </tr>
    <tr>
      <th>30038</th>
      <td>30038</td>
      <td>Andrew Smith</td>
      <td>M</td>
      <td>9th</td>
      <td>Johnson High School</td>
      <td>66</td>
      <td>85</td>
    </tr>
    <tr>
      <th>30039</th>
      <td>30039</td>
      <td>Robert Allison</td>
      <td>M</td>
      <td>11th</td>
      <td>Johnson High School</td>
      <td>63</td>
      <td>85</td>
    </tr>
    <tr>
      <th>34796</th>
      <td>34796</td>
      <td>Michael Mercado</td>
      <td>M</td>
      <td>9th</td>
      <td>Ford High School</td>
      <td>66</td>
      <td>94</td>
    </tr>
    <tr>
      <th>34797</th>
      <td>34797</td>
      <td>Stephen Wolf</td>
      <td>M</td>
      <td>11th</td>
      <td>Ford High School</td>
      <td>68</td>
      <td>63</td>
    </tr>
    <tr>
      <th>34798</th>
      <td>34798</td>
      <td>Bonnie Hughes</td>
      <td>F</td>
      <td>12th</td>
      <td>Ford High School</td>
      <td>73</td>
      <td>59</td>
    </tr>
    <tr>
      <th>34799</th>
      <td>34799</td>
      <td>Melissa Smith</td>
      <td>F</td>
      <td>11th</td>
      <td>Ford High School</td>
      <td>88</td>
      <td>58</td>
    </tr>
    <tr>
      <th>34800</th>
      <td>34800</td>
      <td>Brian Mitchell</td>
      <td>M</td>
      <td>10th</td>
      <td>Ford High School</td>
      <td>96</td>
      <td>55</td>
    </tr>
    <tr>
      <th>37535</th>
      <td>37535</td>
      <td>Norma Mata</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>76</td>
      <td>76</td>
    </tr>
    <tr>
      <th>37536</th>
      <td>37536</td>
      <td>Cody Miller</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>84</td>
      <td>82</td>
    </tr>
    <tr>
      <th>37537</th>
      <td>37537</td>
      <td>Erik Snyder</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>90</td>
    </tr>
    <tr>
      <th>37538</th>
      <td>37538</td>
      <td>Tanya Martinez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>71</td>
      <td>69</td>
    </tr>
    <tr>
      <th>37539</th>
      <td>37539</td>
      <td>Noah Erickson</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>86</td>
      <td>76</td>
    </tr>
  </tbody>
</table>
<p>75 rows × 7 columns</p>
</div>




```python
grouped_math_df = pd.DataFrame(grouped_df["math_score"].mean())
grouped_math_df = grouped_math_df.reset_index()
grouped_math_df
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
      <th>school</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_reading_df = grouped_df["reading_score"].mean()
grouped_reading_df = grouped_reading_df.reset_index()
grouped_reading_df
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
      <th>school</th>
      <th>reading_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
    </tr>
  </tbody>
</table>
</div>




```python
budget_per_student = schools_df["budget"]/schools_df["size"]
schools_df["Per Student Budget"] = budget_per_student
schools_df
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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
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
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
schools_df = schools_df.rename(columns={"name":"school"})
schools_df.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
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
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
merged_math = schools_df.merge(grouped_math_df,on="school")
merged_math.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>math_score</th>
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
    </tr>
  </tbody>
</table>
</div>




```python
merged = merged_math.merge(grouped_reading_df,on="school")
merged.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
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
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
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
    </tr>
  </tbody>
</table>
</div>




```python
new_merged = merged.sort_values("school")
second_merge = new_merged.reset_index()
final_merge = second_merge.drop(columns="index")
final_merge.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>math_score</th>
      <th>reading_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
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
    </tr>
  </tbody>
</table>
</div>




```python
pass_math_school = students_df.loc[students_df["math_score"]>=60]
second_pass_math_school = pass_math_school.groupby(["school"])
final_pass_math_school = second_pass_math_school["math_score"].count().reset_index()
```


```python
pass_read_school = students_df.loc[students_df["reading_score"]>=60]
second_pass_read_school = pass_read_school.groupby(["school"])
final_pass_read_school = second_pass_read_school["reading_score"].count().reset_index()
```


```python
percent_pass_math_school = pd.DataFrame((final_pass_math_school["math_score"]/final_merge["size"])*100)
final_merge["% Passing Math"] = percent_pass_math_school
```


```python
percent_pass_read_school = pd.DataFrame((final_pass_read_school["reading_score"]/final_merge["size"])*100)
final_merge["% Passing Reading"] = percent_pass_read_school
final_merge
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
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
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>89.083064</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>88.858416</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>89.182945</td>
      <td>100.0</td>
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
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>88.547137</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>100.000000</td>
      <td>100.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
overall_passing_school = (final_merge["% Passing Math"]+final_merge["% Passing Reading"])/2
final_merge["% Overall Passing Rate"] = overall_passing_school
final_merge.head()
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
      <td>94.764871</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
      <td>94.651333</td>
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
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
final_school_df = final_merge.rename(columns={"school":"School Name",
                                        "type":"School Type",
                                       "size":"Total Students",
                                        "budget":"Total School Budget",
                                        "math_score":"Average Math Score",
                                        "reading_score":"Average Reading Score",
                                        
                                        }).drop(columns="School ID")
final_school_df.head()
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
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
      <td>94.764871</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
      <td>94.651333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_schools = final_school_df.nlargest(5,"% Overall Passing Rate")
top_schools
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
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
bottom_schools = final_school_df.nsmallest(5,"% Overall Passing Rate")
bottom_schools
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
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>88.547137</td>
      <td>100.0</td>
      <td>94.273568</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>88.858416</td>
      <td>100.0</td>
      <td>94.429208</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>89.083064</td>
      <td>100.0</td>
      <td>94.541532</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>89.182945</td>
      <td>100.0</td>
      <td>94.591472</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_schools_math = pd.DataFrame(students_df.groupby(["school", "grade"])["math_score"].mean())
grouped_schools_math.head()
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
      <th></th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>school</th>
      <th>grade</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">Bailey High School</th>
      <th>10th</th>
      <td>76.996772</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>77.515588</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <th>10th</th>
      <td>83.154506</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_schools_reading = pd.DataFrame(students_df.groupby(["school", "grade"])["reading_score"].mean())
grouped_schools_reading.head()
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
      <th></th>
      <th>reading_score</th>
    </tr>
    <tr>
      <th>school</th>
      <th>grade</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">Bailey High School</th>
      <th>10th</th>
      <td>80.907183</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>80.945643</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>81.303155</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <th>10th</th>
      <td>84.253219</td>
    </tr>
  </tbody>
</table>
</div>




```python
final_school_df
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
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
      <td>94.764871</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
      <td>94.651333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>89.083064</td>
      <td>100.0</td>
      <td>94.541532</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>88.858416</td>
      <td>100.0</td>
      <td>94.429208</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>89.182945</td>
      <td>100.0</td>
      <td>94.591472</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>88.547137</td>
      <td>100.0</td>
      <td>94.273568</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
score_bins = [0, 585, 615, 645, 675]
budget_range_names = ["<$585","$585-615","$615-645","$645-675"]
grouped_budget = pd.cut(final_school_df["Per Student Budget"], score_bins, labels=budget_range_names)
grouped_budget
```




    0     $615-645
    1        <$585
    2     $615-645
    3     $615-645
    4     $615-645
    5     $645-675
    6        <$585
    7     $645-675
    8     $645-675
    9     $585-615
    10    $615-645
    11    $585-615
    12    $615-645
    13       <$585
    14       <$585
    Name: Per Student Budget, dtype: category
    Categories (4, object): [<$585 < $585-615 < $615-645 < $645-675]




```python
grouped_budget_df = grouped_budget.to_frame()
grouped_budget_df
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
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$615-645</td>
    </tr>
    <tr>
      <th>1</th>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$615-645</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$615-645</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$615-645</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$645-675</td>
    </tr>
    <tr>
      <th>6</th>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>7</th>
      <td>$645-675</td>
    </tr>
    <tr>
      <th>8</th>
      <td>$645-675</td>
    </tr>
    <tr>
      <th>9</th>
      <td>$585-615</td>
    </tr>
    <tr>
      <th>10</th>
      <td>$615-645</td>
    </tr>
    <tr>
      <th>11</th>
      <td>$585-615</td>
    </tr>
    <tr>
      <th>12</th>
      <td>$615-645</td>
    </tr>
    <tr>
      <th>13</th>
      <td>&lt;$585</td>
    </tr>
    <tr>
      <th>14</th>
      <td>&lt;$585</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_budget_df["Average Math Score"] = final_school_df["Average Math Score"]
grouped_budget_df["Average Reading Score"] = final_school_df["Average Reading Score"]
grouped_budget_df["% Passing Math"] = final_school_df["% Passing Math"]
grouped_budget_df["% Passing Reading"] = final_school_df["% Passing Reading"]
grouped_budget_df["% Overall Passing Rate"] = final_school_df["% Overall Passing Rate"]
grouped_budget_df
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
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$615-645</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
      <td>94.764871</td>
    </tr>
    <tr>
      <th>1</th>
      <td>&lt;$585</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$615-645</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$615-645</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
      <td>94.651333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$615-645</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$645-675</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>89.083064</td>
      <td>100.0</td>
      <td>94.541532</td>
    </tr>
    <tr>
      <th>6</th>
      <td>&lt;$585</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>$645-675</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>88.858416</td>
      <td>100.0</td>
      <td>94.429208</td>
    </tr>
    <tr>
      <th>8</th>
      <td>$645-675</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>89.182945</td>
      <td>100.0</td>
      <td>94.591472</td>
    </tr>
    <tr>
      <th>9</th>
      <td>$585-615</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>$615-645</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>88.547137</td>
      <td>100.0</td>
      <td>94.273568</td>
    </tr>
    <tr>
      <th>11</th>
      <td>$585-615</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>$615-645</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>&lt;$585</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>&lt;$585</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
new_grouped_budget = grouped_budget_df.groupby(["Per Student Budget"])
new_grouped_budget.mean()
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Per Student Budget</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.599686</td>
      <td>83.885211</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>79.079225</td>
      <td>81.891436</td>
      <td>92.636050</td>
      <td>100.0</td>
      <td>96.318025</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>76.997210</td>
      <td>81.027843</td>
      <td>89.041475</td>
      <td>100.0</td>
      <td>94.520737</td>
    </tr>
  </tbody>
</table>
</div>




```python
size_bins = [0, 1000, 2000, 5000]
size_names = ["Small (<1000)","Medium (1000-2000)","Large (2000-5000)"]
grouped_size = pd.cut(final_school_df["Total Students"], size_bins, labels=size_names)
grouped_size_df = grouped_size.to_frame()
grouped_size_df
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
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium (1000-2000)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Medium (1000-2000)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Small (&lt;1000)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Small (&lt;1000)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Medium (1000-2000)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Medium (1000-2000)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Large (2000-5000)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Medium (1000-2000)</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_size_df["Average Math Score"] = final_school_df["Average Math Score"]
grouped_size_df["Average Reading Score"] = final_school_df["Average Reading Score"]
grouped_size_df["% Passing Math"] = final_school_df["% Passing Math"]
grouped_size_df["% Passing Reading"] = final_school_df["% Passing Reading"]
grouped_size_df["% Overall Passing Rate"] = final_school_df["% Overall Passing Rate"]
grouped_size_df.head()
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
      <th>Total Students</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large (2000-5000)</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
      <td>94.764871</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium (1000-2000)</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Large (2000-5000)</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Large (2000-5000)</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
      <td>94.651333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Medium (1000-2000)</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
new_grouped_size = grouped_size_df.groupby(["Total Students"])
new_grouped_size.mean()
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Total Students</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>83.821598</td>
      <td>83.929843</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>83.374684</td>
      <td>83.864438</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Large (2000-5000)</th>
      <td>77.746417</td>
      <td>81.344493</td>
      <td>90.367591</td>
      <td>100.0</td>
      <td>95.183795</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_type = final_school_df.drop(columns=["Total Students","Total School Budget","Per Student Budget","School Name"])

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
      <th>School Type</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>District</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>89.529743</td>
      <td>100.0</td>
      <td>94.764871</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Charter</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>District</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>88.436758</td>
      <td>100.0</td>
      <td>94.218379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>District</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>89.302665</td>
      <td>100.0</td>
      <td>94.651333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Charter</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>District</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>89.083064</td>
      <td>100.0</td>
      <td>94.541532</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Charter</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>District</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>88.858416</td>
      <td>100.0</td>
      <td>94.429208</td>
    </tr>
    <tr>
      <th>8</th>
      <td>District</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>89.182945</td>
      <td>100.0</td>
      <td>94.591472</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Charter</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>District</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>88.547137</td>
      <td>100.0</td>
      <td>94.273568</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Charter</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Charter</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Charter</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Charter</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
final_school_df = grouped_type.groupby(["School Type"])
final_school_df.mean()
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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>100.000000</td>
      <td>100.0</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>88.991533</td>
      <td>100.0</td>
      <td>94.495766</td>
    </tr>
  </tbody>
</table>
</div>



1.	Smaller schools (i.e. <1000 and 1000-2000) have higher overall passing rates and math and reading passing rates than schools with students totaling 2000-5000. 
2.	Charter schools have higher overall passing rate sand math and reading passing rates than District schools – the top five schools (based on overall passing rate) are all Charter schools while the bottom five schools (based on overall passing rate) are all District schools.
3.	Schools with higher per student budgets have lower overall passing rates than schools with lower per student budgets.
