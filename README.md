## About

Two projects completed in my statistical modelling modules in my first and second years at university.  

### Water Chemistry EDA
EDA of three datasets storing precipiation, soil solution and stream water chemistry data. TO BE ADDED. 

### Diamond Price Modelling
Finding the relationship between the price and cut quality of diamonds using linear regression models. 

#### 1. Dimensional Predictors and Multicollinearity
* **Theoretical Expectation:** the diamond's volume $\text{Volume} \propto xyz$ where $x$, $y$ and $z$ are the width, height and length. In a \log-linear model, this implies the dimensional coefficients $\beta_1 = \beta_2 = \beta_3 = 2$.
* **Problem:** $x, y, z$ are near-perfectly correlated which introduces severe **multicollinearity** causing individual $t$-tests to falsely show $\log(x)$ as insignificant as $p = 0.842$. Conversely, a sequential ANOVA reveals $\log(x)$ is highly significant as $p \ll 0.01$ when introduced first.
* **VIF Metrics:** $\log(x)$: **229.57**, $\log(y)$: **208.49**, and $\log(z)$: **23.08** where values $> 10$ signal extreme inflation.
* **Solution:** replace $x, y, z$ with **Carat weight** which accounts for the diamond's size and mass on the model and does not introduce multicollinearity. 

#### 2. Categorical Effects: Cut Quality
* **Strategy:** evaluated whether diamond `cut` (categories: good, very good, and ideal) changes the baseline pricing model via nested models: $\log(\text{price}) \sim \log(\text{weight}) \times \text{cut}$.
* **Main Effect:** highly significant as $p = 9.86 \times 10^{-11}$. Without `cut`, the baseline pricing model systematically overestimates good cut and underestimates ideal cut diamonds.
* **Interaction Effect:** statistically insignificant as $p = 0.1918$. Price elasticity with respect to weight remains uniform across all cut grades as the regression lines are almost parallel. 
* **Solution:** retain `cut` as a main effect and give each cut grade a different starting price but omit the interaction terms. 

#### 3. Residual Analysis and Ommited Variables: Clarity
* **Pattern:** plotting baseline model errors showed consistent overestimating of the price of Lower-Clarity (`SI`) diamonds and underestimating of High-Clarity (`VSI`) diamonds. 
* **Insight:** the above pattern confirmed an **Omitted Variable Bias** and leaving out clarity caused the model to systematically misprice diamonds. 
* **Proof:** a partial $F$-test confirmed adding clarity resolves the ommited variable bias since $F_{\text{obs}} = 941.4$ and $p < 2.2 \times 10^{-16}$.
* **Note:** as clarity is a binary variable, the above partial $F$-test simplifies to a standard two-sided $t$-test as $F = t^2$. 
