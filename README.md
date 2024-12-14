# R Programming Guide

## Table of Contents
- [Math Operations](#math-operations)
- [Vectors](#vectors)
- [Lists](#lists)
- [Matrices](#matrices)
- [Data Frames](#data-frames)
- [Merging Data](#merging-data)
- [Comparison: Vectors vs Lists](#comparison-vectors-vs-lists)

---

## Math Operations
```R
x = 12 + 2
# Mean of two numbers
hist(c(5, 6, 7, 8, 9))
sqrt(16)
min(5, 2, 3, 9)
```

---

## Vectors
- Single-dimension
- Homogeneous data types (same type)
- Example:

```R
vec <- c(1, 2, 3, 4, 56)
vec[2]

# Creating vectors
v1 <- c(1, 2, 3, 4, 5)
v2 <- c(1:100)

v3 <- seq(from = 0, to = 20, by = 5)
v3 = seq(0, 20, 5)

# Repetition
rep(c(1, 2, 3), times = 2)
rep(c(1, 2, 3), each = 2)
rep(c(1, 2, 3), times = 2, each = 3) # 'each' first

# Combining repetition and sequences
v6 <- c(rep(1, 2), seq(5, 9, 2), 10)
v7 <- c(1:10)
v8 = v7[2:9]
v8 = v7[c(-1, -10)]
v8 <- v7[c(-1, -length(v7))]

v9 = sqrt(v7[6:7])
```

---

## Lists
- One-dimensional but heterogeneous data types (any type)
- Examples:

```R
list1 = list(30, "gene1", F)
list2 = list(p53 = 30, tnf = 20, "gene", T)
list2[[1]]
list2$p53
```

---

## Matrices
- Two-dimensional
- Homogeneous data types

```R
A <- matrix(nrow = 2, ncol = 3, c(1, 2, 3, 4, 5, 6))
cbind(expression, genelength)

# Matrix operations
matrix1 = cbind(expression, genelength)
row.names(matrix1) = genes
matrix1[1, ]
matrix1[, 2]

# Adding a column
lne = matrix1[, 1] / matrix1[, 2]
matrix2 = cbind(matrix1, lne)
matrix2[matrix2[, 2] > 200, ]
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, -2]
matrix2[matrix2[, 2] > 200 & matrix2[, 1] > 5, c(1, 3)]
dim(matrix2)
```

---

## Data Frames
```R
organism = c("human", "cat", "dog")
chromc = c(23, 12, 15)
multicell = c(T, T, F)
df1 = data.frame(organism, chromc, multicell)

# Gene-related data frame
genes <- c("gene1", "gene2", "gene3", "gene4")
gene <- paste0(rep("Gene", 4), seq(1, 4, 1))

genelength = c(100, 3000, 200, 1000)
expression = c(4, 5, 6, 7)
names(genelength) = genes

max(genelength)
which.max(genelength)

expression[genelength > 100 & expression > 5]         
which(genelength > 10  & expression > 5)
```

---

## Merging Data
```R
gene_names <- c("BRCA1", "TP53", "EGFR", "MYC")
ensembl_ids <- c("ENSG00000012048", "ENSG00000141510", "ENSG00000146648", "ENSG00000136997")
pathways <- c("DNA repair", "Cell cycle", "Signal transduction", "Cell proliferation")
gene_lengths <- c(81189, 20791, 19025, 7372)
gene_expression <- c(12.5, 18.3, 10.8, 25.7)  # Simulated gene expression values
genes_data <- data.frame(
  GeneName = gene_names,
  EnsemblID = ensembl_ids,
  Pathway = pathways,
  Length = gene_lengths,
  Expression = gene_expression
)

ensembl_ids_new <- c("ENSG00000012048", "ENSG00000146648", "ENSG00000251562", "ENSG00000284733")
gene_lengths_new <- c(81189, 19025, 15000, 12450)
genes_data_new <- data.frame(
  EnsemblID = ensembl_ids_new,
  Length = gene_lengths_new
)

ensembl_ids_third <- c("ENSG00000012048", "ENSG00000136997", "ENSG00000354053", "ENSG00000354541")
gene_lengths_third <- c(81189, 7372, 22000, 18500)
genes_data_third <- data.frame(
  EnsemblID = ensembl_ids_third,
  Length = gene_lengths_third
)

merg1 = merge(genes_data, genes_data_new, by = "EnsemblID")
merged = merge(merg1, genes_data_third, by = "EnsemblID")
colnames(merg1)[c(4, 6)] = c("length1", "length2")
merg1$lne = merg1[, 5] / merg1[, 4]
merg1$lne2 = merg1[, 5] / merg1[, 6]
merged$foldchange = log2(merged$lne) - log2(merged$lne2)
```

---

## Comparison: Vectors vs Lists

| Feature            | Vector                                  | List                       |
|--------------------|-----------------------------------------|----------------------------|
| Data Type          | Homogeneous (same type)                | Heterogeneous (any type)   |
| Dimensionality     | One-dimensional                        | One-dimensional            |
| Indexing           | By position (e.g., vec[2])             | By position or name        |
| Example Creation   | `c(1, 2, 3)`                           | `list(a = 1, b = "text")` |
| Use Case           | Simple data storage of same type       | Complex data combinations  |
