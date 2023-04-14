# Calculate the 98th percentile of BMI for the population
pop_percentile <- quantile(diabetes$BMI, 0.98)

# Sample 50 patients from the data and calculate their 98th percentile of BMI
set.seed(100)
sample_data <- diabetes[sample(nrow(diabetes), 50), ]
sample_percentile <- quantile(sample_data$BMI, 0.98)

# Create a histogram of BMI for the population and highlight the 98th percentile
hist(diabetes$BMI, main="BMI Distribution in Population", xlab="BMI")
abline(v=pop_percentile, col="blue")

# Create a histogram of BMI for the sample and highlight the 98th percentile
hist(sample_data$BMI, main="BMI Distribution in Sample", xlab="BMI")
abline(v=sample_percentile, col="blue")
