#uni
```python
import matplotlib.pyplot as plt

plt.plot([1,2,3,4], [1,4,9,16])
plt.title("Simple Plot")
plt.xlabel("X axis")
plt.ylabel("Y axis")
plt.show()
```
# Anatomy
- Major tick
- minor tick
- major tick label
- line
- markers (scatter plot) `plt.scatter(, c= 'blue', marker='o')`
- legend
- grid
- spines (bordo)
- figure
# Matplotlib visualization
A matplotlib visualization consists of:
- figure: the overall window or page that contains everything
- axes: an area where data is plotted with a particular coordinate system
```python
fig, ax = plt.subplots() # Create a figure and an axes
ax.plot([1, 2, 3, 4], [1, 4, 9, 16])
ax.set_title("Using Object-Oriented API")
ax.set_xlabel("X axis")
ax.set_ylabel("Y axis")
plt.show()
```
# Basic plots
```python
# Line plot
plt.plot([1, 2, 3, 4], [1, 4, 9, 16], 'r-') # red line
# Scatter plot
plt.scatter([1, 2, 3, 4], [1, 4, 9, 16], c='blue', marker='o')
# Bar chart
plt.bar(['A', 'B', 'C', 'D'], [1, 4, 9, 16])
# Histogram
plt.hist([1, 1, 2, 3, 3, 3, 4, 4, 4, 4], bins=20)
```
# Custom plot appearance
```python
x = [1, 2, 3, 4]
y = [1, 4, 16, 9]
x_pos = 2 + 0.1
y_pos = 4
# Line styles, colors, and markers
plt.plot(x, y, 'g--', linewidth=2, markersize=5)
# Adding grid
plt.grid(True, linestyle='--'
, alpha=0.7)
# Custom colors
plt.plot(x, y, color='#FF8C00') # Dark orange
# Text and annotations
plt.text(x_pos, y_pos, "Important point!")
plt.annotate("Peak", xy=(3, 16), xytext=(3, 12),
			arrowprops=dict(facecolor='black', shrink=0.05))
```
# Multiple subplots
```python
# 2x2 grid of subplots
fig, axs = plt.subplots(2, 2, figsize=(10, 8))
# Plot on each subplot
axs[0, 0].plot(x, y)
axs[0, 0].set_title('Plot 1')
axs[0, 1].scatter(x, y)
axs[0, 1].set_title('Plot 2')
axs[1, 0].bar(x, y)
axs[1, 0].set_title('Plot 3')
axs[1, 1].hist(y)
axs[1, 1].set_title('Plot 4')
# Adjust spacing between subplots
plt.tight_layout()
```
# Advanced customization
```python
import numpy as np
data = np.random.rand(32,32)
# Custom styles
plt.style.use('seaborn-v0_8-whitegrid')
# Setting a global theme
plt.rcParams['font.family'] = 'serif'
plt.rcParams['font.size'] = 12
plt.rcParams['axes.grid'] = True
# Colormaps for complex visualizations
plt.imshow(data, cmap='viridis')
plt.colorbar()
```
# Saving figures
```python
# Save as PNG (raster image)
plt.savefig('my_plot.png', dpi=300)
# Save as PDF (vector image)
plt.savefig('my_plot.pdf')
# Save as SVG (vector image for web)
plt.savefig('my_plot.svg')
# Controlling figure size and resolution
plt.figure(figsize=(10, 6)) # Width, height in inches
plt.plot(x, y)
plt.savefig('high_quality.png', dpi=300, bbox_inches='tight')
```