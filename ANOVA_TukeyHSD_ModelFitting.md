# One-way ANOVA, Tukey Pairwise Comparisons, and Polynomial Fitting

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
**Required Packages**: `{dplyr}`, `{magrittr}`

We start by organizing the data in a way that's easy to visualize. `x_groups` will be a vector containing each group's condition, which we will clean up during plotting. We then generate `dataset1` and `dataset2`, which contain the raw data and the group means, respectively. You can use any package to plot, but we'll stick with the built-in plotting functions. 
```r
x_groups = rep(1:4, each = 6)
dataset1 = data.frame(scores, x_groups)
dataset2 = dataset1 %>% group_by(x_groups) %>% summarise(Avg = mean(scores))

x_values = c(1.0, 2.0, 3.0, 4.0)
x_labels = c("0mg", "100mg", "200mg", "300mg")
plot(dataset1$scores ~ dataset1$x_groups, 
     ylab = "Driving Errors", xlab = "Caffeine (mg)", 
     main = "Driving Errors vs. Caffeine Consumption", axes = FALSE)
axis(side = 1, at = x_values, labels = x_labels)
axis(2)
lines(dataset2$Avg ~ dataset2$x_groups)
```
![](https://github.com/cgarduno1garduno/psy221a/blob/master/de_caffeine_plot1.png)



*Special thanks to @AntoniosK* for helping me understand and visualize the polynomial fitting in [this](https://stackoverflow.com/questions/47726688/quadratic-fitting-for-grouped-data-in-r) post. 
