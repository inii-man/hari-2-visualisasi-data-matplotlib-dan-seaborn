# 📊 Cheatsheet: Matplotlib & Seaborn

Referensi cepat untuk visualisasi data dengan Python.

---

## 📦 Import Libraries

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

# Setup
plt.style.use('default')
sns.set_theme(style='whitegrid')
%matplotlib inline  # For Jupyter
```

---

## 🎨 MATPLOTLIB

### Basic Figure Setup

```python
# Single plot
plt.figure(figsize=(10, 6))

# Multiple subplots
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12, 10))

# Subplot dengan index
plt.subplot(2, 2, 1)  # 2 rows, 2 cols, position 1
```

### Line Plot

```python
# Basic line plot
plt.plot(x, y)

# With styling
plt.plot(x, y,
         color='blue',           # Warna
         linewidth=2,            # Ketebalan garis
         linestyle='-',          # Style: '-', '--', '-.', ':'
         marker='o',             # Marker: 'o', 's', '^', 'D'
         markersize=8,           # Ukuran marker
         label='Data 1')         # Label untuk legend

# Multiple lines
plt.plot(x, y1, label='Line 1')
plt.plot(x, y2, label='Line 2')
plt.legend()
```

### Bar Chart

```python
# Vertical bar
plt.bar(categories, values,
        color='skyblue',
        alpha=0.7,
        edgecolor='black',
        width=0.6)

# Horizontal bar
plt.barh(categories, values)

# Grouped bar
width = 0.35
x = np.arange(len(labels))
plt.bar(x - width/2, values1, width, label='Group 1')
plt.bar(x + width/2, values2, width, label='Group 2')

# Stacked bar
plt.bar(x, values1, label='Group 1')
plt.bar(x, values2, bottom=values1, label='Group 2')
```

### Scatter Plot

```python
# Basic scatter
plt.scatter(x, y)

# With styling
plt.scatter(x, y,
           s=50,              # Size
           c=colors,          # Colors (array or single)
           alpha=0.6,         # Transparency
           cmap='viridis',    # Colormap
           edgecolors='black',
           marker='o')

# Add colorbar
scatter = plt.scatter(x, y, c=z, cmap='viridis')
plt.colorbar(scatter, label='Values')
```

### Customization

```python
# Titles dan Labels
plt.title('Title', fontsize=14, fontweight='bold')
plt.xlabel('X Label', fontsize=12)
plt.ylabel('Y Label', fontsize=12)

# Legend
plt.legend(loc='best',           # Location: 'best', 'upper right', etc.
          title='Legend Title',
          fontsize=10)

# Grid
plt.grid(True, alpha=0.3, linestyle='--')

# Axis limits
plt.xlim(0, 10)
plt.ylim(0, 100)

# Rotate labels
plt.xticks(rotation=45)

# Tight layout (prevent overlap)
plt.tight_layout()

# Save figure
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
```

### Colors

```python
# Named colors
colors = ['red', 'blue', 'green', 'orange', 'purple']

# Hex colors
color = '#FF6B6B'

# RGB tuple
color = (0.2, 0.4, 0.8)

# Colormaps
'viridis', 'plasma', 'inferno', 'magma', 'cividis'
'Reds', 'Blues', 'Greens', 'YlOrRd', 'RdYlBu'
'coolwarm', 'bwr', 'seismic'
```

---

## 🌊 SEABORN

### Setup

```python
# Set theme
sns.set_theme(style='whitegrid')  # 'darkgrid', 'white', 'dark', 'ticks'

# Set context
sns.set_context('notebook')  # 'paper', 'notebook', 'talk', 'poster'

# Set palette
sns.set_palette('Set2')
```

### Distribution Plots

```python
# Histogram
sns.histplot(data=df, x='column', bins=20, kde=True)

# With hue
sns.histplot(data=df, x='column', hue='category',
            multiple='stack')  # 'stack', 'dodge', 'layer'

# KDE Plot
sns.kdeplot(data=df, x='column', fill=True)

# Multiple KDE
sns.kdeplot(data=df, x='column', hue='category')

# Box Plot
sns.boxplot(data=df, x='category', y='value', palette='Set2')

# Violin Plot
sns.violinplot(data=df, x='category', y='value', inner='quartile')

# Swarm Plot (untuk data kecil)
sns.swarmplot(data=df, x='category', y='value')

# Combined
sns.boxplot(data=df, x='category', y='value')
sns.swarmplot(data=df, x='category', y='value',
             color='black', alpha=0.5, size=3)
```

### Relational Plots

```python
# Scatter plot
sns.scatterplot(data=df, x='x', y='y', hue='category',
               size='value', alpha=0.6)

# Line plot
sns.lineplot(data=df, x='x', y='y', hue='category')

# Regression plot
sns.regplot(data=df, x='x', y='y',
           scatter_kws={'alpha': 0.5},
           line_kws={'color': 'red'})
```

### Categorical Plots

```python
# Count plot
sns.countplot(data=df, x='category', palette='Set2')

# Bar plot (dengan agregasi otomatis)
sns.barplot(data=df, x='category', y='value',
           estimator=np.mean, ci=None)

# Point plot
sns.pointplot(data=df, x='category', y='value', hue='group')

# Strip plot
sns.stripplot(data=df, x='category', y='value')
```

### Matrix Plots

```python
# Heatmap
sns.heatmap(data,
           annot=True,           # Show numbers
           fmt='.2f',            # Number format
           cmap='coolwarm',      # Colormap
           center=0,             # Center value
           square=True,          # Square cells
           linewidths=0.5,       # Cell borders
           cbar_kws={'label': 'Values'})

# Heatmap dengan mask (triangle)
mask = np.triu(np.ones_like(corr, dtype=bool))
sns.heatmap(corr, mask=mask, annot=True)

# Clustermap
sns.clustermap(data, annot=True, cmap='coolwarm')
```

### Multi-plot Grids

```python
# Pair Plot
sns.pairplot(df, hue='category', diag_kind='kde')

# FacetGrid
g = sns.FacetGrid(df, row='var1', col='var2', height=4)
g.map(sns.histplot, 'value')
g.set_titles(row_template='{row_name}', col_template='{col_name}')
g.set_axis_labels('X Label', 'Y Label')

# Joint Plot
sns.jointplot(data=df, x='x', y='y', kind='reg')
# kind: 'scatter', 'kde', 'hist', 'hex', 'reg', 'resid'
```

### Color Palettes

```python
# Qualitative (categories)
'Set1', 'Set2', 'Set3', 'Paired', 'tab10'

# Sequential (ordered)
'Blues', 'Greens', 'Reds', 'YlOrRd', 'YlGnBu'

# Diverging (centered)
'coolwarm', 'RdBu', 'RdYlBu', 'RdYlGn'

# Seaborn palettes
'deep', 'muted', 'pastel', 'bright', 'dark', 'colorblind'

# Custom palette
my_palette = sns.color_palette("husl", 8)
sns.set_palette(my_palette)
```

---

## 📊 COMMON PATTERNS

### Load dan Explore Data

```python
# Load CSV
df = pd.read_csv('data.csv')

# Basic info
df.head()
df.info()
df.describe()

# Check missing values
df.isnull().sum()

# Data types
df.dtypes
```

### Data Aggregation

```python
# Group by single column
df.groupby('category')['value'].sum()

# Group by multiple columns
df.groupby(['cat1', 'cat2'])['value'].mean()

# Multiple aggregations
df.groupby('category').agg({
    'value1': 'sum',
    'value2': 'mean',
    'value3': ['min', 'max']
})

# Pivot table
df.pivot_table(values='value',
              index='row_var',
              columns='col_var',
              aggfunc='mean')
```

### Correlation Analysis

```python
# Correlation matrix
corr = df.corr()

# Heatmap
sns.heatmap(corr, annot=True, cmap='coolwarm', center=0)

# Top correlations
corr_pairs = corr.unstack()
top_corr = corr_pairs[corr_pairs < 1.0].sort_values(ascending=False)
```

### Time Series

```python
# Convert to datetime
df['date'] = pd.to_datetime(df['date'])

# Extract components
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
df['dayofweek'] = df['date'].dt.dayofweek

# Resample
df.set_index('date').resample('M')['value'].sum()

# Plot
plt.plot(df['date'], df['value'])
plt.gcf().autofmt_xdate()  # Auto format dates
```

### Dashboard Layout

```python
# 2x2 Dashboard
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle('Dashboard Title', fontsize=16)

# Access subplots
axes[0, 0].plot(x, y1)
axes[0, 1].bar(categories, values)
axes[1, 0].scatter(x, y)
axes[1, 1].pie(sizes, labels=labels)

plt.tight_layout()
```

---

## 🎯 QUICK DECISION GUIDE

| Goal                             | Best Plot Type         |
| -------------------------------- | ---------------------- |
| Show trend over time             | Line plot              |
| Compare categories               | Bar chart              |
| Show distribution                | Histogram, Box plot    |
| Show relationship between 2 vars | Scatter plot           |
| Show correlation matrix          | Heatmap                |
| Compare multiple distributions   | Violin plot, Box plot  |
| Show composition                 | Pie chart, Stacked bar |
| Explore multiple variables       | Pair plot              |
| Show frequency                   | Histogram              |
| Detect outliers                  | Box plot               |

---

## 💡 TIPS & TRICKS

### Performance

```python
# Sample large datasets
df_sample = df.sample(1000, random_state=42)

# Reduce points in line plot
plt.plot(x[::10], y[::10])  # Every 10th point
```

### Styling

```python
# Use with statement for temporary style
with plt.style.context('seaborn-v0_8'):
    plt.plot(x, y)

# Set global font size
plt.rcParams['font.size'] = 12

# Set figure DPI
plt.rcParams['figure.dpi'] = 100
```

### Common Errors

```python
# Fix overlapping labels
plt.xticks(rotation=45)
plt.tight_layout()

# Fix legend outside plot
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')

# Close figures to free memory
plt.close('all')
```

### Export Options

```python
# High quality PNG
plt.savefig('plot.png', dpi=300, bbox_inches='tight')

# Vector format (scalable)
plt.savefig('plot.pdf', bbox_inches='tight')
plt.savefig('plot.svg', bbox_inches='tight')

# Transparent background
plt.savefig('plot.png', transparent=True)
```

---

## 🔧 TROUBLESHOOTING

| Problem              | Solution                                            |
| -------------------- | --------------------------------------------------- |
| Labels overlap       | `plt.xticks(rotation=45)` atau `plt.tight_layout()` |
| Legend blocks data   | `plt.legend(loc='best')` atau `bbox_to_anchor`      |
| Plot too small       | `plt.figure(figsize=(12, 8))`                       |
| Colors not distinct  | Use colorblind-friendly palettes                    |
| Too many data points | Sample data atau use alpha transparency             |
| Memory issues        | Close figures: `plt.close('all')`                   |

---

## 📚 RESOURCES

- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html)
- [Seaborn Gallery](https://seaborn.pydata.org/examples/index.html)
- [Python Graph Gallery](https://www.python-graph-gallery.com/)
- [Matplotlib Cheatsheet](https://matplotlib.org/cheatsheets/)
- [Seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)

---

**💡 Remember:** Practice makes perfect! Experiment with different parameters and styles to find what works best for your data.

**Happy Plotting! 📊✨**
