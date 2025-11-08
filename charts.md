# R Charts: From Basic to Professional

A comprehensive guide for teaching data visualization in R.

---

## 1. Why We Use Charts

Tables show precise numbers, but **charts** help visualize:
- **Patterns** in the data
- **Distributions** of values
- **Relationships** between variables
- **Trends** over time

This makes insights immediately visible and easier to communicate.

### Two Main Approaches in R:
- **Base R graphics** → Built-in functions (`plot()`, `barplot()`, `hist()`)
- **ggplot2 package** → Professional, highly customizable plots

---

## 2. Base R Charts (Built-in Functions)

Let's start with simple example data:

```r
# Example data
age <- c(18, 19, 20, 21, 22, 23, 24)
students <- c(5, 8, 10, 15, 12, 9, 6)
```

---

### 2.1 Bar Plot

**Purpose:** Compare categorical data

```r
barplot(students,
        names.arg = age,
        main = "Number of Students by Age",
        xlab = "Age",
        ylab = "Count",
        col = "skyblue",
        border = "blue")
```

**Key Parameters:**
- `barplot(height, ...)` – creates bars for each value
- `names.arg` – labels for x-axis
- `main` – chart title
- `xlab`, `ylab` – axis labels
- `col` – bar fill color
- `border` – outline color

---

### 2.2 Pie Chart

**Purpose:** Show proportions or percentages

```r
pie(students,
    labels = age,
    main = "Students by Age",
    col = rainbow(length(age)))
```

**Key Parameters:**
- `x` – numeric vector of values
- `labels` – category names
- `col` – colors (try `rainbow()`, `heat.colors()`, or custom colors)
- `main` – chart title

---

### 2.3 Histogram

**Purpose:** Show distribution of continuous data

```r
heights <- c(150, 155, 160, 165, 170, 175, 180, 185, 190)
hist(heights,
     main = "Height Distribution",
     xlab = "Height (cm)",
     col = "lightgreen",
     border = "darkgreen",
     breaks = 5)
```

**Key Parameters:**
- `x` – numeric vector
- `breaks` – number of bins (controls granularity)
- `freq` – if `TRUE`, shows counts; if `FALSE`, shows density
- `col`, `border` – styling options

**Use case:** Understanding how data values are spread or concentrated

---

### 2.4 Boxplot

**Purpose:** Show summary statistics (median, quartiles, outliers)

```r
scores <- c(80, 85, 70, 90, 75, 88, 92, 60)
boxplot(scores,
        main = "Score Distribution",
        ylab = "Score",
        col = "lightpink")
```

**Comparing Groups:**

```r
group <- c(rep("A", 4), rep("B", 4))
boxplot(scores ~ group, 
        main = "Scores by Group", 
        col = c("lightblue", "lightgreen"))
```

**Use case:** Comparing distributions across different categories

---

### 2.5 Line Chart

**Purpose:** Show trends over time or ordered categories

```r
months <- c("Jan", "Feb", "Mar", "Apr", "May")
sales <- c(200, 240, 300, 280, 350)

plot(months, sales,
     type = "o",           # 'o' = both points and lines
     main = "Monthly Sales Trend",
     xlab = "Month",
     ylab = "Sales ($)",
     col = "blue",
     pch = 16)             # solid circle points
```

**Key Parameters:**
- `type` – "p" (points only), "l" (lines only), "b" (both), "o" (overplotted)
- `col` – color
- `pch` – point style (16 = solid circle, 17 = triangle, etc.)
- `lty` – line type (1 = solid, 2 = dashed, etc.)
- `lwd` – line width

---

### 2.6 Scatter Plot

**Purpose:** Visualize relationship between two continuous variables

```r
weight <- c(60, 65, 70, 75, 80, 85)
height <- c(155, 160, 165, 170, 175, 180)

plot(weight, height,
     main = "Height vs Weight",
     xlab = "Weight (kg)",
     ylab = "Height (cm)",
     col = "purple",
     pch = 19)
```

**Adding a Regression Line:**

```r
abline(lm(height ~ weight), col = "red", lwd = 2)
```

**Use case:** Examining correlation between variables

---

## 3. Chart Customization in Base R

### 3.1 Common Customization Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `main` | Chart title | `"My Chart"` |
| `xlab`, `ylab` | Axis labels | `"X Axis"`, `"Y Axis"` |
| `col` | Color of elements | `"red"`, `rainbow(5)` |
| `pch` | Point symbol | `pch=19` (solid circle) |
| `lty` | Line type | `lty=2` (dashed) |
| `lwd` | Line width | `lwd=2` |
| `xlim`, `ylim` | Axis ranges | `xlim=c(0,100)` |
| `cex` | Size of text/points | `cex=1.5` |
| `las` | Axis label orientation | `las=2` (perpendicular) |

---

### 3.2 Adding a Legend

```r
plot(weight, height, col = "blue", pch = 16)
points(weight, height + 5, col = "red", pch = 17)
legend("topleft",
       legend = c("Group 1", "Group 2"),
       col = c("blue", "red"),
       pch = c(16, 17))
```

**Legend positions:** `"topleft"`, `"topright"`, `"bottomleft"`, `"bottomright"`, `"center"`

---

## 4. Professional Charts with ggplot2

`ggplot2` is the **industry standard** for creating publication-quality visualizations in R.

### 4.1 Installation and Setup

```r
install.packages("ggplot2")   # run once
library(ggplot2)
```

### Sample Data

```r
df <- data.frame(
  gender = c("M", "F", "M", "F", "M", "F"),
  score  = c(80, 90, 75, 88, 92, 85),
  group  = c("A", "A", "B", "B", "A", "B")
)
```

---

### 4.2 Bar Chart in ggplot2

```r
ggplot(df, aes(x = gender, fill = group)) +
  geom_bar(position = "dodge") +
  labs(title = "Count by Gender and Group",
       x = "Gender",
       y = "Count") +
  theme_minimal()
```

**The ggplot2 Grammar:**
- `ggplot(df, aes(...))` – define dataset and aesthetic mappings
- `geom_bar()` – add bar layer
- `fill` – color bars by category
- `position = "dodge"` – place bars side-by-side
- `labs()` – add labels
- `theme_minimal()` – apply clean theme

---

### 4.3 Histogram

```r
ggplot(df, aes(x = score, fill = gender)) +
  geom_histogram(bins = 5, alpha = 0.7, color = "black") +
  labs(title = "Score Distribution") +
  theme_light()
```

**Parameters:**
- `bins` – number of intervals
- `alpha` – transparency (0 = transparent, 1 = opaque)
- `fill` – bar fill color
- `color` – outline color

---

### 4.4 Boxplot

```r
ggplot(df, aes(x = gender, y = score, fill = gender)) +
  geom_boxplot() +
  labs(title = "Scores by Gender") +
  theme_classic()
```

**Advantage:** Easy comparison of distributions across multiple categories

---

### 4.5 Scatter Plot with Regression Line

```r
ggplot(df, aes(x = score, y = as.numeric(group))) +
  geom_point(color = "blue", size = 3) +
  geom_smooth(method = "lm", se = FALSE, col = "red") +
  labs(title = "Score vs Group (Linear Fit)",
       x = "Score",
       y = "Group") +
  theme_bw()
```

**Components:**
- `geom_point()` – scatter plot layer
- `geom_smooth(method = "lm")` – add regression line
- `se = FALSE` – hide confidence interval
- `theme_bw()` – black-and-white theme

---

### 4.6 Line Chart

```r
sales_data <- data.frame(
  month = c("Jan", "Feb", "Mar", "Apr", "May"),
  sales = c(200, 240, 300, 280, 350)
)

ggplot(sales_data, aes(x = month, y = sales, group = 1)) +
  geom_line(color = "blue", size = 1.2) +
  geom_point(color = "red", size = 3) +
  labs(title = "Monthly Sales Trend") +
  theme_minimal()
```

**Note:** `group = 1` is needed when x-axis is categorical

---

### 4.7 Saving Charts

```r
ggsave("sales_chart.png", width = 6, height = 4, dpi = 300)
```

**Parameters:**
- `width`, `height` – dimensions in inches
- `dpi` – resolution (300 for publication quality)

---

## 5. Popular ggplot2 Themes

```r
theme_minimal()    # Clean, minimal design
theme_classic()    # Traditional look with axes
theme_bw()         # Black and white
theme_dark()       # Dark background
theme_light()      # Light gray background
theme_void()       # Completely blank
```

---

## 6. Teaching Tips and Best Practices

| Concept | Example | Teaching Goal |
|---------|---------|---------------|
| **Match chart type to data type** | Categorical → bar chart; Continuous → histogram | Help students choose appropriate visualizations |
| **Start with base R** | Quick exploratory plots | Build fundamental understanding |
| **Progress to ggplot2** | Professional, publication-ready graphics | Teach layered grammar of graphics |
| **Always label axes and add titles** | Use `labs()` or `main`, `xlab`, `ylab` | Develop good visualization habits |
| **Encourage experimentation** | Try different colors, themes, point types | Build intuition through practice |
| **Explain aesthetics mapping** | `aes(x = ..., y = ..., color = ...)` | Core concept in ggplot2 |
| **Show real-world examples** | Use meaningful datasets | Increase engagement and relevance |

---

## 7. Common Chart Selection Guide

| Data Type | Question | Recommended Chart |
|-----------|----------|-------------------|
| Categorical | How many in each category? | Bar chart |
| Categorical | What proportion of whole? | Pie chart |
| Continuous | How is data distributed? | Histogram or density plot |
| Continuous | What are the summary statistics? | Boxplot |
| Two continuous | Is there a relationship? | Scatter plot |
| Time series | How does it change over time? | Line chart |
| Comparing groups | How do groups differ? | Boxplot or grouped bar chart |
