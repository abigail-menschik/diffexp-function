# diffexp-function
function to run differential expression

library(GEOquery)
library(limma)

# formatting the data and making targets file not part of the function
# assume it has already been done

diffexpLimma <- function(targ,expset) {

targDF <- targ;
targ <- targ[,1];
design <- model.matrix(~ 0+targ);
colnames(design) <- gsub("targ", "", colnames(design));
fit <- lmFit(expset, design);

contrast.matrix <- makeContrasts(group2-group1, levels=design);
fit2 <- contrasts.fit(fit, contrast.matrix);
fit2 <- eBayes(fit2);
tt <- topTable(fit2, coef=1, number=Inf);
return(tt)

}
    
