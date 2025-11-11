# Data Privacy Utility Metrics and Project Timeline (R Implementation)

### Generalization Loss
Measures average squared deviation between original and anonymized quasi-identifiers.
generalization_loss <- function(original, anonymized) {
  mean((original - anonymized)^2)
}

### Discernibility Metric
Quantifies indistinguishability of records via equivalence class squared sizes.
discernibility_metric <- function(anonymized_df, quasi_identifiers) {
  groups <- aggregate(rep(1, nrow(anonymized_df)),
                      by = anonymized_df[quasi_identifiers],
                      FUN = sum)
  sum(groups$x^2)
}

### KL Divergence (Utility Loss)
Computes divergence between original and anonymized attribute distributions.
kl_divergence <- function(original_dist, anonymized_dist) {
  sum(original_dist * log(original_dist / anonymized_dist))
}
