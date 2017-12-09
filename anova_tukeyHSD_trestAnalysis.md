# One-way ANOVA, Tukey Pairwise Comparisons, and Quadratic Trend Analysis

From *Explaining Psychological Statistics* (4th Ed, Cohen, Ch13, B16), we have the following data showing the number of driving errors that subjects made on a driving simulation video game given some amount of caffeine. 
           
| 0mg | 100mg | 200mg | 300mg |
|-----|-------|-------|-------|
| 25  |  16   |   6   |   8   |
| 19  |  15   |  14   |  18   |
| 22  |  19   |   9   |   9   |
| 15  |  11   |   5   |  10   |
| 16  |  14   |   9   |  12   |
| 20  |  23   |  11   |  13   |

## One-way ANOVA
**Required Packages**: `{psych}`, `{car}`

Input the data into `scores` dataframe and create `labels` variable. Use  `describeBy` from the `{psych}` package to return descriptive statistics. 
```r
scores = c(25, 19, 22, 15, 16, 20,
           16, 15, 19, 11, 14, 23,
            6, 14,  9,  5,  9, 11,
            8, 18,  9, 10, 12, 13)
            
levs = factor(rep(1:4, each=6), levels=c(1:4),
                labels=c("0mg", "100mg", "200mg", "300mg"))
                
pugs = describeBy(scores, levels)

dawg = data.frame(rbind(pugs$`0mg`[3],
                        pugs$`100mg`[3],
                        pugs$`200mg`[3],
                        pugs$`300mg`[3])) 
                        
dawg$condition = levels(levs)
```

We use the `leveneTest` function from the `{cars}` package to test for homogeneity of variance, then use `aov` to compute the ANOVA. 
```r
leveneTest(scores, levs)
scores.aov = aov(scores ~ levs)
summary(scores.aov)
```

## Tukey Pairwise Comparisons
**Required Packages**: `{agricolae}`

We can compute the pairwise comparison easily using `HSD.test` from the `{agricolae}` package. The results can be shown by running `> test` in the console. 
```r
test = HSD.test(scores.aov, 'levs', alpha = 0.05, group = FALSE)
```

## Quadratic Trend Analysis


