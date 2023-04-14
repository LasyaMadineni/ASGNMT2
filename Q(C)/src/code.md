  #Calculate population statistics for BloodPressure
pop_mean <- mean(diabetes$BloodPressure)
pop_sd <- sd(diabetes$BloodPressure)
pop_percentile <- quantile(diabetes$BloodPressure, probs = c(0.25, 0.5, 0.75))

n_samples <- 500
sample_size <- 150
set.seed(100) # for reproducibility
samples <- lapply(1:n_samples, function(x) {
  sample(diabetes$BloodPressure, size = sample_size, replace = TRUE)
})

sample_means <- sapply(samples, mean)
sample_sds <- sapply(samples, sd)
sample_percentiles <- t(sapply(samples, function(x) quantile(x, probs = c(0.25, 0.5, 0.75))))

# Plot the distributions of BloodPressure for the population and the average means from the samples
library(ggplot2)
library(gridExtra)

pop_plot <- ggplot(diabetes, aes(x = BloodPressure)) + 
  geom_histogram(aes(y = ..density..), binwidth = 2, color = "grey", fill = "white") +
  geom_density(color = "red") + 
  ggtitle("Distribution of BloodPressure in the Population")

sample_plot <- ggplot(data.frame(mean = sample_means), aes(x = mean)) + 
  geom_histogram(aes(y = ..density..), binwidth = 2, color = "grey", fill = "white") +
  geom_density(color = "blue") + 
  ggtitle("Distribution of Average Means from Samples")

grid.arrange(pop_plot, sample_plot, ncol = 2)

#Compare the population statistics with the sample statistics
cat("Population Mean: ", pop_mean, "\n")
cat("Sample Mean: ", mean(sample_means), "\n\n")
cat("Population SD: ", pop_sd, "\n")
cat("Sample SD: ", mean(sample_sds), "\n\n")
cat("Population Percentiles: \n")
print(pop_percentile)
cat("\n")
cat("Sample Percentiles: \n")
print(apply(sample_percentiles, 2, mean))

