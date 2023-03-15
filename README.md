<div align='center'>

# Classification Trees With Unbiased Mulitway Splits

</div>
note

1. **Classification tree**

   * binary trees: CART、QUEST  
    More effect may be needed to fully understand a binary tree than one with multiway splits.  
    This is hard to interpret that some classes are spread over two or more terminal nodes.  
    Prune:Some class will not be predict after pruning.  
    J(the number of classes):The more J,the more terminal nodes are required.
   * nonbinary splits(multiway splits): FACT、C4.5、CHA D、FRM  
     CHA D is inapplicable to numerical variables.FACT and FRM do not prune.C4.5 only for categorical variables.  
     **Selection bias**:  
     FACT is biased toward categorical variables and FRM is biased toward numerical variables.  
     Variables differ in their proportions of missing values.

2. **CRUISE(classification rule with unbiased interaction selection and estimation)**
   * Prediction accuracy at least as high as those of CART and QUEST
   * Fast computation speed
   * Practically free of selection bias
   * Sensitive to local interactions
   * It has all preceding properties with or without missing values

3. **Selection of split variable**  
   1D method:To detect unequal class means and variances in the numerical variables.  
   Steps:  
   Let $\alpha$ be a significance level.Suppose $X_1,X_2,\dots,X_k$ are numerical and $X_{k+1},X_{k+2},\dots,X_K$ are categorical.
   1. Carry out an ANOVA analysis on each numerical variable and compute its p-values.Suppose $X_{k_1}$ has the smallest p-value $\hat{\alpha_1}$.
   2. For each categorical variable,form a contingency table and find its $\chi^2$ p-values.Suppose $X_{k_2}$ has the smallest p-value $\hat{\alpha_2}$.
   3. Define $$k'=\begin{cases}k_1, & \hat{\alpha_1}\leq\hat{\alpha_2}\\k_2, & \hat{\alpha_1}>\hat{\alpha_2}\end{cases}$$
   4. If $\min(\hat{\alpha_1},\hat{\alpha_2})<\alpha/K$,choose $X_{k'}$ as the split variable.
   5. Otherwise,find the p-values for Levene's F test for each numerical variable.Suppose $X_{k''}$ has the smallest p-value $\tilde{\alpha}$.  
    (a) If $\tilde{\alpha}<\alpha/(K+K_1)$,choose $X_{k''}$.  
    (b) Otherwise,choose $X_{k'}$

4. **Selection of split points**  
   If X is numerical,FACT applies LDA(normal distribution:Box-Cox transformation).  
   If X is categorical,it is converted to 0-1 vectors.
