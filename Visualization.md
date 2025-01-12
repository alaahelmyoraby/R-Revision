# Data Analysis and Visualization with R

This README outlines the steps to analyze and visualize data using R, focusing on basic data inspection, data visualization, and more advanced techniques like Principal Component Analysis (PCA) and heatmap visualization.

### Required Packages

```R
# Install required packages
install.packages(c("corrplot", "pheatmap", "ggfortify"))
```

### Load the Libraries

```R
# Load the libraries
library(corrplot)    # For correlation heatmap visualization
library(pheatmap)    # For creating heatmaps
library(ggfortify)   # For autoplot() PCA visualization
```

---

## 1. Basic Data Inspection

### Inspect Structure of the Dataset

```R
myData=read.csv("metagenomics_example.csv", row.names = 1)
str(myData)  
# Provides an overview of the dataset's structure, including data types and sample entries.
```

### Summary Statistics for Each Column

```R
summary(myData)
summary(t(myData[,-4]))
# Displays min, max, mean, median, and quartiles for numeric columns.
```

### Frequency Table for a Categorical Column

```R
table(myData)
```

### Dataset Dimensions

```R
dim(myData)  
# Returns the number of rows and columns as (rows, columns).
nrow(myData)
ncol(myData)
```

### Check for Missing Values

```R
is.na(myData)  
# Identifies missing values in the dataset. Use `any(is.na(myData))` to check if there are any.
any(is.na(myData))
```

---

## 2. Basic Data Visualization

### Histogram for Visualizing Data Distribution

```R
hist(as.matrix(myData[,-4]), main = "Histogram of Column", xlab = "Column Values", col = "lightblue")
```

### Boxplot to Identify Outliers and Compare Groups

```R
boxplot(myData$Abundance1 ~ myData$Group, main = "Boxplot by Group", col = "lightgreen")
```

### Q-Q Plot for Assessing Normality

```R
# Compares data quantiles to theoretical normal quantiles.  
qqnorm(myData[,-4]$Abundance1, main = "Q-Q Plot for Column")
qqline(myData[,-4]$Abundance1, col = "red", lwd = 2)  
```

### Correlation Between Two Numeric Variables

```R
cor(myData$Abundance1, myData$Abundance1, method = "pearson", use = "pairwise.complete.obs")  
# should be 1
# Calculates the Pearson correlation coefficient. Replace `pearson` with `spearman` for rank-based correlation.
cor(myData$Abundance1, myData$Abundance1, method = "spearman", use = "pairwise.complete.obs")  
```

### Correlation Heatmap with the `corrplot` Package

```R
cor_matrix <- cor(myData[,-4], use = "pairwise.complete.obs")
corrplot(cor_matrix, method = "color", col = colorRampPalette(c("blue", "white", "red"))(200),  
         main = "Correlation Heatmap", tl.col = "black", addCoef.col = "black")
```

---

## 3. PCA and Heatmap Visualization

### Perform Principal Component Analysis (PCA)

```R
myData_clean <- na.omit(myData)
pca_result <- prcomp(myData_clean[,-4], scale = TRUE)  
```

### Visualize PCA Results

```R
library(ggfortify)
autoplot(pca_result, 
         data = myData_clean,   # Use the cleaned data
         colour = 'Group',      # Color points by an existing variable (e.g., Group)
         title = "PCA Plot")    # Add a title
```

### Heatmap of Scaled Data

```R
library(pheatmap)  
scaled_data <- scale(myData_clean[,-4])  # Standardizes the data
# Creates a heatmap with hierarchical clustering.
pheatmap(scaled_data, cluster_rows = TRUE, cluster_cols = TRUE,  
         color = colorRampPalette(c("blue", "white", "red"))(50), main = "Heatmap of Scaled Data")
```
