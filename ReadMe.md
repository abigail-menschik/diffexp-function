# diffexp-function
function to run differential expression

library(GEOquery)
library(limma)

# formatting the data and making targets file not part of the function
# assume it has already been done

diffexpLimma <- function(targ,exp) {
design <- model.matrix(~ 0+targ[,1]);
colnames(design) <- c("UHR","HR");
fit <- lmFit(exp, design);
contrast.matrix <- makeContrasts(UHR-HR, levels=design);
fit2 <- contrasts.fit(fit, contrast.matrix);
fit2 <- eBayes(fit2);
tt <- topTable(fit2, coef=1, number=Inf);
return(tt)
}
    
