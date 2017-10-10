Useful R functions
```r
# Function used to clear global environment
clearws = function() {
  rm(list=ls(.GlobalEnv), envir=.GlobalEnv)
}
```
