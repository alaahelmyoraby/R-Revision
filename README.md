# Table of Contents
# 1. Basic Operations
# 2. Vectors
# 3. Lists
# 4. Matrices
# 5. Data Frames
# 6. Merging Data Frames
# 7. Comparison Table

# 1. Basic Operations
x <- 12 + 2  # Simple addition operation
# Mean of two
mean_value <- mean(c(5, 6))  # Calculating mean of two numbers
hist(c(5, 6, 7, 8, 9))  # Creating a histogram of values
sqrt(16)  # Square root of 16
min(5, 2, 3, 9)  # Minimum value among the given numbers

# 2. Vectors
# Single dimension, same type of data
vec <- c(1, 2, 3, 4, 56)  # Creating a vector
vec[2]  # Accessing the second element of the vector

# Create vectors
v1 <- c(1, 2, 3, 4, 5)  # Vector with specific values
v2 <- c(1:100)  # Sequence from 1 to 100
v3 <- seq(from = 0, to = 20, by = 5)  # Sequence from 0 to 20 with steps of 5
v3 <- seq(0, 20, 5)  # Alternative way to create the sequence
rep(c(1, 2, 3), times = 2)  # Repeating values twice
rep(c(1, 2, 3), each = 2)  # Repeating each value twice
rep(c(1, 2, 3), times = 2, each = 3)  # Repeating each value three times and the whole sequence twice

v6 <- c(rep(1, 2), seq(5, 9, 2), 10)  # Combination of repeated values and sequences
v7 <- c(1:10)  # Sequence from 1 to 10
v8 <- v7[2:9]  # Subset from index 2 to 9
v8 <- v7[c(-1, -10)]  # Excluding the first and last elements
v8 <- v7[c(-1, -length(v7))]  # Another way to exclude the first and last elements
v9 <- sqrt(v7[6:7])  # Square root of selected elements

length(dir())  # Number of files in the current directory
dir()[1]  # First file in the current directory

# Named vector
genes <- c("gene1", "gene2", "gene3", "gene4")  # Vector of gene names
gene <- paste0(rep("Gene", 4), seq(1, 4, 1))  # Generating names dynamically
genelength <- c(100, 3000, 200, 1000)  # Lengths of genes
expression <- c(4, 5, 6, 7)  # Expression levels of genes
names(genelength) <- genes  # Assigning names to genelength vector

max(genelength)  # Maximum value in genelength
which.max(genelength)  # Index of the maximum value
expression[genelength > 100 & expression > 5]  # Values meeting multiple conditions
which(genelength > 10 & expression > 5)  # Indices meeting the conditions

genelist <- c("gene1", "gene2", "gene3", "gene4")  # First list of genes
secondgenelist <- c("gene5", "gene4")  # Second list of genes
logicalindx <- genelist %in% secondgenelist  # Logical index for overlapping elements
unique(genelist[logicalindx])  # Unique overlapping elements

# 3. Lists
list1 <- list(30, "gene1", FALSE)  # List with heterogeneous data types
list2 <- list(p53 = 30, tnf = 20, "gene", TRUE)  # Named list with mixed data\list2[[1]]  # Accessing the first element of the list
list2$p53  # Accessing the named element 'p53'

# 4. Matrices
A <- matrix(nrow = 2, ncol = 3, c(1, 2, 3, 4, 5, 6))  # Creating a 2x3 matrix
cbind(expression, genelength)  # Combining vectors into a matrix by columns

# Type checks
typeof(gene)  # Data type of 'gene'
class(gene)  # Class of 'gene'
typeof(A)  # Data type of matrix 'A'
class(A)  # Class of matrix 'A'

matrix1 <- cbind(expression, genelength)  # Combining vectors into a matrix
row.names(matrix1) <- genes  # Assigning row names to the matrix
matrix1[1, ]  # Accessing the first row
matrix1[, 2]  # Accessing the second column
lne <- matrix1[, 1] / matrix1[, 2]  # Calculating a ratio for each row
matrix2 <- cbind(matrix1, lne)  # Adding the ratio as a new column
matrix2[matrix2[, 2] > 200, ]  # Rows where the second column is greater than 200
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, -2]  # Subset of rows with conditions, excluding the second column
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, c(1, 3)]  # Subset of rows and selected columns

dim(matrix2)  # Dimensions of the matrix

# 5. Data Frames
organism <- c("human", "cat", "dog")  # Vector of organism names
chromc <- c(23, 12, 15)  # Vector of chromosome counts
multicell <- c(TRUE, TRUE, FALSE)  # Vector indicating multicellularity
df1 <- data.frame(organism, chromc, multicell)  # Creating a data frame

gene_names <- c("BRCA1", "TP53", "EGFR", "MYC")  # Gene names
ensembl_ids <- c("ENSG00000012048", "ENSG00000141510", "ENSG00000146648", "ENSG00000136997")  # Ensembl IDs
pathways <- c("DNA repair", "Cell cycle", "Signal transduction", "Cell proliferation")  # Pathways
gene_lengths <- c(81189, 20791, 19025, 7372)  # Gene lengths
gene_expression <- c(12.5, 18.3, 10.8, 25.7)  # Gene expression levels
genes_data <- data.frame(
  GeneName = gene_names,
  EnsemblID = ensembl_ids,
  Pathway = pathways,
  Length = gene_lengths,
  Expression = gene_expression
)  # Creating a data frame with gene data

# 6. Merging Data Frames
ensembl_ids_new <- c("ENSG00000012048", "ENSG00000146648", "ENSG00000251562", "ENSG00000284733")  # New Ensembl IDs
gene_lengths_new <- c(81189, 19025, 15000, 12450)  # Corresponding lengths
genes_data_new <- data.frame(
  EnsemblID = ensembl_ids_new,
  Length = gene_lengths_new
)  # Creating a new data frame

ensembl_ids_third <- c("ENSG00000012048", "ENSG00000136997", "ENSG00000354053", "ENSG00000354541")  # Another set of IDs
gene_lengths_third <- c(81189, 7372, 22000, 18500)  # Corresponding lengths
genes_data_third <- data.frame(
  EnsemblID = ensembl_ids_third,
  Length = gene_lengths_third
)  # Creating a third data frame

merg1 <- merge(genes_data, genes_data_new, by = "EnsemblID")  # Merging the first two data frames by EnsemblID
merg1 <- merge(genes_data, genes_data_new, by.x = 2, by.y = 1)  # Merging with custom column matching
merged <- merge(merg1, genes_data_third, by = "EnsemblID")  # Adding the third data frame to the merge
colnames(merg1)[c(4, 6)] <- c("length1", "length2")  # Renaming columns in the merged data frame
merg1$lne <- merg1[, 5] / merg1[, 4]  # Calculating a new column based on division
merg1$lne1 <- merg1[, 5] / merg1[, 4]  # Another calculation (duplicate)
merg1$lne2 <- merg1[, 5] / merg1[, 6]  # Division with a different column

mean(as.numeric(merged[1, c(7:8)]))  # Calculating mean for specific columns
merged$foldchange <- log2(merged$lne) - log2(merged$lne2)  # Fold change calculation
sum(merg1[merg1$Pathway == "Signal transduction", 4])  # Summing values for a specific pathway

# 7. Comparison Table
comparison_table <- data.frame(
  Property = c("Data Type", "Dimension", "Homogeneity", "Indexing"),
  Vector = c("Any", "1D", "Homogeneous", "Numeric"),
  Matrix = c("Numeric/Character", "2D", "Homogeneous", "[row, column]"),
  List = c("Any", "1D", "Heterogeneous", "[[index]]"),
  DataFrame = c("Any", "2D", "Heterogeneous", "[row, column]")
)
print(comparison_table)  # Printing the comparison table
