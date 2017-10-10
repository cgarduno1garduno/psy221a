###General Maintenance Functions
The functions below clear the workspace, console, or both. 
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
