# 📊 Complete R Visualization Guide: Base R & ggplot2

## 🎯 Learning Objectives

By the end of this guide, you will be able to:

1. Create and customize charts using **Base R** and **ggplot2**
2. Understand key **parameters** and their functions
3. Choose the **appropriate chart type** for your data
4. Apply **memory techniques** to retain syntax and concepts

---

## 🧠 1. Understanding R's Two Visualization Systems

| System | Description | Best For | Learning Curve |
|--------|-------------|----------|----------------|
| **Base R** | Built-in functions (`barplot()`, `hist()`, `plot()`) | Quick exploration, data checks | Low - immediate results |
| **ggplot2** | Grammar of Graphics framework, layered approach | Publication-quality visuals, reports | Moderate - powerful when mastered |

💡 **Mental Model**: Base R = quick sketches, ggplot2 = polished artwork

---

## 📊 2. Chart Types & When to Use Them

### 🔹 Bar Chart
**Purpose**: Compare frequencies or counts across categories

**Base R**
```r
barplot(table(demo$Occupation),
        main = "Occupation Distribution",
        xlab = "Occupation",
        ylab = "Count",
        col = "skyblue",
        border = "blue")
```

**ggplot2**
```r
ggplot(demo, aes(x = Occupation)) +
  geom_bar(fill = "skyblue", color = "blue") +
  labs(title = "Occupation Distribution",
       x = "Occupation",
       y = "Count") +
  theme_minimal()
```

**Key Parameters**

| Parameter | Base R | ggplot2 | Purpose | Memory Tip |
|-----------|--------|---------|---------|------------|
| Title | `main=` | `labs(title=)` | Names the chart | **Main = Main title** |
| Axis labels | `xlab=`, `ylab=` | `labs(x=, y=)` | Identifies variables | **X-label, Y-label** |
| Fill color | `col=` | `fill=` | Interior color | **Fill fills inside** |
| Border | `border=` | `color=` | Outline color | **Color = outline** |

---

### 🔹 Pie Chart
**Purpose**: Show proportions of a whole (best with few categories)

**Base R**
```r
pie(table(demo$Sex),
    main = "Sex Distribution",
    col = c("pink", "lightblue"))
```

**ggplot2**
```r
ggplot(demo, aes(x = "", fill = Sex)) +
  geom_bar(width = 1) +
  coord_polar("y") +
  labs(title = "Sex Distribution") +
  theme_void()
```

⚠️ **Note**: Pie charts work best with 2-5 categories. For more categories, use bar charts.

---

### 🔹 Histogram
**Purpose**: Display distribution of continuous numeric data

**Base R**
```r
hist(demo$Age,
     breaks = 5,
     freq = TRUE,
     main = "Age Distribution",
     xlab = "Age (years)",
     col = "lightgreen",
     border = "white")
```

**ggplot2**
```r
ggplot(demo, aes(x = Age)) +
  geom_histogram(binwidth = 5, fill = "lightgreen", color = "black") +
  labs(title = "Age Distribution",
       x = "Age (years)",
       y = "Count") +
  theme_light()
```

**Critical Parameters**

| Parameter | Base R | ggplot2 | Function | Memory Tip |
|-----------|--------|---------|----------|------------|
| Bin control | `breaks=` | `binwidth=` | Sets interval width | **Breaks = bins** |
| Count type | `freq=TRUE/FALSE` | `aes(y=..density..)` | Frequency vs density | **Freq = frequency** |

---

### 🔹 Boxplot
**Purpose**: Compare distributions, show median, quartiles, and outliers

**Base R**
```r
boxplot(Age ~ Sex, data = demo,
        main = "Age by Sex",
        xlab = "Sex",
        ylab = "Age (years)",
        col = c("pink", "lightblue"))
```

**ggplot2**
```r
ggplot(demo, aes(x = Sex, y = Age, fill = Sex)) +
  geom_boxplot() +
  labs(title = "Age by Sex",
       x = "Sex",
       y = "Age (years)") +
  theme_classic()
```

**Formula Syntax**: `Y ~ X` means "Y by X" or "Y split by groups in X"

💡 **Why boxplots?** They reveal distribution shape, central tendency, spread, and outliers in one view.

---

### 🔹 Line Chart
**Purpose**: Show trends over time or ordered sequences

**Base R**
```r
months <- c("Jan", "Feb", "Mar", "Apr", "May")
sales <- c(200, 240, 300, 280, 350)

plot(months, sales,
     type = "o",  # "o" = overlaid points and lines
     main = "Monthly Sales Trend",
     xlab = "Month",
     ylab = "Sales ($)",
     col = "blue",
     pch = 16)
```

**ggplot2**
```r
sales_data <- data.frame(
  month = c("Jan", "Feb", "Mar", "Apr", "May"),
  sales = c(200, 240, 300, 280, 350)
)

ggplot(sales_data, aes(x = month, y = sales, group = 1)) +
  geom_line(color = "blue", size = 1.2) +
  geom_point(color = "red", size = 3) +
  labs(title = "Monthly Sales Trend",
       x = "Month",
       y = "Sales ($)") +
  theme_minimal()
```

**Line Parameters**

| Parameter | Values | Purpose | Memory Tip |
|-----------|--------|---------|------------|
| `type=` | "p", "l", "o", "b" | Points, lines, both | **O = Overlap** |
| `pch=` | 0-25 | Point shape | **pch = Point CHaracter** |
| `lty=` | 1-6 | Line type (solid, dashed) | **lty = Line TYpe** |
| `lwd=` | numeric | Line thickness | **lwd = Line WiDth** |

---

### 🔹 Scatter Plot
**Purpose**: Examine relationships between two numeric variables

**Base R**
```r
plot(demo$Age, jitter(as.numeric(demo$Occupation)),
     main = "Age vs Occupation",
     xlab = "Age",
     ylab = "Occupation",
     col = "purple",
     pch = 19)
```

**ggplot2**
```r
ggplot(demo, aes(x = Age, y = as.numeric(Occupation))) +
  geom_point(color = "purple", size = 3, alpha = 0.6) +
  geom_smooth(method = "lm", se = FALSE, color = "red") +
  labs(title = "Age vs Occupation",
       x = "Age",
       y = "Occupation (Numeric)") +
  theme_bw()
```

**Adding Trend Lines**

- Base R: `abline(lm(y ~ x))`
- ggplot2: `geom_smooth(method = "lm")`

💡 **Memory**: "abline adds a line"

---

## 🎨 3. Essential Parameters Reference

### Titles & Labels

| Feature | Base R | ggplot2 | Purpose | Mnemonic |
|---------|--------|---------|---------|----------|
| Main title | `main="Title"` | `labs(title="Title")` | Chart heading | **Main = Main** |
| X-axis label | `xlab="Label"` | `labs(x="Label")` | Horizontal axis | **X-Label** |
| Y-axis label | `ylab="Label"` | `labs(y="Label")` | Vertical axis | **Y-Label** |
| Subtitle | — | `labs(subtitle="")` | Additional context | — |
| Caption | — | `labs(caption="")` | Data source | — |

🧠 **Chant**: "Main – X – Y: Every chart needs these three!"

---

### Colors & Aesthetics

| Element | Base R | ggplot2 | Function | Mnemonic |
|---------|--------|---------|----------|----------|
| Fill color | `col=` | `fill=` | Interior color | **Fill fills inside** |
| Border/line | `border=` | `color=` | Outline color | **Color = outline** |
| Transparency | — | `alpha=` | 0 = transparent, 1 = opaque | **Alpha = opacity** |
| Point shape | `pch=` | `shape=` | Marker style | **pch = Point CHaracter** |
| Line type | `lty=` | `linetype=` | Line pattern | **lty = Line TYpe** |
| Line width | `lwd=` | `size=` | Thickness | **lwd = Line WiDth** |

🧠 **Remember**: "Color outside, Fill inside"

---

### Axes & Scale Control

| Function | Base R | ggplot2 | Purpose | Mnemonic |
|----------|--------|---------|---------|----------|
| Axis limits | `xlim=c(min,max)`, `ylim=` | `coord_cartesian(xlim=, ylim=)` | Focus range | **Limit = range** |
| Flip axes | — | `coord_flip()` | Horizontal bars | **Flip = swap** |
| Percentage scale | Manual | `scale_y_continuous(labels=scales::percent)` | Format as % | **Scale = rescale** |
| Log scale | `log="x"` or `log="y"` | `scale_x_log10()` | Logarithmic axis | — |

🧠 **Chant**: "Limit – Label – Flip"

---

### Data Mapping (ggplot2 specific)

| Concept | Syntax | Purpose | Mnemonic |
|---------|--------|---------|----------|
| Map variables | `aes(x=, y=, fill=, color=)` | Connect data to visuals | **AES = Assign Every Symbol** |
| Side-by-side bars | `position="dodge"` | Compare groups | **Dodge = move aside** |
| Stacked bars | `position="stack"` | Show totals | **Stack = pile up** |
| 100% stacked | `position="fill"` | Show proportions | **Fill = fill to 100%** |

🧠 **Key concept**: `aes()` is the heart of ggplot2 — it maps data to visual properties.

---

### Binning & Frequency

| Function | Base R | ggplot2 | Purpose | Mnemonic |
|----------|--------|---------|---------|----------|
| Histogram bins | `breaks=5` | `binwidth=5` | Control detail | **Breaks = bins** |
| Frequency | `freq=TRUE` | default | Show counts | **Freq = frequency** |
| Density | `freq=FALSE` | `aes(y=..density..)` | Normalized distribution | — |
| Count table | `table(x)` | — | Frequency table | **Table counts** |
| Proportion | `prop.table(table(x))` | — | Percentages | **Prop proportions** |

🧠 **Remember**: "Table counts, Prop proportions"

---

### Themes & Layout

| Feature | Base R | ggplot2 | Purpose | Mnemonic |
|---------|--------|---------|---------|----------|
| Background style | Manual | `theme_minimal()`, `theme_light()`, `theme_bw()`, `theme_classic()` | Visual tone | **Theme = tone** |
| Split by group | Multiple plots | `facet_wrap(~ variable)` | Compare subgroups | **Facet = focus** |
| Grid layout | `par(mfrow=c(2,2))` | `facet_grid(row ~ col)` | Arrange plots | — |
| Legend | `legend("topright", ...)` | Auto-generated | Explain colors | **Legend = logic** |

🧠 **Chant**: "Theme for tone, Facet for focus, Legend for logic"

---

### Annotations & Enhancements

| Element | Base R | ggplot2 | Purpose | Mnemonic |
|---------|--------|---------|---------|----------|
| Trend line | `abline(lm(y ~ x))` | `geom_smooth(method="lm")` | Show relationship | **Line = trend** |
| Text labels | `text(x, y, "label")` | `geom_text(aes(label=))` | Annotate points | **Label = explanation** |
| Table totals | `addmargins(table(...))` | — | Add row/col totals | **Margin = totals** |
| Horizontal line | `abline(h=value)` | `geom_hline(yintercept=)` | Reference line | — |
| Vertical line | `abline(v=value)` | `geom_vline(xintercept=)` | Reference line | — |

🧠 **Remember**: "Line – Label – Margin: The 3 L's of explanation"

---

## 🔄 4. Complete Parameter Comparison Table

| Feature | Base R | ggplot2 | Purpose |
|---------|--------|---------|---------|
| Title | `main="Title"` | `labs(title="Title")` | Chart heading |
| X-axis label | `xlab="X"` | `labs(x="X")` | Horizontal axis name |
| Y-axis label | `ylab="Y"` | `labs(y="Y")` | Vertical axis name |
| Fill color | `col="blue"` | `fill="blue"` | Interior color |
| Border color | `border="black"` | `color="black"` | Outline color |
| Transparency | — | `alpha=0.7` | See-through effect |
| Point shape | `pch=19` | `shape=19` | Marker style |
| Line type | `lty=2` | `linetype="dashed"` | Line pattern |
| Line width | `lwd=2` | `size=2` | Line thickness |
| X-axis limits | `xlim=c(0,100)` | `coord_cartesian(xlim=c(0,100))` | Focus range |
| Y-axis limits | `ylim=c(0,100)` | `coord_cartesian(ylim=c(0,100))` | Focus range |
| Flip axes | — | `coord_flip()` | Horizontal orientation |
| Histogram bins | `breaks=10` | `binwidth=5` | Interval width |
| Side-by-side bars | `beside=TRUE` | `position="dodge"` | Compare groups |
| Stacked bars | `beside=FALSE` | `position="stack"` | Show totals |
| Theme | Manual styling | `theme_minimal()` etc. | Visual style |
| Faceting | Multiple plots | `facet_wrap(~ var)` | Split by category |
| Legend | `legend("topright", ...)` | Auto + `labs(fill=)` | Explain symbols |

---

## 🧠 5. Memory Techniques Summary

### Core Mnemonics

| Concept | Mnemonic | Meaning |
|---------|----------|---------|
| **Essential labels** | Main – X – Y | Always include these three |
| **Color logic** | Color outside, Fill inside | Outline vs interior |
| **Axis control** | Limit – Label – Flip | Scale management |
| **ggplot mapping** | AES = Assign Every Symbol | Core of ggplot2 |
| **Data scale** | Table counts, Prop proportions | Frequency vs percentage |
| **Layout** | Theme for tone, Facet for focus, Legend for logic | Style, split, explain |
| **Annotation** | Line – Label – Margin | Add meaning |

### Parameter Categories

**COLORS**: Color outside, Fill inside
- `color` = outlines and borders
- `fill` = interior areas

**LABELS**: Main – X – Y
- `main` / `labs(title=)` = title
- `xlab` / `labs(x=)` = x-axis
- `ylab` / `labs(y=)` = y-axis

**GROUPING**: AES = Assign Every Symbol
- `aes()` connects data columns to visual properties
- `position=` controls how groups appear

**THEMES**: Theme for tone, Facet for focus, Legend for logic
- `theme_*()` = overall style
- `facet_wrap()` = split by categories
- Legend = auto-generated explanation

---

## 🧑‍🏫 6. Teaching Strategy

### Step 1: Start with Base R
- Show simple commands with immediate results
- Explain each parameter slowly: "This controls color, this controls labels"
- Let students modify one thing at a time

### Step 2: Transition to ggplot2
- Explain the layered structure: `ggplot(data) + aes() + geom_*() + theme()`
- Show the same chart in both systems side-by-side
- Emphasize that concepts are the same, syntax differs

### Step 3: Demonstrate Parallels
- Use comparison tables to show equivalents
- Point out: "See? `main=` in Base R is `labs(title=)` in ggplot2"

### Step 4: Encourage Exploration
- Provide datasets and ask students to:
  - Change colors
  - Modify bin widths
  - Add titles and labels
  - Try different themes

### Step 5: Reinforce with Mnemonics
- Chant together in class:
  > "Main – X – Y! Color outside, Fill inside! AES = Assign Every Symbol!"
- Create flashcards with mnemonics on one side, parameters on the other

---

## 🎯 7. Common Mistakes & How to Avoid Them

| Mistake | Why It Happens | Solution | Prevention |
|---------|----------------|----------|------------|
| Missing labels | Forget to add titles/labels | Charts lack context | Always use "Main – X – Y" |
| Wrong color parameter | Confuse `col` vs `fill` | Colors don't appear | Remember: "Color outside, Fill inside" |
| Misleading scales | Don't set axis limits | Data appears distorted | Always check with "Limit – Label – Flip" |
| Too many bins | Default breaks too small | Histogram too noisy | Experiment with `breaks=` or `binwidth=` |
| No grouping | Forget `aes(fill=)` | Groups not distinguished | Use "AES = Assign Every Symbol" |
| Cluttered legend | Too many categories | Hard to read | Consider faceting instead |

---

## 📊 8. Practice Exercises

### Exercise 1: Basic Bar Chart
Create a bar chart showing counts of a categorical variable with:
- A descriptive title
- Labeled axes
- Custom colors

### Exercise 2: Distribution Analysis
Make a histogram of a numeric variable:
- Experiment with different bin widths
- Add appropriate labels
- Try both frequency and density

### Exercise 3: Group Comparison
Create a boxplot comparing a numeric variable across groups:
- Use color to distinguish groups
- Add clear labels
- Interpret quartiles and outliers

### Exercise 4: Trend Visualization
Build a line chart showing change over time:
- Add points and lines
- Use appropriate colors
- Label axes with units

### Exercise 5: Relationship Exploration
Make a scatter plot of two numeric variables:
- Add a trend line
- Use transparency for overlapping points
- Include correlation in title

---

## 🏁 9. Key Takeaways

### Base R
- ✅ **Fast**: Immediate results with simple syntax
- ✅ **Built-in**: No installation needed
- ✅ **Exploratory**: Perfect for quick data checks
- ⚠️ **Limited**: Harder to create complex, polished visuals

### ggplot2
- ✅ **Powerful**: Highly customizable and flexible
- ✅ **Consistent**: Same structure for all chart types
- ✅ **Professional**: Publication-ready output
- ⚠️ **Learning curve**: Requires understanding of layered grammar

### Universal Principles
1. **Always label**: Main – X – Y
2. **Use color wisely**: Color outside, Fill inside
3. **Control scale**: Limit – Label – Flip
4. **Map thoughtfully**: AES = Assign Every Symbol
5. **Style appropriately**: Theme for tone

---

## 📚 10. Quick Reference: Common Tasks

### Change Chart Type
```r
# Base R
barplot()    # Bar chart
hist()       # Histogram
boxplot()    # Box plot
plot()       # Scatter or line

# ggplot2
geom_bar()       # Bar chart
geom_histogram() # Histogram
geom_boxplot()   # Box plot
geom_point()     # Scatter
geom_line()      # Line chart
```

### Add Colors
```r
# Base R
col = "blue"          # Fill
border = "black"      # Outline

# ggplot2
fill = "blue"         # Fill
color = "black"       # Outline
alpha = 0.7           # Transparency
```

### Control Axes
```r
# Base R
xlim = c(0, 100)
ylim = c(0, 50)

# ggplot2
coord_cartesian(xlim = c(0, 100), ylim = c(0, 50))
coord_flip()  # Horizontal bars
```

### Apply Themes
```r
# ggplot2 only
theme_minimal()   # Clean, minimal
theme_classic()   # Traditional look
theme_bw()        # Black & white
theme_light()     # Light gray
```

---

## 🎓 Conclusion

Mastering R visualization requires understanding:

1. **When** to use each chart type
2. **What** each parameter controls
3. **Why** proper styling matters
4. **How** to remember syntax with mnemonics

Practice regularly, experiment with parameters, and always ask: "Does my chart clearly communicate the data's story?"

**Remember the golden rule**: "Main – X – Y, Color outside Fill inside, AES Assign Every Symbol!"

Happy visualizing! 📊✨
