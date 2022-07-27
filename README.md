# Feature Selection Using Correlation-Association

**Notes**
- When performing Feature Selection, pay attention to entire Correlation score, not only features to target but also features to features
- Take notes on number of features, if total number of features are low, use them regardless of the correlation score
- If correlation is high (>0.8) between features and target, perform EDA based on Domain Knowledge whether feature has direct impact to the target or not.
    - if Yes, drop column/feature regardless of the high correlation score
- If correlation is high (>0.8) between 2 or more features, drop either one to prevent Multicollinearity (few columns/features have same purpose/function), as well as for computation efficiency
- Choosing threshold must consider overall correlation score between Features - Target, if the highest of them all is 0.4 and there's only 1 feature, do not use that threshold but consider to lower them to certain number.

## Correlation (for Numeric x Numeric Columns)
1. Pearson
    > `df.corr('pearson')` or simply `df.corr()`
    - Linear Relationship
    - Condition: Normally Distributed
    - Range: -1 to 1
        - -0.3 < x < 0.3 : Low Correlation
        - -0.7 < x < -0.3 or 0.7 < x < 0.3 : Mid Correlation
        - -1.0 < x < -0.7 or 1.0 < x < 0.7 : High Correlation
    - Positive Correlation: One Way - Linear
    - Negative Correlation: Opposite Way
    - Closer to 1 = Strong Correlation, Linear
        - example: Correlation A and B : 0.90, means Positive High Correlation (the higher the B, the higher A as well)
    - Closer to -1 = Strong Correlation, Opposite
        - example: Correlation C and D : -0.85, means Negative High Correlation (the higher the C, the lower the D)
    - Closer to 0 = Weak Correlation, Barely Correlated

2. Spearman
    > `df.corr('spearman')`
    - Rank Relationship
    - No requirement for data distribution
    - Condition: Different Subject
        - ex: Test score from Teacher A vs Test score from Teacher B
        - ex: Stock price Company A vs  Stock price Company B
    - Range and Correlation Score Interpretation `exactly the same as Pearson`  
    
    3. Kendall
    > `df.corr('kendall')`
    - Condition: Same Subject
        - ex: Quiz score vs Test score from Student A
    - Other detail is `same as Spearman`
    
    `In actual, Spearman and Kendall are not used for Machine Learning, even though in practical many misused occurred but still works`
    
    ## Association (for Categorical x Categorical Columns)
- Range: 0 to 1
- Closer to 1, having more association
    ex: Position vs Promotion
- `Same as correlation`, association did not have causality (cause-effect)

1. Cramers'V
    - Simmetrical: V(x|y) = V(y|x) -> may cause bias
        - ex: Association of City (Silicon Valley, CA) and Job (Tech Engineer) : 0.8
            - V(City|Job) and V(Job|City)
            - Almost all workers in Silicon Valley, CA are Tech Engineers
            - Almost all tech engineers works at Silicon Valley -> bias
    - Based on Pearson Chi-Square
    - Range: 0 to 1
    
2. Theil's U
    - Assimetrical: T(x|y) != T(y|x)
        - ex: Association of City (Silicon Valley, CA) and Job (Tech Engineer)
            - V(City|Job) : 0.4 and V(Job|City) : 0.8
            - Workers in Silicon Valley, CA might not be Tech Engineers
            - Almost all tech engineers works at Silicon Valley
            
## Correlation Ratio (for Numerical x Categorical Columns)
- Range: 0 to 1
- ex: Correlation ratio of City (Cat) and House Price (Num)
- ex: Correlation ratio of Education Level (Cat) and Salary (Num)

## Causality
1. Both `Correlation` and `Association` did not have causality effect
    - ex: Correlation of Land area and House Price -> 0.80
        - House Price: USD 5,000 - Land Area: 60m2
        - Did not translate into USD 5,000 is a result because the land area is 60m2, but there are many other aspects that build the house price
