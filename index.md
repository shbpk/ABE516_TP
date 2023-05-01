---
layout: default
---
---


## Introduction
Antimicrobials, including antibiotics, antivirals, antifungals and antiparasitics are the medicines used to prevent and treat infections in humans, animals and plants. According to the National data for the United States reveal that almost 270 million antibiotics prescriptions are written each year <a href="https://www.michiganmedicine.org/health-lab/nearly-quarter-antibiotic-prescriptions-may-be-unnecessary#:~:text=National%20data%20indicate%20that%20around,prescriptions%20are%20filled%20every%20year">[report]</a>. This is roughly a prescription for every 5 out of 6 people in the US. Antimicrobial Resistance (AMR) occurs when bacteria, viruses, fungi and parasites change over time and no longer respond to medicines making infections harder to treat and increasing the risk of disease spread, severe illness and death. As a result of drug resistance, antibiotics and other antimicrobial medicines become ineffective and infections become increasingly difficult or impossible to treat. AMR can be a serious threat  for the future generations and according the some researchers, it can be a threat more severe than cancer in 2050 as shown if the figure.



![alt text](assets/css/AMR-ONeil.png)
<center>
Predicted mortality from AMR compared to other common caualities
<a href="https://www.gavi.org/vaccineswork/what-antimicrobial-resistance-and-how-can-we-tackle-it?gclid=CjwKCAjwo7iiBhAEEiwAsIxQEe9oBkLiHuUFI8ru5pDI6lSTsba_wHPjZBYob6fX-YYfKzztvWuvEhoCdtUQAvD_BwE">[Image Source: Gravi.org]</a>
</center>


## AMR in Agriculture
The global spread of antimicrobial resistant organisms and AMR-associated genes poses a serious threat to the safety of both human and natural systems, increasing the hospitalization and mortality rates of both humans and production animals <a href="#1"><sup>1</sup></a>. In particular, the release of ARGs and organisms into the environment from agricultural sources is considered a serious health threat <a href="#2"><sup>2</sup></a>. For example, antibiotic treatments have been observed to cause increases in the abundance of ARGs in animals, which leads to concomitant ARG prevalence in manure from antibiotic-treated animals <a href="#3"><sup>3</sup></a>. Elevated concentrations of antibiotics and ARGs have also been found in or near livestock production facilities <a href="#4"><sup>4</sup></a>. Moreover, land application of manure has been observed to result in transient increases in ARG abundance and populations of resistant zoonotic microorganisms <a href="#5"><sup>5</sup></a>. In sum, the joint occurrence of a large number of farm animals receiving antibiotics and dependence on shared soil and water resources makes animal agriculture and farms important potential contributors to antibiotic resistance observed in clinical settings <a href="#6"><sup>6</sup></a>.

There can be various pathways antimicrobial resistance in the environment. One of the hypothesized pathway is illustrated in the figure below.

![AMR in Ag. Pathway](assets\AgAMRCycl.png)
<center>A hypothetical AMR cyle in agricultural environment</center>

Antibiotics administered to animals for various reasons are not metabolized completely and aree found undigested in their manure. Applying manure for better soil health resulting to better crops is a common practices around the world. This can be an environment where bacteria can develope resistance to the antibiotics and reach human through water uptake by plants or instream water.

Tylosin is an antibiotic drug commonly used in veterinary medicine to treat a wide range of bacterial infections in animals, particularly in poultry, swine, and cattle. Tylosin works by inhibiting bacterial protein synthesis, which prevents the growth and spread of the bacteria <a href="#7"><sup>7</sup></a>.

Enterocci is a bacteria found in human intestine and egricultural environment <a href="#8"><sup>8</sup></a> and have shown tendency to develop resistance to antibiotics.

## Objective
 The objective of this study was to deduce a relationship between the presence of enterocci, a bacteria found in human intestine and egricultural environment <a href="#8"><sup>8</sup></a>, and it's mutated variant having tylosin resistance, the tylosin resistance eterrocci. 

This will provide an evidence of tylosic resistance bacteria in agricultural watersheds where enterocci is found if a strong relationship is found.

## Material and Methods
### Study Area
The data comprises of observed water quality data from the Black Halk Lake (BHL) watershed in SAC county-IA. The Black Hawk Lake watershed catalouged as HUC12 level by the USEPA is a small watershed (shown is figure below) within the North Raccoon River (HUC-8) and Indian Creek-North Raccoon River (HUC-10) watersheds.

![Study Area Map](assets\bhl.png)
<center>Study area, the Black Hawk Lake Watershed</center>

### Data
Observed data includes grab sampling from 5 different locations within the BHL watershed done every two week since 2018. The samples are bacteria plated to check for the presence of enterrocci and its tylosin resistant variant along with other water quality paramterets like total nitrogen, and phosphorous, etc. The data analzyed in this study also consists of climatic variables of the sampling week, i.e., total precipiation, and the average temperature of the week when sampling was done. Sample of the data analyzed is shown below:

| `Date` | `ent` | `tet_ent` | `tyl_ent` | `ecoli` | `Precip` |	`Precip-1` | `Temp` | `Temp-1` | `TSS` |	`DRP` |	`TP`	| `TN`	| `Avg_Flow` |
|:-----|:-----|:-----|:-----|:-----|:-----|:------|:-----|:-----|:-----|:-----|:-----|:-----|:-----|
|18/03/2021	|87|22|5|120|0|1|55|60|80|244|22|66|0.03|
|25/03/2021	|90|18|2|99|3|0|66|66|88|279|23|80|0.08|

The variables are described as follows

| Variable        | Description          | Unit |
|:-------------|:------------------|:------|
| `Date`           | day of sampling | Date  |
| `ent`           | Amount to enterocci | Colonies per 100 ml of sample  |
| `tet_ent`           | Amount of tetracycline resistant enterococci | Colonies per 100 ml of sample  |
| `tyl_ent`           | Amount of tylosin resistant enterococci | Colonies per 100 ml of sample  |
| `ecoli`           | Amount of Ecoli. | Colonies per 100 ml of sample  |
| `Precip`           | Total rainfall during the sampling week | inch  |
| `Precip-1`           | Total rainfall in previous week | inch  |
| `Temp`           | Average temperature od sampling week | Degrees farenheit  |
| `Temp-1`           | Average temperature of previous week | Degrees farenheit  |
| `TSS`           | Total suspended solids  | mg/L|
| `DRP`           | Dissolved reactive phosphorous  | mg/L|
| `TP`           | Total phosphorous  | mg/L|
| `TN`           | Total nitrogen  | mg/L|
| `Avg_Flow`           | Average flow of the sampling week  | mg/L|


# Analyses
The study uses machine learning approach to develop a model to predict tylosin resitant bacteria in an agricultural watershed. Two model are used in this study, `1- Linear regression to treat data ignoring timeseries behavious`, and `2- XGBoost regressor considering timeseries`. Analyzed dataset is available in the  <a href="https://github.com/shbpk/ABE516_TP">GitHub repository</a> along with the interactive python notebooks.

[`View full code for Linear Regression`](https://github.com/shbpk/ABE516_TP/blob/ffbdd114018512647dde6a179ecf72b358a17891/Notebooks/Term%20Project%20LR.ipynb)

[`View full code for XGBoost Regression`](https://github.com/shbpk/ABE516_TP/blob/ffbdd114018512647dde6a179ecf72b358a17891/Notebooks/Term%20Project%20XGBR.ipynb)

The analyses starts with eliminating the null values or substituting them with a legitimate assumption, executing their descriptive analysis and scatter plot to understand the data. Scatter plot of the predicted variable "`tet_ent`" with other variables is shown below.

![Scatter Plot](assets\LR_Plot.png)
<center>Scatter plot of the variables</center>

The variable, formatted and cleaned treated with the linear regression model library from sckikitlearn and also the XGBoost regressor.

### Methodology Flowchart




# Results
## Linear Regression Analysis

### Model Performance

|Statitics|.|.|.|
|:-------|:-----|:-----|:-----|
|Dep. Variable:|      tet_ent|   R-squared:|         0.859|
|F-statistic:|       393.9|   Adj. R-squared:|       0.857|
|No. Observations:|     330|   Prob (F-statistic):     |2.51e-135|


### Coefficients and Their Significance

|Predictor                 |Coefficent    |Standard Error          |t-statistic      |Probability>t      |Confidence Intervals I 95%[0.025      0.975]|
|:----|:-----|:-----|:-----|:------|:------|
|Intercept    |-16.9269      |8.953     |-1.891      |0.060     |-34.540    ~   0.686|
|ent            |0.0170      |0.005      |3.536      |0.000       |0.008 ~      0.026|
|ecoli          |0.0307      |0.003     |10.171      |0.000       |0.025 ~      0.037|
|tyl_ent        |1.0604      |0.097     |10.906      |0.000       |0.869 ~       1.252|
|Precip        |65.0207      |9.205      |7.064      |0.000      |46.911 ~     83.130|
|Temp           |0.2425      v0.150      |1.611      |0.108      |-0.054 ~       0.539|


## XGBoost Regression

![Scatter Plot](assets\xgbr_out.png)
<center>Significance of variables for XGBoost Model</center>

`R-Squared for XGBoost Model = 0.914`

# Refernces
<p id="1">1- Allen, H. K.; Donato, J.; Wang, H. H.; Cloud-Hansen, K. A.; Davies, J.; Handelsman, J., Call of the wild: antibiotic resistance genes in natural environments. Nat. Rev. Microbiol. 2010, 8, (4), 251-259.</p>

<p id="2">2- PCAST Report to the President on Combating Antibiotic Resistance; Executive Office of the President of the United States: 2014, 2014; p 78.</p>

<p id="3">3- Holman, D. B.; Chénier, M. R., Impact of subtherapeutic administration of tylosin and chlortetracycline on antimicrobial resistance in farrow-to-finish swine. FEMS Microbiol. Ecol. 2013, 85, (1), 1-13.</p>

<p id="4">4- Chee-Sanford, J. C.; Mackie, R. I.; Koike, S.; Krapac, I. G.; Lin, Y.-F.; Yannarell, A. C.; Maxwell, S.; Aminov, R. I., Fate and transport of antibiotic residues and antibiotic resistance genes following land application of manure waste. J. Environ. Qual. 2009, 38, (3), 1086-1108.</p>

<p id="5">5- Heuer, H.; Schmitt, H.; Smalla, K., Antibiotic resistance gene spread due to manure application on agricultural fields. Curr. Opin. Microbiol. 2011, 14, (3), 236-243.</p>

<p id="6">6- McEwen, S. A.; Fedorka-Cray, P. J., Antimicrobial use and resistance in animals. Clin. Infect. Dis. 2002, 34 Suppl 3, S93-S106.</p>

<p id="7">7- Suchodolski, Jan S., Scot E. Dowd, Elias Westermarck, Jörg M. Steiner, Randy D. Wolcott, Thomas Spillmann, and Jaana A. Harmoinen. "The effect of the macrolide antibiotic tylosin on microbial diversity in the canine small intestine as demonstrated by massive parallel 16S rRNA gene sequencing." BMC microbiology 9, no. 1 (2009): 1-16.</p>

<p id="8">8- Ramos, Sónia, Vanessa Silva, Maria de Lurdes Enes Dapkevicius, Manuela Caniça, María Teresa Tejedor-Junco, Gilberto Igrejas, and Patrícia Poeta. "Escherichia coli as commensal and pathogenic bacteria among food-producing animals: Health implications of extended spectrum β-lactamase (ESBL) production." Animals 10, no. 12 (2020): 2239.</p>

<a href="#TOP">Back to top</a>


_____________________________________________________



```python
# Code to show here
import pandas as pd
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

[#View full code for XGBoost Regessor](https://github.com/shbpk/ABE516_TP/blob/0dabaabaf7d6935327f6261e57a2a2c9f23e7f96/Notebooks/Term%20Project%20XGBR.ipynb)

[#View full code for Linear Regression](https://github.com/shbpk/ABE516_TP/blob/0dabaabaf7d6935327f6261e57a2a2c9f23e7f96/Notebooks/Term%20Project%20LR.ipynb).



## Results and Discussion



| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>
   

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
More Notes May be ?
```





