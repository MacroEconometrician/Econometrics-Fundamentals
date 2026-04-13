# Econometrics-Fundamentals
Heteroskedasticity: Detection, Diagnosis, and Correction in OLS Regression
Author: Elizabeth Saint-Wonder | Macro-Econometrician & AI-Augmented Quantitative Researcher | Stack: Python · NumPy · Pandas · Statsmodels · Scikit-learnDomain: Econometrics | Regression Diagnostics | Inference Reliability
What This Code Is
This notebook provides an end-to-end treatment of heteroskedasticity in Ordinary Least Squares (OLS) regression; one of the violations of the Gauss-Markov assumptions in applied econometrics.
The code moves through three deliberate stages:
	∙	Simulation : intentionally generating heteroskedastic data to isolate the problem in a controlled environment
	∙	Detection : applying the Breusch-Pagan test to formally diagnose non-constant error variance
	∙	Correction : implementing two industry-standard remedies: Heteroskedasticity-Consistent (HC3) robust standard errors, and Weighted Least Squares (WLS)
A real-world wage regression scenario, modelling earnings as a function of education and experience is used as the applied case study throughout.
The Concept and Intuition
What Is Heteroskedasticity?
OLS regression rests on a foundational assumption: the variance of the error term is constant across all observations: a property called homoskedasticity. When that assumption breaks down, that is, when the spread of residuals grows or shrinks systematically with the value of a regressor, you have heteroskedasticity.
The intuition is straightforward. Consider wages: a worker with 8 years of education earns within a fairly narrow band. A worker with 20 years of education may earn anywhere from modestly above minimum wage to an executive salary. The variance of the outcome is not constant, it fans out with education. This is heteroskedasticity in its most recognisable form, and it is ubiquitous in economic and financial data.
Why It Matters and Why It Is Often Misunderstood
Here is the critical distinction that this notebook makes explicit, and that too many practitioners get wrong:
Heteroskedasticity does not bias your OLS coefficients. It biases your standard errors.
The beta estimates remain unbiased and consistent. What breaks down is inference: the standard errors your model reports are no longer reliable, which means your t-statistics are wrong, your confidence intervals are wrong, and your significance tests are wrong. You can make a variable look significant when it is not, or dismiss a genuinely important predictor. In policy and institutional contexts, that is not a technical inconvenience, it is a material risk.
The Two-Solution Framework
Solution 1 : HC3 Robust Standard ErrorsRather than correcting the data-generating process, HC3 corrects the variance-covariance matrix of the estimator. It reweights the contribution of each residual to the standard error calculation, giving greater weight to observations with larger squared residuals. The result: standard errors that honestly reflect uncertainty even when variance is non-constant. This is the minimum viable correction in any applied setting. 
Solution 2 : Weighted Least Squares (WLS)Where HC3 corrects inference after the fact, WLS corrects the estimation itself. Observations with higher variance are downweighted [contributing less to the parameter estimates], while observations with lower, more reliable variance carry greater influence. In practice, WLS regresses squared OLS residuals on the regressors to estimate the variance function, then uses the inverse of predicted variance as observation weights. The result is a more efficient estimator that extracts maximum information from the data.
