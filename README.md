# R-Revision
```markdown
# R Operations and Data Structures

This README provides examples of various mathematical operations and R data structures, such as vectors, matrices, lists, and data frames. It also includes a comparison table to highlight the differences between these data structures.

## Math Operations and Vector Operations

### Basic Math Operations
```r
x = 12 + 2  # Addition operation

# Square root and minimum value
sqrt(16)  # Square root of 16
min(5, 2, 3, 9)  # Minimum value in the vector
```

### Histogram of Numeric Data
```r
hist(c(5, 6, 7, 8, 9))  # Histogram of numeric values
```

### Vector Creation and Operations
```r
# A vector is a one-dimensional structure of the same data type
vec <- c(1, 2, 3, 4, 56)  # Define a numeric vector
vec[2]  # Access the second element in the vector
```

### Creating Vectors with Sequences
```r
v1 <- c(1, 2, 3, 4, 5)  # Simple numeric vector
v2 <- c(1:100)  # Sequence from 1 to 100
v3 <- seq(from = 0, to = 20, by = 5)  # Sequence with a step size of 5
v3 = seq(0, 20, 5)  # Alternative way to define the same sequence
```

### Replicating Values in Vectors
```r
rep(c(1, 2, 3), times = 2)  # Repeat the entire vector twice
rep(c(1, 2, 3), each = 2)  # Repeat each element twice
rep(c(1, 2, 3), times = 2, each = 3)  # Repeat each element 3 times, then repeat the entire sequence
```

### Combining Operations in Vectors
```r
v6 <- c(rep(1, 2), seq(5, 9, 2), 10)  # Mix of repetitions and sequences
```

### Vector Indexing
```r
v7 <- c(1:10)  # Vector from 1 to 10
v8 = v7[2:9]  # Extract elements from the 2nd to the 9th
v8 = v7[c(-1, -10)]  # Exclude the 1st and 10th elements
v8 <- v7[c(-1, -length(v7))]  # Exclude the 1st and the last elements
```

### Mathematical Operations on Vector Elements
```r
v9 = sqrt(v7[6:7])  # Square root of elements 6 and 7
```

## Matrices

### Creating a Matrix
```r
A <- matrix(nrow = 2, ncol = 3, c(1, 2, 3, 4, 5, 6))  # Define a 2x3 matrix
```

### Combining Vectors into a Matrix
```r
cbind(expression, genelength)  # Combine vectors into a matrix
```

### Matrix Operations
```r
matrix1 = cbind(expression, genelength)  # Create a matrix
row.names(matrix1) = genes  # Assign row names
```

### Accessing Elements in a Matrix
```r
matrix1[1, ]  # First row
matrix1[, 2]  # Second column
```

### Adding New Columns to a Matrix
```r
lne = matrix1[, 1] / matrix1[, 2]  # Calculate length-to-expression ratio
matrix2 = cbind(matrix1, lne)  # Add the ratio as a new column
```

### Conditional Indexing in Matrices
```r
matrix2[matrix2[, 2] > 200, ]  # Rows where the second column is >200
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, -2]  # Rows meeting both conditions, excluding column 2
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, c(1, 3)]  # Select specific columns meeting conditions
```

### Matrix Dimensions
```r
dim(matrix2)  # Dimensions of the matrix
```

## Data Frames

### Creating a Data Frame
```r
organism = c("human", "cat", "dog")  # Organism names
chromc = c(23, 12, 15)  # Chromosome counts
multicell = c(T, T, F)  # Multicellular status
df1 = data.frame(organism, chromc, multicell)  # Create a data frame
```

### Creating and Merging Gene Data Frames
```r
gene_names <- c("BRCA1", "TP53", "EGFR", "MYC")  # Gene names
ensembl_ids <- c("ENSG00000012048", "ENSG00000141510", "ENSG00000146648", "ENSG00000136997")  # Ensembl IDs
pathways <- c("DNA repair", "Cell cycle", "Signal transduction", "Cell proliferation")  # Pathways
gene_lengths <- c(81189, 20791, 19025, 7372)  # Gene lengths
gene_expression <- c(12.5, 18.3, 10.8, 25.7)  # Gene expression values

genes_data <- data.frame(  # Create the main gene data frame
  GeneName = gene_names,
  EnsemblID = ensembl_ids,
  Pathway = pathways,
  Length = gene_lengths,
  Expression = gene_expression
)
```

### Merging Data Frames
```r
# Merge by EnsemblID
merg1 = merge(genes_data, genes_data_new, by = "EnsemblID")  
# Merge using different columns
merg1 = merge(genes_data, genes_data_new, by.x = 2, by.y = 1)  
# Merge with a third data frame
merged = merge(merg1, genes_data_third, by = "EnsemblID")
```

### Renaming Columns and Calculating Ratios
```r
colnames(merg1)[c(4, 6)] = c("length1", "length2")
merg1$lne = merg1[, 5] / merg1[, 4]
merg1$lne1 = merg1[, 5] / merg1[, 4]
merg1$lne2 = merg1[, 5] / merg1[, 6]
```

### Summing Values Based on Conditions
```r
sum(merg1[merg1$Pathway == "Signal transduction", 4])  # Sum of a specific pathway's length
```

## Comparison Table: Vectors, Matrices, and Data Frames

| **Feature**           | **Vector**                               | **Matrix**                                 | **Data Frame**                               |
|-----------------------|------------------------------------------|--------------------------------------------|----------------------------------------------|
| **Dimensionality**     | 1D                                        | 2D                                         | 2D                                           |
| **Structure**          | Single row/column                        | Rows and columns                           | Columns with different types of data         |
| **Data Type**          | Homogeneous                              | Homogeneous                                 | Heterogeneous                                |
| **Accessing Elements** | Single index                             | Two indices                                | Rows and columns with indices                |
| **Operations**         | Element-wise                             | Matrix operations (e.g., multiplication)    | Row/column-wise operations                   |
| **Creation**           | `c(1,2,3)`                               | `matrix()`                                 | `data.frame()`                               |
| **Example**            | `c(1,2,3)`                               | `matrix(1:6, nrow = 2, ncol = 3)`           | `data.frame(ID = 1:3, Name = c("A", "B", "C"))` |
```

This README provides a complete overview of mathematical operations and how vectors, matrices, and data frames differ in R. You can save this as a `.md` file to use in a GitHub repository or a personal project.
