# 📘 COURSE MODULES: **Data Visualization in R (Base R vs ggplot2)**

---

## 🟦 **Module 1: Introduction to Data Visualization in R**

### 🎯 Learning Objectives

* Understand why we visualize data.
* Know the two main visualization systems in R.
* Load and prepare data for plotting.

### 🧠 Key Concepts

* Visualization = turning numbers into stories.
* R has two main plotting systems:

  * **Base R graphics** (built-in, simple)
  * **ggplot2** (advanced, grammar of graphics)

### 🧩 Practical Steps

```r
# Load packages
library(tidyverse)

# Example dataset
demo <- data.frame(
  Occupation = c("Farmer", "Teacher", "Trader", "Student", "Farmer"),
  Sex = c("M", "F", "F", "M", "F"),
  Age = c(25, 29, 22, 19, 35),
  Education = c("Primary", "Secondary", "Tertiary", "Secondary", "Primary")
)
```

### 💬 Teaching Notes

Explain:

* **Base R** = Quick sketches (use for exploration).
* **ggplot2** = Structured layering (use for presentation).

**Mnemonic:**

> “Base R is fast and simple. ggplot2 is flexible and beautiful.”

### 🧑‍💻 Student Tasks

* Load your own dataset with `read.csv()` or `read_excel()`.
* Use `str()` and `glimpse()` to inspect it.

---

## 🟩 **Module 2: Chart Fundamentals and Parameters**

### 🎯 Learning Objectives

* Understand what chart parameters are.
* Learn how to label, color, and style charts.
* Know parameter equivalents in Base R vs ggplot2.

### 🧠 Key Parameters

| Purpose      | Base R          | ggplot2                 | Mnemonic                   |
| ------------ | --------------- | ----------------------- | -------------------------- |
| Title        | `main`          | `labs(title=)`          | Main = main title          |
| Axis labels  | `xlab`, `ylab`  | `labs(x=, y=)`          | Label axes                 |
| Color        | `col`, `border` | `fill`, `color`         | Color outside, Fill inside |
| Scale limits | `xlim`, `ylim`  | `coord_cartesian()`     | Limit = range              |
| Themes       | —               | `theme_minimal()`, etc. | Theme = tone               |

### 💬 Teaching Notes

* Explain how each parameter changes the chart’s look.
* Use one chart and adjust parameters step by step.

### 🧩 Example (Bar Chart)

**Base R**

```r
barplot(table(demo$Occupation),
        main = "Occupation Distribution",
        xlab = "Occupation",
        ylab = "Count",
        col = "skyblue")
```

**ggplot2**

```r
ggplot(demo, aes(x = Occupation)) +
  geom_bar(fill = "skyblue") +
  labs(title = "Occupation Distribution",
       x = "Occupation",
       y = "Count") +
  theme_minimal()
```

### 🧠 Mnemonic Drill

> “**Main–X–Y**: every chart needs these three.”
> “**Color outside, Fill inside.**”

### 🧑‍💻 Student Tasks

* Change bar colors and titles.
* Flip the axis (`coord_flip()` in ggplot2).
* Add labels using `text()` or `geom_text()`.

---

## 🟨 **Module 3: Chart Types – Understanding and Practice**

### 🎯 Learning Objectives

* Learn major chart types and when to use them.
* Create them in both Base R and ggplot2.
* Interpret what each chart tells us.

---

### 🔹 **3.1 Bar Chart**

**Use:** Compare categories.

**Base R**

```r
barplot(table(demo$Occupation),
        col="lightblue", main="Occupation Distribution")
```

**ggplot2**

```r
ggplot(demo, aes(x=Occupation)) + geom_bar(fill="lightblue")
```

---

### 🔹 **3.2 Pie Chart**

**Use:** Show proportions (for few categories).

**Base R**

```r
pie(table(demo$Sex), main="Sex Distribution", col=c("pink","lightblue"))
```

**ggplot2**

```r
ggplot(demo, aes(x="", fill=Sex)) + geom_bar(width=1) + coord_polar("y")
```

---

### 🔹 **3.3 Histogram**

**Use:** Show numeric distributions.

**Base R**

```r
hist(demo$Age, breaks=5, col="green", main="Age Distribution")
```

**ggplot2**

```r
ggplot(demo, aes(x=Age)) + geom_histogram(binwidth=5, fill="green", color="black")
```

---

### 🔹 **3.4 Boxplot**

**Use:** Compare distributions between groups.

**Base R**

```r
boxplot(Age ~ Sex, data=demo, col=c("pink","lightblue"))
```

**ggplot2**

```r
ggplot(demo, aes(x=Sex, y=Age, fill=Sex)) + geom_boxplot()
```

---

### 🔹 **3.5 Line Chart**

**Use:** Trends over time.

**Base R**

```r
plot(months, sales, type="o", col="blue", main="Sales Trend")
```

**ggplot2**

```r
ggplot(data, aes(x=month, y=sales, group=1)) + geom_line()
```

---

### 🔹 **3.6 Scatter Plot**

**Use:** Relationship between two numeric variables.

**Base R**

```r
plot(demo$Age, jitter(as.numeric(demo$Occupation)), col="purple", pch=19)
```

**ggplot2**

```r
ggplot(demo, aes(x=Age, y=as.numeric(Occupation))) + geom_point(color="purple")
```

---

### 🧠 Mnemonics Recap

| Concept         | Mnemonic                                              | Meaning              |
| --------------- | ----------------------------------------------------- | -------------------- |
| Titles & Labels | **Main–X–Y**                                          | Always label chart   |
| Colors          | **Color outside, Fill inside**                        | Outline vs interior  |
| Axes            | **Limit–Label–Flip**                                  | Scale control        |
| Grouping        | **AES = Assign Every Symbol**                         | ggplot2 data mapping |
| Layout          | **Theme for tone, Facet for focus, Legend for logic** | Style structure      |

---

### 🧑‍💻 Student Exercises

1. Create each chart type for your dataset.
2. Add titles and axis labels.
3. Change colors and try `theme_light()` or `theme_bw()`.
4. Compare Base R vs ggplot2 results.

---

## 🟧 **Module 4: Customization and Advanced Features**

### 🎯 Learning Objectives

* Enhance charts with annotations and themes.
* Learn how to group, facet, and style charts.
* Use mnemonics for quick recall.

### 🧠 Key Functions

| Feature         | Base R         | ggplot2                         | Purpose           |
| --------------- | -------------- | ------------------------------- | ----------------- |
| Add lines       | `abline()`     | `geom_smooth()`                 | Add trend lines   |
| Add text        | `text()`       | `geom_text()`                   | Label points      |
| Themes          | Manual         | `theme_minimal()`, `theme_bw()` | Style chart       |
| Split by groups | Multiple plots | `facet_wrap(~ variable)`        | Compare subgroups |
| Legend          | `legend()`     | Auto / `labs(fill=)`            | Explain colors    |

### 💬 Mnemonic

> “**Theme for tone, Facet for focus, Legend for logic.**”

### 🧩 Example

```r
ggplot(demo, aes(x=Occupation, fill=Sex)) +
  geom_bar(position="dodge") +
  facet_wrap(~Education) +
  labs(title="Occupation by Sex and Education") +
  theme_light()
```

---

## 🟥 **Module 5: Putting It All Together**

### 🎯 Learning Objectives

* Combine learned parameters and chart types.
* Choose the right chart for the right message.
* Prepare charts for presentations or reports.

### 🧩 Integrated Example

```r
ggplot(demo, aes(x=Sex, y=Age, fill=Education)) +
  geom_boxplot() +
  facet_wrap(~Occupation) +
  labs(title="Age by Sex and Education Across Occupations",
       x="Sex", y="Age (years)") +
  theme_minimal()
```

### 💬 Discussion

* Ask: What does this visualization show?
* Which parameters control its style?
* How could we improve clarity?

### 🧑‍💻 Student Challenge

1. Create 3 different chart types using your own dataset.
2. Add at least one title, theme, and label.
3. Save your plots using `ggsave()` or `png()` in Base R.

---

## 🟪 **Module 6: Summary & Revision**

### 🔁 Quick Review Table

| Concept        | Base R          | ggplot2                | Memory Tip                 |
| -------------- | --------------- | ---------------------- | -------------------------- |
| Title          | `main`          | `labs(title=)`         | Main = main title          |
| Axis Labels    | `xlab`, `ylab`  | `labs(x=, y=)`         | Label axes                 |
| Colors         | `col`, `border` | `fill`, `color`        | Color outside, Fill inside |
| Limits         | `xlim`, `ylim`  | `coord_cartesian()`    | Limit = visible range      |
| Group Bars     | `beside=TRUE`   | `position="dodge"`     | Dodge = move aside         |
| Histogram Bins | `breaks`        | `binwidth`             | Breaks = bins              |
| Themes         | manual          | `theme_minimal()` etc. | Theme = tone               |
| Legends        | `legend()`      | auto                   | Legend = logic             |

---

### 🧠 Mnemonics Recap (Final Drill)

> ✅ **Main–X–Y:** always label
> 🎨 **Color outside, Fill inside**
> 📏 **Limit–Label–Flip**
> 🔠 **AES = Assign Every Symbol**
> 🎭 **Theme for tone, Facet for focus, Legend for logic**
> ✍️ **Line–Label–Margin = add meaning**

---

## 🏁 Outcome

After these modules, students can:
✅ Create all common chart types.
✅ Understand and explain each parameter.
✅ Choose between Base R and ggplot2 confidently.
✅ Customize charts for professional reporting.

---

Would you like me to generate a **PDF “Instructor Pack”** version — with structured sections, color-coded tables, and space for student notes (like a workbook)?
It’s perfect for classroom teaching or self-paced study.
