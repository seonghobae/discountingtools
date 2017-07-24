# discountingtools
-------------------
R package for performing delay discounting analyses.  Features include approximate Bayesian model selection, derivation of the Effective Delay 50 (ED50) and both normal and log10 transformation model area using Numerical Integration

### Version
-------------------
0.0.0.2 (alpha)

### Installation
----------------
1) Install and load the devtools package. 
2) Install and load the digest package. 
3) Run install_github to install the package.

```r
install.packages("devtools")
install.packages("digest")

devtools::install_github("miyamot0/discountingtools")

library(discountingtools)
```

### Examples
-------------------------

#### Effective Delay Plotting

```r
dat <- data.frame(X=c(1,30,180,540,1080, 2160), Y=c(1,0.9,0.8,0.7,0.6, 0.4))

results <- discountingModelSelection(dat, 
                                     models = c("exponential", "hyperbolic", "bd", "mg", "rachlin", "cs"), 
                                     figures = "ed50",
                                     summarize = TRUE,
                                     lineSize = 1.5)
                                     
Model Comparison Summary:
Rank #:  1  =  CS
 Probability  =  0.759601
 BIC  =  -22.2279

Rank #:  2  =  Rachlin
 Probability  =  0.18008
 BIC  =  -19.349116

Rank #:  3  =  MG
 Probability  =  0.033585
 BIC  =  -15.990462

Rank #:  4  =  Mazur
 Probability  =  0.022795
 BIC  =  -15.215414

Rank #:  5  =  exp
 Probability  =  0.003675
 BIC  =  -11.565193

Rank #:  6  =  BD
 Probability  =  0.000258
 BIC  =  -6.252941

Rank #:  7  =  noise
 Probability  =  6e-06
 BIC  =  1.128501
 
print(results)
                                     
  noise.mean noise.RMSE noise.BIC noise.AIC   exp.lnk   exp.RMSE   exp.BIC   exp.AIC Mazur.lnk Mazur.RMSE Mazur.BIC Mazur.AIC
1  0.7333333  0.2160247  1.128501  1.544982 -7.615692 0.07500726 -11.56519 -11.14871 -7.217119 0.05533467 -15.21541 -14.79893
    BD.beta  BD.delta   BD.RMSE    BD.BIC   BD.AIC    MG.lnk     MG.s    MG.RMSE    MG.BIC    MG.AIC Rachlin.lnk Rachlin.s
1 0.9999994 0.9993449 0.1124525 -6.252941 -5.62822 -5.657531 0.378083 0.04995242 -15.99046 -15.36574          -5      0.68
  Rachlin.RMSE Rachlin.BIC Rachlin.AIC    CS.lnk      CS.s    CS.RMSE   CS.BIC    CS.AIC noise.BF   exp.BF Mazur.BF    BD.BF
1   0.03775746   -19.34912   -18.72439 -7.976814 0.5702152 0.02970408 -22.2279 -21.60318        1 570.6905 3540.268 40.07374
     MG.BF Rachlin.BF    CS.BF   noise.prob    exp.prob Mazur.prob      BD.prob    MG.prob Rachlin.prob   CS.prob probable.model
1 5215.976   27967.79 117971.8 6.438837e-06 0.003674583 0.02279521 0.0002580283 0.03358482      0.18008 0.7596009             CS
  probable.ED50 probable.AUC probable.Log10AUC
1      7.334051    0.5976186         0.8438519
```

![Alt text](Figure_ED50.png?raw=true "ED50 Visuals")

#### Model-based Area

```r
dat <- data.frame(X=c(1,30,180,540,1080, 2160), Y=c(1,0.9,0.8,0.7,0.6, 0.4))

results <- discountingModelSelection(dat, 
                                     models = c("exponential", "hyperbolic", "bd", "mg", "rachlin", "cs"), 
                                     figures = "auc",
                                     summarize = TRUE,
                                     lineSize = 1.5)
                                     
Model Comparison Summary:
Rank #:  1  =  CS
 Probability  =  0.759601
 BIC  =  -22.2279

Rank #:  2  =  Rachlin
 Probability  =  0.18008
 BIC  =  -19.349116

Rank #:  3  =  MG
 Probability  =  0.033585
 BIC  =  -15.990462

Rank #:  4  =  Mazur
 Probability  =  0.022795
 BIC  =  -15.215414

Rank #:  5  =  exp
 Probability  =  0.003675
 BIC  =  -11.565193

Rank #:  6  =  BD
 Probability  =  0.000258
 BIC  =  -6.252941

Rank #:  7  =  noise
 Probability  =  6e-06
 BIC  =  1.128501
 
print(results)
                                     
  noise.mean noise.RMSE noise.BIC noise.AIC   exp.lnk   exp.RMSE   exp.BIC   exp.AIC Mazur.lnk Mazur.RMSE Mazur.BIC Mazur.AIC
1  0.7333333  0.2160247  1.128501  1.544982 -7.615692 0.07500726 -11.56519 -11.14871 -7.217119 0.05533467 -15.21541 -14.79893
    BD.beta  BD.delta   BD.RMSE    BD.BIC   BD.AIC    MG.lnk     MG.s    MG.RMSE    MG.BIC    MG.AIC Rachlin.lnk Rachlin.s
1 0.9999994 0.9993449 0.1124525 -6.252941 -5.62822 -5.657531 0.378083 0.04995242 -15.99046 -15.36574          -5      0.68
  Rachlin.RMSE Rachlin.BIC Rachlin.AIC    CS.lnk      CS.s    CS.RMSE   CS.BIC    CS.AIC noise.BF   exp.BF Mazur.BF    BD.BF
1   0.03775746   -19.34912   -18.72439 -7.976814 0.5702152 0.02970408 -22.2279 -21.60318        1 570.6905 3540.268 40.07374
     MG.BF Rachlin.BF    CS.BF   noise.prob    exp.prob Mazur.prob      BD.prob    MG.prob Rachlin.prob   CS.prob probable.model
1 5215.976   27967.79 117971.8 6.438837e-06 0.003674583 0.02279521 0.0002580283 0.03358482      0.18008 0.7596009             CS
  probable.ED50 probable.AUC probable.Log10AUC
1      7.334051    0.5976186         0.8438519
```

![Alt text](Figure_Model_AUC.png?raw=true "Model AUC Visuals")

#### Model-based Area (logarithmic scaling)

```r
dat <- data.frame(X=c(1,30,180,540,1080, 2160), Y=c(1,0.9,0.8,0.7,0.6, 0.4))

results <- discountingModelSelection(dat, 
                                     models = c("exponential", "hyperbolic", "bd", "mg", "rachlin", "cs"), 
                                     figures = "logauc",
                                     summarize = TRUE,
                                     lineSize = 1.5)
                                     
Model Comparison Summary:
Rank #:  1  =  CS
 Probability  =  0.759601
 BIC  =  -22.2279

Rank #:  2  =  Rachlin
 Probability  =  0.18008
 BIC  =  -19.349116

Rank #:  3  =  MG
 Probability  =  0.033585
 BIC  =  -15.990462

Rank #:  4  =  Mazur
 Probability  =  0.022795
 BIC  =  -15.215414

Rank #:  5  =  exp
 Probability  =  0.003675
 BIC  =  -11.565193

Rank #:  6  =  BD
 Probability  =  0.000258
 BIC  =  -6.252941

Rank #:  7  =  noise
 Probability  =  6e-06
 BIC  =  1.128501
 
print(results)

  noise.mean noise.RMSE noise.BIC noise.AIC   exp.lnk   exp.RMSE   exp.BIC   exp.AIC Mazur.lnk Mazur.RMSE Mazur.BIC Mazur.AIC
1  0.7333333  0.2160247  1.128501  1.544982 -7.615692 0.07500726 -11.56519 -11.14871 -7.217119 0.05533467 -15.21541 -14.79893
    BD.beta  BD.delta   BD.RMSE    BD.BIC   BD.AIC    MG.lnk     MG.s    MG.RMSE    MG.BIC    MG.AIC Rachlin.lnk Rachlin.s
1 0.9999994 0.9993449 0.1124525 -6.252941 -5.62822 -5.657531 0.378083 0.04995242 -15.99046 -15.36574          -5      0.68
  Rachlin.RMSE Rachlin.BIC Rachlin.AIC    CS.lnk      CS.s    CS.RMSE   CS.BIC    CS.AIC noise.BF   exp.BF Mazur.BF    BD.BF
1   0.03775746   -19.34912   -18.72439 -7.976814 0.5702152 0.02970408 -22.2279 -21.60318        1 570.6905 3540.268 40.07374
     MG.BF Rachlin.BF    CS.BF   noise.prob    exp.prob Mazur.prob      BD.prob    MG.prob Rachlin.prob   CS.prob probable.model
1 5215.976   27967.79 117971.8 6.438837e-06 0.003674583 0.02279521 0.0002580283 0.03358482      0.18008 0.7596009             CS
  probable.ED50 probable.AUC probable.Log10AUC
1      7.334051    0.5976186         0.8438519

```

![Alt text](Figure_Model_AUC_Log10.png?raw=true "Log10 Model AUC Visuals")

### Model Candidates (Possible models within the model selection approach)
-------------------
* Noise Model: Intecept-only comparison model (included by default)
* Exponential Model: Samuelson, P. A. (1937). A note on measurement of utility. The Review of Economic Studies, 4(2), 155–161. https://doi.org/10.2307/2967612
* Hyperbolic Model: Mazur, J. E. (1987). An adjusting procedure for studying delayed reinforcement. In Quantitative analysis of behavior: Vol. 5. The effect of delay and intervening events on reinforcement value (pp. 55–73). Hillsdale, NJ: Erlbaum.
* Beta Delta Model: Laibson, D. (1997). Golden eggs and hyperbolic discounting. The Quarterly Journal of Economics, 112(2), 443–478. https://doi.org/10.1162/003355397555253
* Green & Myerson Model: Green, L., & Myerson, J. (2004). A discounting framework for choice with delayed and probabilistic rewards. Psychological Bulletin, 130(5), 769–792. https://doi.org/10.1037/0033-2909.130.5.769
* Rachlin Model: Rachlin, H. (2006). Notes on discounting. Journal of the Experimental Analysis of Behavior, 85(3), 425–435. https://doi.org/10.1901/jeab.2006.85-05
* Ebert & Prelec Model: Ebert, J. E. J., & Prelec, D. (2007). The Fragility of Time: Time-Insensitivity and Valuation of the Near and Far Future. Management Science, 53(9), 1423–1438. https://doi.org/10.1287/mnsc.1060.0671

### Referenced Works (academic works)
-------------------
The Small N Stats Discounting Model Selector is based on the following academic works:
* Franck, C. T., Koffarnus, M. N., House, L. L., & Bickel, W. K. (2015). Accurate characterization of delay discounting: a multiple model approach using approximate Bayesian model selection and a unified discounting measure. Journal of the Experimental Analysis of Behavior, 103(1), 218–233. https://doi.org/10.1002/jeab.128
* Gilroy, S. P., Franck, C. T., & Hantula, D. A. (2017). The discounting model selector: Statistical software for delay discounting applications. Journal of the Experimental Analysis of Behavior, 107(3), 388–401. https://doi.org/10.1002/jeab.257
* Borges, A. M., Kuang, J., Milhorn, H., & Yi, R. (2016). An alternative approach to calculating Area-Under-the-Curve (AUC) in delay discounting research. Journal of the Experimental Analysis of Behavior, 106(2), 145–155. https://doi.org/10.1002/jeab.219

### Acknowledgments
-------------------
* Donald A. Hantula, Decision Making Laboratory, Temple University [Site](http://astro.temple.edu/~hantula/)
* Chris Franck, Laboratory for Interdisciplinary Statistical Analysis - Virginia Tech

### Questions, Suggestions, and Contributions
---------------------------------------------

Questions? Suggestions for features? <shawn.gilroy@temple.edu>.

### License
-----------

GPL Version 2+
