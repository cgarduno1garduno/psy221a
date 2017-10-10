The function below is used to clear/delete the global workspace.
```r
clearws = function() {
  rm(list=ls(.GlobalEnv), envir=.GlobalEnv)
}
```

This function clears the console. 
```r
clearcons = function() {
  cat("\014")
}
```

You can call functions within functions (as long as the nested functions have been defined, your new function will run) to make things neater. 
```r
clear = function() {
  clearcons()
  clearws()
}  
```
