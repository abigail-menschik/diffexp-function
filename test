# diffexp-function
function to run differential expression

library(GEOquery)
library(limma)

diffexp <- function(x) {
        data <- getGEO("x")
        eset <- data[[1]]
        e <- exprs(eset)
        
