### Revision
# Math Operations

## Addition
```r
x = 12 + 2  # Addition
mean_of_two <- mean(c(12, 2))  # Mean of two numbers
```

## Histogram
```r
data_for_hist <- c(5, 6, 7, 8, 9)  # Data for histogram
hist(data_for_hist)  # Plot histogram
```

## Other Operations
```r
sqrt(16)  # Square root
min(5, 2, 3, 9)  # Minimum value
```

## Vectors
### Creating and Accessing Vectors
```r
vec <- c(1, 2, 3, 4, 56)  # Create a vector
vec[2]  # Access the second element
v1 <- c(1, 2, 3, 4, 5)  # Manual creation
v2 <- c(1:100)  # Sequence from 1 to 100
```

### Sequence and Repetition
```r
v3 <- seq(from=0, to=20, by=5)  # Sequence from 0 to 20 with step 5
v3 <- seq(0, 20, 5)  # Equivalent sequence
rep(c(1, 2, 3), times=2)  # Repeat the sequence twice
rep(c(1, 2, 3), each=2)  # Repeat each element twice
rep(c(1, 2, 3), times=2, each=3)  # Repeat each element three times
```

### Combining and Accessing Elements
```r
v6 <- c(rep(1, 2), seq(5, 9, 2), 10)  # Combine repeated values and sequence
v7 <- c(1:10)  # Create a vector
v8 <- v7[2:9]  # Slice vector from index 2 to 9
v8 <- v7[c(-1, -10)]  # Exclude first and last elements
v8 <- v7[c(-1, -length(v7))]  # Exclude last element
```

### Mathematical Operations on Vectors
```r
v9 <- sqrt(v7[6:7])  # Square root of specific elements
```

### Directory Operations
```r
length(dir())  # Length of files in the current directory
dir()[1]  # First file in the directory
```

## Named Vectors
```r
genes <- c("gene1", "gene2", "gene3", "gene4")  # Gene names
gene <- paste0(rep("Gene", 4), seq(1, 4, 1))  # Generate gene names
genelength <- c(100, 3000, 200, 1000)  # Gene lengths
expression <- c(4, 5, 6, 7)  # Expression values
names(genelength) <- genes  # Assign names to genelength
```

### Filtering and Logical Indexing
```r
max(genelength)  # Maximum gene length
which.max(genelength)  # Index of maximum gene length
expression[genelength > 100 & expression > 5]  # Filter expression
which(genelength > 10 & expression > 5)  # Index of filtered genes
```

## Lists
```r
list1 <- list(30, "gene1", F)  # Mixed data types
list2 <- list(p53=30, tnf=20, "gene", T)  # Named list
list2[[1]]  # Access by position
list2$p53  # Access by name
```

## Matrices
```r
A <- matrix(nrow=2, ncol=3, c(1, 2, 3, 4, 5, 6))  # Create matrix
cbind(expression, genelength)  # Combine vectors column-wise
```

### Matrix Operations
```r
matrix1 <- cbind(expression, genelength)  # Combine vectors
row.names(matrix1) <- genes  # Assign row names
matrix1[1, ]  # Access first row
matrix1[, 2]  # Access second column
lne <- matrix1[, 1] / matrix1[, 2]  # Element-wise division
matrix2 <- cbind(matrix1, lne)  # Add new column
matrix2[matrix2[, 2] > 200, ]  # Filter rows based on condition
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, -2]  # Exclude column
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, c(1, 3)]  # Select specific columns
```

### Dimensions
```r
dim(matrix2)  # Dimensions of matrix
```

## Data Frames
```r
organism <- c("human", "cat", "dog")  # Organisms
chromc <- c(23, 12, 15)  # Chromosome counts
multicell <- c(T, T, F)  # Multicellularity
df1 <- data.frame(organism, chromc, multicell)  # Create data frame
```

### Gene Data Frame
```r
gene_names <- c("BRCA1", "TP53", "EGFR", "MYC")  # Gene names
ensembl_ids <- c("ENSG00000012048", "ENSG00000141510", "ENSG00000146648", "ENSG00000136997")  # IDs
pathways <- c("DNA repair", "Cell cycle", "Signal transduction", "Cell proliferation")  # Pathways
gene_lengths <- c(81189, 20791, 19025, 7372)  # Gene lengths
gene_expression <- c(12.5, 18.3, 10.8, 25.7)  # Expression values
genes_data <- data.frame(
  GeneName = gene_names,
  EnsemblID = ensembl_ids,
  Pathway = pathways,
  Length = gene_lengths,
  Expression = gene_expression
)
```

### Merging Data Frames
```r
ensembl_ids_new <- c("ENSG00000012048", "ENSG00000146648", "ENSG00000251562", "ENSG00000284733")  # New IDs
gene_lengths_new <- c(81189, 19025, 15000, 12450)  # New lengths
genes_data_new <- data.frame(
  EnsemblID = ensembl_ids_new,
  Length = gene_lengths_new
)

ensembl_ids_third <- c("ENSG00000012048", "ENSG00000136997", "ENSG00000354053", "ENSG00000354541")  # Third set of IDs
gene_lengths_third <- c(81189, 7372, 22000, 18500)  # Third set of lengths
genes_data_third <- data.frame(
  EnsemblID = ensembl_ids_third,
  Length = gene_lengths_third
)

merg1 <- merge(genes_data, genes_data_new, by="EnsemblID")  # Merge by EnsemblID
merg1 <- merge(genes_data, genes_data_new, by.x=2, by.y=1)  # Merge with different columns
merged <- merge(merg1, genes_data_third, by="EnsemblID")  # Merge three data frames
colnames(merg1)[c(4, 6)] <- c("length1", "length2")  # Rename columns
merg1$lne <- merg1[, 5] / merg1[, 4]  # Calculate ratio
merg1$lne2 <- merg1[, 5] / merg1[, 6]  # Ratio with second length

# Fold change calculation
merged$foldchange <- log2(merged$lne) - log2(merged$lne2)  # Log2 fold change
```

### Summation
```r
sum(merg1[merg1$Pathway == "Signal transduction", 4])  # Sum for specific pathway
```

## Comparison Table

| Feature           | Vector                      | List                                | Data Frame                            | Matrix                              |
|-------------------|-----------------------------|-------------------------------------|---------------------------------------|-------------------------------------|
| **Data Type**    | Homogeneous (same type)    | Heterogeneous (different types)    | Heterogeneous (columns)              | Homogeneous (same type)            |
| **Structure**    | 1D                         | 1D (collection of objects)         | 2D (rows and columns)                | 2D (rows and columns)              |
| **Indexing**     | Single dimensional (e.g., `[i]`) | Element-wise or by name (e.g., `[[i]]` or `$name`) | Column-wise and row-wise (e.g., `[i, j]`) | Element-wise (e.g., `[i, j]`)      |
| **Flexibility**  | Limited                    | Highly flexible                    | Optimized for tabular data           | Optimized for numerical operations |
| **Usage**        | Simple data storage        | Group related but diverse data     | Statistical or relational data       | Mathematical or numerical data     |
