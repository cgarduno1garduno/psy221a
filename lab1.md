# Lab 1 Assignment
This is an exercise in inputting data and plotting simple bar graphs
Optional functions are listed, and commented out, at the bottom of the script

##### Known issues:
Plots don't fit properly on screen
no y labels on plots

### Input data
There are ABSOLUTELY easier ways of inputting data. Just generate a text file or csv file and read it in. 
```r
subid  = c(1:10)  # Subject ID
recom  = c(3,5,1,5,2,3,5,4,3,2)  # Student's recommendation of class
wkhard = c(5,4,3,1,4,5,2,4,4,4)  # How hard student reported working
coll   = c(1,2,3,1,NA,1,2,3,1,2) # College variable
gen    = c(0,1,1,1,0,0,0,1,0,1)  # binary gender response
read   = c(0,1,0,1,1,0,0,1,1,1)  # T/F; did reading
hw     = c(1,1,1,0,1,1,1,1,0,1)  # T/F; did homework
excdt  = c(1,0,0,0,1,1,1,0,0,1)  # T/F; did extra credit
gpa    = c(3.12,2.91,3.33,NA,2.98,3.12,2.91,3.33,2.65,2.98) # GPA
```

### Generate labels for the factor functions below
Labels can be explicitly stated in the factor function, but consider keeping your code clean and easy to read.
```r
labs_coll = c("Arts&Sciences","Business","Engineering")
labs_gen  = c("Female", "Male")
labs_cnc  = c("Checked", "Not Checked")
```

### Transform coll and gen to factors
```r
collf  = factor(coll,  level = c(1:3), labs_coll)
genf   = factor(gen,   level = c(1,0), labs_gen)
readf  = factor(read,  level = c(1,0), labs_cnc)
hwf    = factor(hw,    level = c(1,0), labs_cnc)
excdtf = factor(excdt, level = c(1,0), labs_cnc)
```

### Generate data frame, and csv file to directory
If you read your data from a file, you can directly make it into an R or Pandas dataframe. 
```r
dat = data.frame(subid, recom, wkhard, collf, genf, gpa, readf, hwf, excdtf)
write.csv(dat, "Psy221ALab_Sept23data")
```

### Generate graphs
```r
par(mfrow = c(4,2))
par(mar = rep(2, 4))
plot(dat$gen,   main = "Gender",              border = 'navyblue', col = "deepskyblue") 
plot(dat$coll,  main = "College",             border = 'navyblue', col = "deepskyblue") 
plot(dat$read,  main = "Did the Reading",     border = 'navyblue', col = "deepskyblue") 
plot(dat$hw,    main = "Did the Homework",    border = 'navyblue', col = "deepskyblue")
plot(dat$excdt, main = "Did Extra Credit",    border = 'navyblue', col = "deepskyblue") 
hist(recom,     main = "Recommend the Class", border = 'navyblue', col = "deepskyblue") 
hist(wkhard,    main = "Worked Hard",         border = 'navyblue', col = "deepskyblue")
hist(gpa,       main = "GPA", xlab = 'GPA',   border = 'navyblue', col = "deepskyblue") 
```
