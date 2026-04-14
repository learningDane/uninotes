#uni 
Seaborn è una libreria di visualizzazione di dati per il [[Python]], basata su [[Matplotlib]]. Fornisce una interfaccia ad alto livello per creare grafici.

Si integra direttamente con [[Pandas]].

```bash
pip install seaborn
import seabron as sns
import matplotlib.pyplot as plt
```
# Basic plots
```python
# Load sample dataset
tips = sns.load_dataset("tips")
# Distribution plots
sns.histplot(tips["total_bill"])
sns.kdeplot(tips["total_bill"])

# Categorical plots
sns.boxplot(x="day", y="total_bill", data=tips)
sns.violinplot(x="day", y="total_bill", data=tips)
sns.barplot(x="day", y="total_bill", data=tips)

# Relationship plots
sns.scatterplot(x="total_bill", y="tip", data=tips)
sns.lineplot(x="total_bill", y="tip", data=tips)
```
# Distribution Plots
```python
# Histogram
sns.histplot(data=tips, x="total_bill", bins=20, kde=True)
# Kernel Density Estimation (KDE)
sns.kdeplot(data=tips, x="total_bill", shade=True)
# Distribution plot
sns.displot(data=tips, x="total_bill", kind="kde")
# Joint distribution of two variables
sns.jointplot(data=tips, x="total_bill", y="tip", kind="scatter")
```
# Categorical Plots
```python
# Box plot
sns.boxplot(x="day", y="total_bill", data=tips)
# Violin plot
sns.violinplot(x="day", y="total_bill", data=tips)
# Bar plot (with confidence intervals)
sns.barplot(x="day", y="total_bill", data=tips)
# Point plot (showing mean and confidence interval)
sns.pointplot(x="day", y="total_bill", data=tips)
# Count plot (like a histogram for categorical data)
sns.countplot(x="day", data=tips)
```
# Relationship Plots
```python
# Scatter plot
sns.scatterplot(x="total_bill", y="tip", data=tips)
# Line plot
sns.lineplot(x="total_bill", y="tip", data=tips)
# Regression plot (with regression line)
sns.regplot(x="total_bill", y="tip", data=tips)
# Residual plot
sns.residplot(x="total_bill", y="tip", data=tips)
```
# Matrix Plots
```python
# Correlation heatmap
corr = tips.corr()
sns.heatmap(corr, annot=True, cmap="coolwarm")
# Pairwise relationships
sns.pairplot(tips)
# Cluster map
sns.clustermap(corr, cmap="coolwarm", standard_scale=1)


# example with random matrix
feats = np.random.rand(100,100)
sns.heatmap(feats)
# example with identity matrix
ident = np.identity(100)
sns.heatmap(ident)
# example with diagonal block matrix
block_size = 10
num_blocks = 100 // block_size

# correlated random values
blocks = [np.random.rand(block_size, block_size)
	for _ in range(num_blocks)]

# block diagonal matrix
matrix = block_diag(*blocks)
sns.heatmap(matrix, annot=False)
```