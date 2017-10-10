### General Maintenance Functions
Cleaning up your workspace
```r
# Clear workspace
clearws = function() {
  rm(list=ls(.GlobalEnv), envir=.GlobalEnv)
}

# Clear console
clearcons = function() {
  cat("\014")
}

# Clear workspace and console
# *The previous two functions must be defined in order for this function to work*
clear = function() {
  clearcons()
  clearws()
}  
```

Setting up a working environment. Note that you can also setup a user R configuration startup file. 
```r
# Retrieve current working directory
getwd()

# Set new working directory
setwd("~/Desktop/UCSB/fall2017/psych221a/lab")
```
