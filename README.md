# R for Epidemiology - Comprehensive Guide
## Lessons 1-2: Foundation to Data Mastery

---

# LESSON 1: Introduction to R and Basic Data Exploration

## Learning Objectives
By the end of this lesson, you will be able to:
- Understand what R is and why it's valuable for epidemiological research
- Navigate the RStudio interface confidently
- Install and load essential packages for epidemiological analysis
- Understand basic R data types and structures
- Read data from various file formats commonly used in epidemiology
- Explore datasets using built-in R functions
- Calculate descriptive statistics for epidemiological variables
- Create basic visualizations to understand your data
- Generate frequency tables and cross-tabulations

---

## 1.1 What is R and Why Use It in Epidemiology?

### What is R?
R is a **free, open-source programming language** specifically designed for statistical computing and data analysis. Think of it as a powerful calculator that can handle massive datasets, perform complex statistical analyses, and create publication-quality graphs.

### Why R is Essential for Modern Epidemiology

**1. Cost-Effective Research**
- Completely free (unlike SAS, STATA, or SPSS)
- No licensing fees for institutions or students
- Democratizes access to advanced statistical tools

**2. Powerful Statistical Capabilities**
```r
# R can handle complex epidemiological analyses in just a few lines
library(epiR)
outbreak_data <- read_csv("cholera_outbreak.csv")
risk_ratio <- epi.2by2(table(outbreak_data$water_source, outbreak_data$illness))
```

**3. Reproducible Research**
- Scripts can be saved, shared, and re-run
- Ensures transparency in research methods
- Allows colleagues to verify and build upon your work
- Essential for published research in top-tier journals

**4. Specialized Epidemiological Packages**
- `epiR`: Epidemiological analysis tools
- `survival`: Survival analysis and Cox regression
- `outbreak`: Infectious disease modeling
- `EpiEstim`: Real-time epidemic curve analysis

**5. Data Visualization Excellence**
```r
# Create publication-ready epidemic curves
ggplot(outbreak_data, aes(x = symptom_date)) +
  geom_histogram(binwidth = 1, fill = "steelblue", alpha = 0.7) +
  labs(title = "Epidemic Curve: Cholera Outbreak",
       x = "Date of Symptom Onset",
       y = "Number of Cases") +
  theme_minimal()
```

**6. Large Community Support**
- Extensive online resources and tutorials
- Active epidemiology user communities
- Rapid development of new methods and packages

---

## 1.2 Introduction to RStudio Interface

RStudio is an **Integrated Development Environment (IDE)** that makes working with R much easier. Think of it as Microsoft Word for R programming.

### The Four Main Panes

#### **1. Console (Bottom Left)**
- Where you type commands and see immediate results
- Interactive area for quick calculations and testing
- Shows output, warnings, and error messages

```r
# Try typing these in the console:
2 + 2
mean(c(10, 20, 30, 40, 50))
```

#### **2. Script Editor (Top Left)**
- Where you write and save your R code
- Like a text document for your analysis
- Can run selected lines or entire scripts
- **Always work in scripts for reproducible research**

#### **3. Environment/History (Top Right)**
- **Environment tab**: Shows all your data objects and variables
- **History tab**: Records all commands you've run
- **Connections tab**: For database connections
- **Tutorial tab**: Interactive tutorials

#### **4. Files/Plots/Packages/Help (Bottom Right)**
- **Files**: Navigate your computer's file system
- **Plots**: View graphs and charts you create
- **Packages**: Install and manage R packages
- **Help**: Documentation for functions and packages
- **Viewer**: View web content and interactive plots

### Essential RStudio Shortcuts
```
Ctrl + Enter (Windows) / Cmd + Return (Mac): Run current line/selection
Ctrl + Shift + Enter: Run entire script
Ctrl + 1: Focus on script editor
Ctrl + 2: Focus on console
Tab: Auto-complete function names
F1: Get help on selected function
```

### Setting Up Your Workspace
```r
# Always start your analysis session with these steps:

# 1. Set working directory (where your files are located)
setwd("C:/Users/YourName/EpiAnalysis")  # Windows
setwd("/Users/YourName/EpiAnalysis")    # Mac

# 2. Check current working directory
getwd()

# 3. List files in current directory
list.files()

# 4. Clear environment (start fresh)
rm(list = ls())
```

---

## 1.3 Installing and Using Packages

### Understanding Packages
Packages are collections of functions that extend R's capabilities. Think of them as specialized toolboxes for different types of analysis.

### Essential Packages for Epidemiology
```r
# Core packages - install once per computer
install.packages("tidyverse")    # Data manipulation and visualization
install.packages("epiR")         # Epidemiological analysis
install.packages("readxl")       # Read Excel files
install.packages("haven")        # Read SPSS, SAS, STATA files
install.packages("lubridate")    # Work with dates and times
install.packages("epitools")     # Additional epi tools
install.packages("survival")     # Survival analysis
install.packages("table1")       # Create publication tables

# Install multiple packages at once
packages_needed <- c("tidyverse", "epiR", "readxl", "haven", 
                     "lubridate", "epitools", "survival", "table1")
install.packages(packages_needed)
```

### Loading Packages (Every Session)
```r
# Load packages at the beginning of each R session
library(tidyverse)     # Data manipulation and ggplot2
library(epiR)          # Epidemiological functions
library(readxl)        # Excel file reading
library(haven)         # SPSS/SAS/STATA files
library(lubridate)     # Date manipulation

# Alternative: Load multiple packages at once
packages_to_load <- c("tidyverse", "epiR", "readxl", "haven", "lubridate")
lapply(packages_to_load, library, character.only = TRUE)
```

### Package Management Tips
```r
# Check if package is installed
"tidyverse" %in% installed.packages()

# Update packages
update.packages()

# See all installed packages
installed.packages()

# Get help on a package
help(package = "epiR")
```

---

## 1.4 Basic R Syntax and Data Types

### R as a Calculator
```r
# Basic arithmetic
5 + 3          # Addition: 8
10 - 4         # Subtraction: 6
6 * 7          # Multiplication: 42
20 / 4         # Division: 5
2^3            # Exponentiation: 8
sqrt(16)       # Square root: 4
log(10)        # Natural logarithm
log10(100)     # Base-10 logarithm: 2
```

### Assignment and Objects
```r
# Create objects (variables) using <- or =
age <- 35
height <- 170
weight <- 70

# R is case sensitive!
Age    # This would cause an error - 'Age' doesn't exist, only 'age'

# Calculate BMI
bmi <- weight / (height/100)^2
print(bmi)  # 24.22

# You can update objects
age <- age + 1  # Now age is 36
```

### Vectors: The Building Blocks
Vectors are collections of values of the same type - the most basic data structure in R.

```r
# Numeric vectors
ages <- c(25, 30, 35, 40, 45, 50)
blood_pressure <- c(120, 130, 140, 125, 135, 145)

# Character vectors
names <- c("Alice", "Bob", "Charlie", "Diana", "Eve", "Frank")
gender <- c("Female", "Male", "Male", "Female", "Female", "Male")

# Logical vectors (TRUE/FALSE)
hypertensive <- c(FALSE, FALSE, TRUE, FALSE, TRUE, TRUE)

# Check vector properties
length(ages)        # How many elements: 6
class(ages)         # What type: "numeric"
str(ages)           # Structure: num [1:6] 25 30 35 40 45 50
```

### Vector Operations (Vectorization)
```r
# Mathematical operations work on entire vectors
ages_in_months <- ages * 12
ages_plus_10 <- ages + 10

# Logical operations
elderly <- ages >= 65
young_adults <- ages >= 18 & ages < 30

# Statistical functions
mean(ages)          # Average age: 37.5
median(ages)        # Middle value: 37.5
min(ages)           # Youngest: 25
max(ages)           # Oldest: 50
range(ages)         # Min and max: 25 50
```

### Data Frames: The Epidemiologist's Best Friend
Data frames are like Excel spreadsheets - rows represent observations (participants) and columns represent variables.

```r
# Create a data frame
study_participants <- data.frame(
  participant_id = 1:6,
  name = names,
  age = ages,
  gender = gender,
  systolic_bp = blood_pressure,
  hypertensive = hypertensive,
  stringsAsFactors = FALSE  # Keep text as text, not factors
)

# View the data frame
print(study_participants)
View(study_participants)  # Opens in a spreadsheet-like viewer

# Access specific columns
study_participants$age              # All ages
study_participants$gender           # All genders
study_participants[["systolic_bp"]] # Alternative syntax

# Access specific rows and columns
study_participants[1, ]             # First row, all columns
study_participants[, "age"]         # All rows, age column
study_participants[1:3, c("name", "age")]  # First 3 rows, name and age
```

### Factors: Categorical Variables
Factors are how R handles categorical data with specific levels.

```r
# Convert character to factor
study_participants$gender <- factor(study_participants$gender)
study_participants$gender

# Specify levels explicitly (useful for ordering)
severity <- factor(c("Mild", "Moderate", "Severe", "Mild", "Severe"),
                  levels = c("Mild", "Moderate", "Severe"))
print(severity)

# Ordered factors for ordinal data
severity_ordered <- factor(c("Mild", "Moderate", "Severe", "Mild", "Severe"),
                          levels = c("Mild", "Moderate", "Severe"),
                          ordered = TRUE)
print(severity_ordered)

# Factor properties
levels(severity)          # Show categories
nlevels(severity)         # Number of categories
table(severity)           # Frequency count
```

### Lists: Containers for Mixed Data Types
Lists can hold different types of data - useful for complex analyses.

```r
# Create a list
study_info <- list(
  study_name = "Hypertension Prevalence Study",
  n_participants = nrow(study_participants),
  data_collection_date = Sys.Date(),
  participant_data = study_participants,
  notes = c("Baseline data collection", "No missing values")
)

# Access list elements
study_info$study_name           # By name
study_info[[1]]                # By position
study_info[["participant_data"]] # Alternative syntax

# List structure
str(study_info)
```

---

## 1.5 Reading Data from Various Sources

### CSV Files (Most Common)
```r
# Base R method
data <- read.csv("study_data.csv", 
                 header = TRUE,           # First row contains column names
                 stringsAsFactors = FALSE) # Keep text as character

# Tidyverse method (recommended)
library(readr)
data <- read_csv("study_data.csv")

# Handle different delimiters
data_semicolon <- read_csv2("european_data.csv")  # Semicolon separated
data_tab <- read_tsv("tab_separated_data.txt")    # Tab separated

# Specify column types
data <- read_csv("study_data.csv",
                col_types = cols(
                  participant_id = col_character(),
                  age = col_double(),
                  gender = col_factor(),
                  date_enrolled = col_date()
                ))
```

### Excel Files
```r
library(readxl)

# Read Excel file
data <- read_excel("epidemiology_study.xlsx")

# Specify sheet
data <- read_excel("epidemiology_study.xlsx", sheet = "ParticipantData")
data <- read_excel("epidemiology_study.xlsx", sheet = 2)  # Second sheet

# Specify range
data <- read_excel("epidemiology_study.xlsx", 
                  sheet = "Data", 
                  range = "A1:F100")

# Skip rows if needed
data <- read_excel("epidemiology_study.xlsx", skip = 2)

# See sheet names
excel_sheets("epidemiology_study.xlsx")
```

### SPSS, SAS, and STATA Files
```r
library(haven)

# SPSS files (.sav)
data <- read_sav("epidemiology_data.sav")

# STATA files (.dta)
data <- read_dta("epidemiology_data.dta")

# SAS files (.sas7bdat)
data <- read_sas("epidemiology_data.sas7bdat")

# These functions preserve variable labels and value labels
attributes(data$gender)  # See SPSS labels
```

### Web Data and APIs
```r
# Read CSV from URL
url <- "https://raw.githubusercontent.com/datasets/covid-19/master/data/countries-aggregated.csv"
covid_data <- read_csv(url)

# Read data from GitHub
github_url <- "https://raw.githubusercontent.com/user/repo/main/data.csv"
data <- read_csv(github_url)
```

### Handling Common Import Issues
```r
# Missing values
data <- read_csv("data.csv", na = c("", "NA", "NULL", "Missing", "."))

# Character encoding issues
data <- read_csv("data.csv", locale = locale(encoding = "UTF-8"))

# Date formats
data <- read_csv("data.csv", 
                col_types = cols(
                  date_column = col_date(format = "%d/%m/%Y")
                ))

# Large files (show progress)
data <- read_csv("large_dataset.csv", progress = TRUE)
```

---

## 1.6 Exploring Datasets

### First Look at Your Data
```r
# Load example dataset
data(mtcars)  # Built-in R dataset
covid_data <- read_csv("covid_surveillance.csv")

# Essential exploration functions
head(covid_data)          # First 6 rows
head(covid_data, n = 10)  # First 10 rows
tail(covid_data)          # Last 6 rows
glimpse(covid_data)       # Compact overview (tidyverse)
str(covid_data)           # Structure (base R)
summary(covid_data)       # Summary statistics
```

### Understanding Data Dimensions and Structure
```r
# Data dimensions
nrow(covid_data)          # Number of rows (observations)
ncol(covid_data)          # Number of columns (variables)
dim(covid_data)           # Both dimensions: [rows, columns]
names(covid_data)         # Column names
colnames(covid_data)      # Alternative for column names
rownames(covid_data)      # Row names (usually numbers)

# Data types
class(covid_data)         # Overall class: "data.frame"
sapply(covid_data, class) # Class of each column
```

### Detailed Data Inspection
```r
# Check for missing values
sum(is.na(covid_data))                    # Total missing values
colSums(is.na(covid_data))                # Missing per column
covid_data %>% summarise_all(~sum(is.na(.))) # Tidyverse approach

# Identify complete cases
complete_cases <- complete.cases(covid_data)
sum(complete_cases)                       # Number of complete rows
covid_complete <- covid_data[complete_cases, ] # Keep only complete cases

# Look for duplicates
sum(duplicated(covid_data))               # Number of duplicate rows
covid_data[duplicated(covid_data), ]      # Show duplicate rows
```

### Variable-Specific Exploration
```r
# Numeric variables
summary(covid_data$age)
quantile(covid_data$age, probs = c(0.1, 0.25, 0.5, 0.75, 0.9))
range(covid_data$age)
IQR(covid_data$age)  # Interquartile range

# Categorical variables
table(covid_data$gender)
prop.table(table(covid_data$gender))      # Proportions
table(covid_data$gender, useNA = "always") # Include missing values

# Cross-tabulation
table(covid_data$gender, covid_data$outcome)
xtabs(~ gender + outcome, data = covid_data) # Alternative syntax
```

---

## 1.7 Descriptive Statistics for Epidemiological Data

### Measures of Central Tendency
```r
# Mean (average)
mean(covid_data$age)                      # Simple mean
mean(covid_data$age, na.rm = TRUE)        # Remove missing values
weighted.mean(covid_data$age, covid_data$weight) # Weighted mean

# Median (50th percentile)
median(covid_data$age, na.rm = TRUE)

# Mode (most frequent value) - R doesn't have built-in mode function
get_mode <- function(x) {
  unique_x <- unique(x)
  unique_x[which.max(tabulate(match(x, unique_x)))]
}
get_mode(covid_data$symptoms)
```

### Measures of Variability
```r
# Standard deviation
sd(covid_data$age, na.rm = TRUE)

# Variance
var(covid_data$age, na.rm = TRUE)

# Range
range(covid_data$age, na.rm = TRUE)
diff(range(covid_data$age, na.rm = TRUE))  # Range width

# Interquartile range (IQR)
IQR(covid_data$age, na.rm = TRUE)

# Quantiles and percentiles
quantile(covid_data$age, probs = c(0.25, 0.5, 0.75), na.rm = TRUE)
quantile(covid_data$age, probs = seq(0, 1, 0.1), na.rm = TRUE) # Deciles

# Coefficient of variation (relative variability)
cv <- sd(covid_data$age, na.rm = TRUE) / mean(covid_data$age, na.rm = TRUE)
```

### Group-wise Statistics
```r
# Using base R
aggregate(age ~ gender, data = covid_data, mean)
aggregate(age ~ gender + outcome, data = covid_data, mean)

# Using tidyverse (more flexible)
covid_data %>%
  group_by(gender) %>%
  summarise(
    n = n(),                              # Count
    mean_age = mean(age, na.rm = TRUE),
    median_age = median(age, na.rm = TRUE),
    sd_age = sd(age, na.rm = TRUE),
    min_age = min(age, na.rm = TRUE),
    max_age = max(age, na.rm = TRUE),
    .groups = "drop"
  )

# Multiple grouping variables
covid_data %>%
  group_by(gender, age_group) %>%
  summarise(
    cases = n(),
    mortality_rate = mean(outcome == "Death", na.rm = TRUE),
    avg_days_to_outcome = mean(days_to_outcome, na.rm = TRUE),
    .groups = "drop"
  )
```

### Epidemiological Summary Statistics
```r
# Incidence calculations
covid_data %>%
  group_by(exposure_group) %>%
  summarise(
    total_person_time = sum(follow_up_days),
    cases = sum(outcome == "Infected"),
    incidence_rate = cases / total_person_time * 365.25, # per person-year
    .groups = "drop"
  )

# Prevalence calculations
covid_data %>%
  summarise(
    total_tested = n(),
    positive_cases = sum(test_result == "Positive"),
    prevalence = positive_cases / total_tested,
    prevalence_percent = prevalence * 100
  )
```

---

## 1.8 Data Visualization Fundamentals

### Base R Plotting
```r
# Histogram for continuous variables
hist(covid_data$age, 
     main = "Distribution of Age in COVID Study",
     xlab = "Age (years)",
     ylab = "Frequency",
     col = "lightblue",
     breaks = 20)

# Boxplot for comparing groups
boxplot(age ~ gender, 
        data = covid_data,
        main = "Age Distribution by Gender",
        xlab = "Gender",
        ylab = "Age (years)",
        col = c("pink", "lightblue"))

# Scatter plot
plot(covid_data$age, covid_data$days_to_recovery,
     main = "Age vs Days to Recovery",
     xlab = "Age (years)",
     ylab = "Days to Recovery",
     pch = 19,  # Point style
     col = "darkblue")

# Bar chart
gender_counts <- table(covid_data$gender)
barplot(gender_counts,
        main = "Gender Distribution",
        xlab = "Gender",
        ylab = "Count",
        col = c("pink", "lightblue"))
```

### ggplot2: Grammar of Graphics (Recommended)
```r
library(ggplot2)

# Basic histogram
ggplot(covid_data, aes(x = age)) +
  geom_histogram(binwidth = 5, fill = "steelblue", alpha = 0.7) +
  labs(title = "Age Distribution in COVID Study",
       x = "Age (years)",
       y = "Count") +
  theme_minimal()

# Boxplot with better aesthetics
ggplot(covid_data, aes(x = gender, y = age, fill = gender)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("Female" = "coral", "Male" = "lightblue")) +
  labs(title = "Age Distribution by Gender",
       x = "Gender",
       y = "Age (years)") +
  theme_minimal() +
  theme(legend.position = "none")  # Remove legend (redundant)

# Scatter plot with trend line
ggplot(covid_data, aes(x = age, y = days_to_recovery)) +
  geom_point(alpha = 0.6, color = "darkblue") +
  geom_smooth(method = "lm", se = TRUE, color = "red") +
  labs(title = "Relationship between Age and Recovery Time",
       x = "Age (years)",
       y = "Days to Recovery") +
  theme_minimal()

# Bar chart
ggplot(covid_data, aes(x = gender, fill = gender)) +
  geom_bar(alpha = 0.8) +
  scale_fill_manual(values = c("Female" = "coral", "Male" = "lightblue")) +
  labs(title = "Gender Distribution",
       x = "Gender",
       y = "Count") +
  theme_minimal() +
  theme(legend.position = "none")
```

### Epidemiological Visualizations
```r
# Epidemic curve
ggplot(covid_data, aes(x = symptom_onset_date)) +
  geom_histogram(binwidth = 1, fill = "darkred", alpha = 0.7) +
  labs(title = "COVID-19 Epidemic Curve",
       x = "Date of Symptom Onset",
       y = "Number of Cases") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Age-specific attack rates
covid_data %>%
  group_by(age_group) %>%
  summarise(
    exposed = n(),
    cases = sum(infected == "Yes"),
    attack_rate = cases/exposed * 100,
    .groups = "drop"
  ) %>%
  ggplot(aes(x = age_group, y = attack_rate)) +
  geom_col(fill = "darkgreen", alpha = 0.7) +
  labs(title = "COVID-19 Attack Rate by Age Group",
       x = "Age Group",
       y = "Attack Rate (%)") +
  theme_minimal()

# Multiple outcomes by exposure
covid_data %>%
  count(exposure_status, outcome) %>%
  ggplot(aes(x = exposure_status, y = n, fill = outcome)) +
  geom_col(position = "dodge") +
  labs(title = "Outcomes by Exposure Status",
       x = "Exposure Status",
       y = "Number of Cases",
       fill = "Outcome") +
  theme_minimal()
```

---

## 1.9 Tables and Frequency Distributions

### Basic Frequency Tables
```r
# Simple frequency table
table(covid_data$gender)
table(covid_data$outcome)

# With proportions
prop.table(table(covid_data$gender))
prop.table(table(covid_data$gender)) * 100  # Percentages

# Include missing values
table(covid_data$gender, useNA = "always")
```

### Cross-tabulations (2x2 Tables)
```r
# Basic cross-tabulation
exposure_outcome <- table(covid_data$exposure, covid_data$outcome)
print(exposure_outcome)

# Add margins (totals)
addmargins(exposure_outcome)

# Row percentages
prop.table(exposure_outcome, margin = 1) * 100

# Column percentages  
prop.table(exposure_outcome, margin = 2) * 100

# Overall percentages
prop.table(exposure_outcome) * 100
```

### Advanced Tables with tidyverse
```r
# Detailed frequency table
covid_data %>%
  count(gender, outcome) %>%
  pivot_wider(names_from = outcome, values_from = n, values_fill = 0)

# Calculate percentages within groups
covid_data %>%
  group_by(exposure) %>%
  count(outcome) %>%
  mutate(percentage = n / sum(n) * 100) %>%
  select(exposure, outcome, n, percentage)

# Three-way cross-tabulation
covid_data %>%
  count(gender, age_group, outcome) %>%
  pivot_wider(names_from = outcome, values_from = n, values_fill = 0)
```

### Publication-Ready Tables
```r
library(table1)

# Descriptive table (Table 1)
table1(~ age + gender + comorbidities + symptom_severity | exposure_group, 
       data = covid_data)

# Custom labels and formatting
label(covid_data$age) <- "Age (years)"
label(covid_data$gender) <- "Gender"
label(covid_data$comorbidities) <- "Comorbidities"

table1(~ age + gender + comorbidities | exposure_group, 
       data = covid_data,
       render.continuous = c(.="Mean (SD)", .="Median (Q1, Q3)"))
```

---

# LESSON 2: Data Cleaning and Transformation

## Learning Objectives
By the end of this lesson, you will be able to:
- Apply tidy data principles to organize datasets effectively
- Identify, handle, and make decisions about missing values
- Filter datasets to focus on relevant observations
- Create new variables and recode existing ones appropriately
- Work with categorical variables and factor levels
- Reshape data between wide and long formats
- Merge multiple datasets correctly
- Handle date and time variables properly
- Create comprehensive data summaries and cross-tabulations

---

## 2.1 Tidy Data Principles

### The Foundation of Good Data Analysis
**Tidy data** follows three key principles that make analysis easier and more reliable:

1. **Each variable forms a column**
2. **Each observation forms a row**  
3. **Each type of observational unit forms a table**

### Untidy vs Tidy Data Examples

**Untidy Data (Common Problems):**
```r
# Problem 1: Multiple variables in column names
untidy_bp <- data.frame(
  patient_id = c("P001", "P002", "P003"),
  systolic_baseline = c(120, 130, 140),
  systolic_followup = c(115, 125, 135),
  diastolic_baseline = c(80, 85, 90),
  diastolic_followup = c(75, 80, 85)
)

# Problem 2: Multiple observations per row
untidy_symptoms <- data.frame(
  patient_id = c("P001", "P002"),
  symptoms = c("fever,cough,fatigue", "headache,nausea")
)

# Problem 3: Variables stored in rows
untidy_labs <- data.frame(
  patient_id = c("P001", "P001", "P002", "P002"),
  test_type = c("WBC", "Hemoglobin", "WBC", "Hemoglobin"),
  result = c(7.5, 14.2, 6.8, 13.1),
  reference_range = c("4.5-11.0", "12.0-15.5", "4.5-11.0", "12.0-15.5")
)
```

**Converting to Tidy Data:**
```r
library(tidyr)
library(dplyr)

# Fix Problem 1: Pivot longer
tidy_bp <- untidy_bp %>%
  pivot_longer(
    cols = -patient_id,
    names_to = c("measure", "time_point"),
    names_pattern = "(.+)_(.+)",
    values_to = "blood_pressure"
  ) %>%
  pivot_wider(
    names_from = measure,
    values_from = blood_pressure
  )

# Fix Problem 2: Separate symptoms
tidy_symptoms <- untidy_symptoms %>%
  separate_rows(symptoms, sep = ",") %>%
  mutate(present = TRUE) %>%
  pivot_wider(
    names_from = symptoms,
    values_from = present,
    values_fill = FALSE
  )

# Problem 3 is actually already tidy!
# Each row is one test result for one patient
```

### Why Tidy Data Matters for Epidemiology
```r
# With tidy data, analysis becomes straightforward:

# Calculate mean BP by time point
tidy_bp %>%
  group_by(time_point) %>%
  summarise(
    mean_systolic = mean(systolic, na.rm = TRUE),
    mean_diastolic = mean(diastolic, na.rm = TRUE)
  )

# Visualize BP changes
tidy_bp %>%
  pivot_longer(c(systolic, diastolic), names_to = "bp_type", values_to = "value") %>%
  ggplot(aes(x = time_point, y = value, color = bp_type, group = bp_type)) +
  geom_line() +
  geom_point() +
  facet_wrap(~bp_type)
```

---

## 2.2 Handling Missing Values: The Epidemiologist's Dilemma

Missing data is inevitable in epidemiological studies. How you handle it can significantly impact your results.

### Understanding Missing Data Types

**1. Missing Completely at Random (MCAR)**
- Missing values are random and unrelated to any variable
- Example: Equipment malfunction causing random lab result losses

**2. Missing at Random (MAR)**  
- Missing values depend on observed variables but not the missing value itself
- Example: Older participants more likely to miss follow-up visits

**3. Missing Not at Random (MNAR)**
- Missing values depend on the unobserved value itself
- Example: Sicker patients more likely to drop out of study

### Identifying Missing Values
```r
# Load example dataset with missing values
covid_data <- read_csv("covid_study_data.csv")

# Basic missing value assessment
summary(covid_data)                           # Shows NA's for each column
sum(is.na(covid_data))                        # Total missing values
colSums(is.na(covid_data))                    # Missing per column
rowSums(is.na(covid_data))                    # Missing per row

# Percentage missing per column
covid_data %>%
  summarise_all(~sum(is.na(.)) / length(.) * 100)

# Identify patterns of missingness
library(VIM)
aggr(covid_data, col = c('navyblue', 'red'), numbers = TRUE, sortVars = TRUE)
```

### Missing Value Strategies

#### Strategy 1: Complete Case Analysis (Listwise Deletion)
```r
# Remove all rows with any missing values
covid_complete <- na.omit(covid_data)
nrow(covid_complete)  # Check how many observations remain

# Remove rows missing specific variables
covid_analysis <- covid_data %>%
  filter(
    !is.na(age),
    !is.na(gender),
    !is.na(outcome)
  )

# Check what you're losing
missing_summary <- covid_data %>%
  summarise(
    total_observations = n(),
    complete_cases = sum(complete.cases(.)),
    percent_complete = complete_cases / total_observations * 100
  )
```

#### Strategy 2: Available Case Analysis (Pairwise Deletion)
```r
# Use all available data for each analysis
correlation_matrix <- cor(covid_data[, c("age", "days_hospitalized", "symptom_severity")], 
                         use = "pairwise.complete.obs")

# Calculate statistics using available data
covid_data %>%
  summarise(
    mean_age = mean(age, na.rm = TRUE),
    mean_hospitalization = mean(days_hospitalized, na.rm = TRUE),
    correlation_age_hosp = cor(age, days_hospitalized, use = "complete.obs")
  )
```

#### Strategy 3: Simple Imputation
```r
# Mean/mode imputation (use with caution!)
covid_imputed <- covid_data %>%
  mutate(
    age = ifelse(is.na(age), mean(age, na.rm = TRUE), age),
    gender = ifelse(is.na(gender), 
                   names(sort(table(gender), decreasing = TRUE))[1], 
                   gender),
    bmi = ifelse(is.na(bmi), median(bmi, na.rm = TRUE), bmi)
  )

# Forward fill (carry last observation forward)
covid_longitudinal <- covid_data %>%
  arrange(participant_id, visit_date) %>%
  group_by(participant_id) %>%
  fill(symptom_severity, .direction = "down") %>%
  ungroup()

# Backward fill
covid_longitudinal <- covid_longitudinal %>%
  arrange(participant_id, visit_date) %>%
  group_by(participant_id) %>%
  fill(symptom_severity, .direction = "up") %>%
  ungroup()
```

#### Strategy 4: Advanced Imputation Methods
```r
library(mice)  # Multiple Imputation by Chained Equations

# Perform multiple imputation
covid_mice <- mice(covid_data, m = 5, method = 'pmm', seed = 123, printFlag = FALSE)

# Check imputation
plot(covid_mice)
densityplot(covid_mice)

# Create completed datasets
covid_complete_list <- complete(covid_mice, action = "long")

# Pool results from multiple imputations
library(pool)
pooled_model <- with(covid_mice, lm(days_hospitalized ~ age + gender + comorbidities))
pooled_results <- pool(pooled_model)
summary(pooled_results)
```

### Missing Value Best Practices
```r
# Document missing value patterns
missing_report <- covid_data %>%
  summarise_all(~sum(is.na(.))) %>%
  pivot_longer(everything(), names_to = "variable", values_to = "missing_count") %>%
  mutate(
    missing_percent = missing_count / nrow(covid_data) * 100,
    action_taken = case_when(
      missing_percent == 0 ~ "No missing values",
      missing_percent < 5 ~ "Complete case analysis acceptable",
      missing_percent < 20 ~ "Consider imputation",
      TRUE ~ "Investigate missing data mechanism"
    )
  ) %>%
  arrange(desc(missing_percent))

print(missing_report)

# Create missing value indicators (useful for sensitivity analysis)
covid_data <- covid_data %>%
  mutate(
    age_missing = is.na(age),
    bmi_missing = is.na(bmi),
    symptom_missing = is.na(symptom_severity)
  )
```

---

## 2.3 Filtering and Subsetting Data

### Basic Filtering with Base R
```r
# Logical indexing
adults_only <- covid_data[covid_data$age >= 18, ]
females_only <- covid_data[covid_data$gender == "Female", ]
severe_cases <- covid_data[covid_data$symptom_severity == "Severe", ]

# Multiple conditions with & (AND) and | (OR)
high_risk <- covid_data[covid_data$age >= 65 & covid_data$comorbidities == "Yes", ]
priority_cases <- covid_data[covid_data$age >= 65 | covid_data$symptom_severity == "Severe", ]

# Using subset() function (base R)
subset_data <- subset(covid_data, 
                     age >= 18 & !is.na(outcome),
                     select = c(participant_id, age, gender, outcome))
```

### Advanced Filtering with dplyr
```r
# Basic filter
adults <- covid_data %>%
  filter(age >= 18)

# Multiple conditions
high_risk_adults <- covid_data %>%
  filter(
    age >= 18,                              # AND condition (comma-separated)
    comorbidities == "Yes",
    !is.na(outcome)                         # Remove missing outcomes
  )

# OR conditions
priority_patients <- covid_data %>%
  filter(age >= 65 | symptom_severity == "Severe")

# Complex conditions
analysis_cohort <- covid_data %>%
  filter(
    age >= 18,
    gender %in% c("Male", "Female"),        # Include only these values
    !is.na(symptom_onset_date),
    days_since_onset >= 0,
    days_since_onset <= 30
  )

# Filter based on calculated conditions
recent_cases <- covid_data %>%
  filter(
    as.Date(test_date) >= as.Date("2023-01-01"),
    symptom_severity %in% c("Moderate", "Severe")
  )
```

### String-based Filtering
```r
# Text matching
covid_data %>%
  filter(str_detect(symptoms, "fever"))     # Contains "fever"

covid_data %>%
  filter(str_starts_with(participant_id, "COVID"))  # Starts with "COVID"

covid_data %>%
  filter(str_ends_with(hospital, "General"))        # Ends with "General"

# Regular expressions
covid_data %>%
  filter(str_detect(participant_id, "^COVID-\\d{4}$"))  # Matches pattern COVID-#### 
```

### Sampling and Random Selection
```r
# Random sample
set.seed(123)  # For reproducibility
random_sample <- covid_data %>%
  sample_n(100)  # Random 100 observations

random_percent <- covid_data %>%
  sample_frac(0.1)  # Random 10% of data

# Stratified sampling
stratified_sample <- covid_data %>%
  group_by(age_group, gender) %>%
  sample_n(10) %>%        # 10 from each group
  ungroup()

# Top/bottom observations
oldest_patients <- covid_data %>%
  top_n(20, age)          # 20 oldest patients

most_severe <- covid_data %>%
  filter(!is.na(severity_score)) %>%
  top_n(50, severity_score)
```

---

## 2.4 Creating and Modifying Variables

### Basic Variable Creation
```r
# Using base R
covid_data$age_group <- ifelse(covid_data$age < 65, "Under 65", "65 and older")
covid_data$bmi_category <- ifelse(covid_data$bmi < 25, "Normal", "Overweight/Obese")

# Calculate derived variables
covid_data$days_to_recovery <- covid_data$recovery_date - covid_data$symptom_onset_date
covid_data$mortality_risk_score <- covid_data$age * 0.1 + covid_data$comorbidity_count * 2
```

### Advanced Variable Creation with dplyr
```r
covid_data <- covid_data %>%
  mutate(
    # Age categories
    age_group = case_when(
      age < 18 ~ "Child",
      age < 65 ~ "Adult", 
      age >= 65 ~ "Elderly",
      TRUE ~ "Unknown"                      # Catch-all for missing
    ),
    
    # BMI categories (WHO classification)
    bmi_category = case_when(
      is.na(bmi) ~ "Missing",
      bmi < 18.5 ~ "Underweight",
      bmi < 25.0 ~ "Normal weight",
      bmi < 30.0 ~ "Overweight",
      bmi >= 30.0 ~ "Obese",
      TRUE ~ "Other"
    ),
    
    # Risk scoring
    risk_score = case_when(
      age >= 65 & comorbidities == "Yes" ~ "High",
      age >= 65 | comorbidities == "Yes" ~ "Medium",
      TRUE ~ "Low"
    ),
    
    # Time-based calculations
    days_since_onset = as.numeric(Sys.Date() - symptom_onset_date),
    hospitalization_duration = discharge_date - admission_date,
    
    # Logical variables
    is_elderly = age >= 65,
    has_comorbidities = comorbidities == "Yes",
    severe_outcome = outcome %in% c("ICU", "Death"),
    
    # Text processing
    symptoms_count = str_count(symptoms_list, ",") + 1,
    has_fever = str_detect(tolower(symptoms_list), "fever"),
    
    # Mathematical transformations
    log_viral_load = log10(viral_load + 1),      # Add 1 to handle zeros
    age_squared = age^2,
    bmi_centered = bmi - mean(bmi, na.rm = TRUE)
  )
```

### Conditional Variable Creation
```r
# Complex conditional logic
covid_data <- covid_data %>%
  mutate(
    treatment_eligibility = case_when(
      age < 18 ~ "Not eligible - too young",
      is.na(symptom_severity) ~ "Cannot determine - missing severity",
      symptom_severity == "Mild" & comorbidities == "No" ~ "Not eligible - low risk",
      symptom_severity %in% c("Moderate", "Severe") ~ "Eligible",
      age >= 65 & symptom_severity == "Mild" ~ "Eligible - high risk age",
      comorbidities == "Yes" & symptom_severity == "Mild" ~ "Eligible - comorbidities",
      TRUE ~ "Review case manually"
    ),
    
    # Multi-step calculations
    infection_severity = case_when(
      # First check for hospitalization
      !is.na(admission_date) & outcome == "ICU" ~ "Critical",
      !is.na(admission_date) & outcome != "ICU" ~ "Severe",
      # Then check symptoms for non-hospitalized
      symptom_severity == "Severe" ~ "Moderate-Severe",
      symptom_severity == "Moderate" ~ "Moderate",
      TRUE ~ "Mild"
    )
  )
```

### Working with Multiple Datasets for Variable Creation
```r
# Add external reference data
reference_mortality <- data.frame(
  age_group = c("0-17", "18-49", "50-64", "65-74", "75+"),
  baseline_mortality = c(0.001, 0.01, 0.05, 0.15, 0.30)
)

covid_data <- covid_data %>%
  mutate(
    age_category = case_when(
      age <= 17 ~ "0-17",
      age <= 49 ~ "18-49", 
      age <= 64 ~ "50-64",
      age <= 74 ~ "65-74",
      TRUE ~ "75+"
    )
  ) %>%
  left_join(reference_mortality, by = c("age_category" = "age_group")) %>%
  mutate(
    excess_risk = ifelse(outcome == "Death", 1, 0) - baseline_mortality
  )
```

---

## 2.5 Working with Categorical Variables and Factors

### Understanding Factors in R
```r
# Character vs Factor
symptoms_char <- c("Mild", "Severe", "Moderate", "Mild", "Severe")
symptoms_factor <- factor(symptoms_char)

print(symptoms_char)   # Just text
print(symptoms_factor) # Text with levels

# Check properties
class(symptoms_char)   # "character"
class(symptoms_factor) # "factor"
levels(symptoms_factor) # "Mild" "Moderate" "Severe" (alphabetical!)
```

### Creating Factors with Proper Ordering
```r
# Ordered factors (important for epidemiological scales)
severity_ordered <- factor(
  c("Mild", "Severe", "Moderate", "Mild", "Severe"),
  levels = c("Mild", "Moderate", "Severe"),  # Logical order
  ordered = TRUE
)

print(severity_ordered)
# [1] Mild   Severe Moderate Mild   Severe  
# Levels: Mild < Moderate < Severe

# This matters for analysis!
summary(severity_ordered)  # Shows ordered counts
median(severity_ordered)   # Can calculate median for ordered factors
```

### Factor Operations in Data Cleaning
```r
covid_data <- covid_data %>%
  mutate(
    # Convert character to factor with specific levels
    gender = factor(gender, levels = c("Male", "Female", "Other")),
    
    # Ordered factors for severity scales
    symptom_severity = factor(
      symptom_severity,
      levels = c("Asymptomatic", "Mild", "Moderate", "Severe", "Critical"),
      ordered = TRUE
    ),
    
    # Education levels (ordinal)
    education = factor(
      education,
      levels = c("Less than high school", "High school", "Some college", 
                "Bachelor's degree", "Graduate degree"),
      ordered = TRUE
    ),
    
    # Treatment groups (keep original order)
    treatment_group = factor(treatment_group, 
                           levels = c("Control", "Treatment A", "Treatment B"))
  )
```

### Recoding Factor Levels
```r
# Method 1: Using recode()
covid_data <- covid_data %>%
  mutate(
    gender_recoded = recode(gender,
                           "M" = "Male",
                           "F" = "Female", 
                           "O" = "Other"),
    
    # Collapse categories
    age_simple = recode(age_group,
                       "18-29" = "Young Adult",
                       "30-49" = "Young Adult", 
                       "50-64" = "Middle Age",
                       "65-74" = "Older Adult",
                       "75+" = "Older Adult")
  )

# Method 2: Using case_when() for complex recoding
covid_data <- covid_data %>%
  mutate(
    risk_category = case_when(
      age >= 65 & comorbidities == "Yes" ~ "Very High Risk",
      age >= 65 | comorbidities == "Yes" ~ "High Risk",
      age >= 50 ~ "Moderate Risk",
      TRUE ~ "Low Risk"
    ) %>% factor(levels = c("Low Risk", "Moderate Risk", "High Risk", "Very High Risk"),
                 ordered = TRUE)
  )

# Method 3: Using fct_recode() from forcats package
library(forcats)

covid_data <- covid_data %>%
  mutate(
    ethnicity_clean = fct_recode(ethnicity,
                                "Hispanic/Latino" = "Hispanic",
                                "Hispanic/Latino" = "Latino", 
                                "Non-Hispanic White" = "White",
                                "Non-Hispanic Black" = "Black",
                                "Non-Hispanic Asian" = "Asian"),
    
    # Combine rare categories
    ethnicity_collapsed = fct_lump_min(ethnicity_clean, min = 50, other_level = "Other/Mixed")
  )
```

### Factor Analysis and Visualization
```r
# Frequency tables with factors maintain level order
table(covid_data$symptom_severity)  # Ordered from Mild to Severe
prop.table(table(covid_data$symptom_severity)) * 100

# Cross-tabulation preserves ordering
xtabs(~ age_group + symptom_severity, data = covid_data)

# Visualization respects factor levels
ggplot(covid_data, aes(x = symptom_severity)) +
  geom_bar() +
  labs(title = "Distribution of Symptom Severity")  # Bars appear in logical order!

# Grouped analysis with factors
covid_data %>%
  group_by(symptom_severity) %>%
  summarise(
    n = n(),
    mean_age = mean(age, na.rm = TRUE),
    mortality_rate = mean(outcome == "Death", na.rm = TRUE)
  )
```

---

## 2.6 Data Organization and Restructuring

### Renaming Variables
```r
# Base R method
names(covid_data)[names(covid_data) == "old_name"] <- "new_name"

# dplyr method (recommended)
covid_data <- covid_data %>%
  rename(
    participant_id = id,
    date_of_birth = dob,
    symptom_onset = onset_date,
    hospitalization_date = hosp_date
  )

# Rename multiple variables with pattern
covid_data <- covid_data %>%
  rename_with(~ str_replace(.x, "date_", ""), contains("date_"))

# Make all names lowercase and replace spaces
covid_data <- covid_data %>%
  rename_with(~ str_to_lower(str_replace_all(.x, " ", "_")))
```

### Reordering and Sorting
```r
# Arrange rows by variables
covid_sorted <- covid_data %>%
  arrange(symptom_onset_date, participant_id)  # Sort by date, then ID

# Descending order
covid_sorted <- covid_data %>%
  arrange(desc(age), symptom_severity)

# Arrange by multiple criteria with mixed ordering
covid_sorted <- covid_data %>%
  arrange(gender, desc(age), symptom_onset_date)

# Reorder columns
covid_organized <- covid_data %>%
  select(
    # ID variables first
    participant_id, study_site,
    # Demographics
    age, gender, race_ethnicity, education,
    # Clinical variables
    symptom_onset_date, symptom_severity, comorbidities,
    # Outcomes
    hospitalized, icu_admission, outcome, 
    # Everything else
    everything()
  )
```

### Reshaping Data: Wide to Long
```r
# Example: Blood pressure measurements at multiple visits
bp_wide <- data.frame(
  patient_id = c("P001", "P002", "P003"),
  systolic_baseline = c(120, 135, 140),
  systolic_month1 = c(118, 130, 135),
  systolic_month3 = c(115, 125, 130),
  diastolic_baseline = c(80, 85, 90),
  diastolic_month1 = c(78, 82, 88),
  diastolic_month3 = c(75, 80, 85)
)

# Convert to long format
bp_long <- bp_wide %>%
  pivot_longer(
    cols = -patient_id,                        # Don't pivot ID column
    names_to = c("bp_type", "visit"),         # Create two new columns
    names_pattern = "(.+)_(.+)",              # Extract parts of column names
    values_to = "blood_pressure"              # Values go here
  )

print(bp_long)
```

### Reshaping Data: Long to Wide
```r
# Convert back to wide format
bp_wide_again <- bp_long %>%
  pivot_wider(
    names_from = c(bp_type, visit),           # Use both variables for column names
    names_sep = "_",                          # Separator for new column names
    values_from = blood_pressure
  )

# Alternative: Create separate columns for each BP type
bp_analysis <- bp_long %>%
  pivot_wider(
    names_from = bp_type,
    values_from = blood_pressure
  )
```

### Complex Reshaping Examples
```r
# Laboratory results over time
lab_wide <- data.frame(
  patient_id = rep(c("P001", "P002"), each = 3),
  visit = rep(c("Baseline", "Week2", "Week4"), 2),
  wbc = c(7.2, 6.8, 7.1, 8.5, 8.0, 7.8),
  hemoglobin = c(14.1, 13.8, 14.0, 13.5, 13.2, 13.4),
  platelets = c(250, 260, 255, 300, 290, 285)
)

# Convert to analysis-friendly format
lab_analysis <- lab_wide %>%
  pivot_longer(
    cols = c(wbc, hemoglobin, platelets),
    names_to = "lab_test",
    values_to = "result"
  ) %>%
  group_by(patient_id, lab_test) %>%
  mutate(
    baseline_value = first(result),
    change_from_baseline = result - baseline_value,
    percent_change = (result - baseline_value) / baseline_value * 100
  ) %>%
  ungroup()
```

---

## 2.7 Merging and Combining Datasets

### Types of Joins
```r
# Sample datasets
patients <- data.frame(
  patient_id = c("P001", "P002", "P003", "P004"),
  age = c(45, 62, 38, 71),
  gender = c("F", "M", "F", "M")
)

lab_results <- data.frame(
  patient_id = c("P001", "P002", "P005"),  # Note: P005 not in patients
  wbc_count = c(7.2, 8.5, 6.9),
  hemoglobin = c(14.1, 13.5, 12.8)
)

treatments <- data.frame(
  patient_id = c("P001", "P001", "P002", "P003"),  # P001 has 2 treatments
  treatment = c("Drug A", "Drug B", "Drug A", "Drug C"),
  start_date = as.Date(c("2023-01-15", "2023-02-01", "2023-01-20", "2023-01-18"))
)
```

### Inner Join (Only Matching Records)
```r
# Keep only patients who have both demographic and lab data
inner_joined <- inner_join(patients, lab_results, by = "patient_id")
print(inner_joined)
# Result: Only P001 and P002 (both have demographic AND lab data)
```

### Left Join (Keep All from Left Dataset)
```r
# Keep all patients, add lab data where available
left_joined <- left_join(patients, lab_results, by = "patient_id") 
print(left_joined)
# Result: All 4 patients, lab values are NA for P003 and P004
```

### Right Join (Keep All from Right Dataset)
```r
# Keep all lab results, add patient data where available
right_joined <- right_join(patients, lab_results, by = "patient_id")
print(right_joined)
# Result: P001, P002, P005 (P005 has lab data but no demographics)
```

### Full Join (Keep All Records)
```r
# Keep everything from both datasets
full_joined <- full_join(patients, lab_results, by = "patient_id")
print(full_joined)
# Result: All patients (P001-P005), with NAs where data is missing
```

### Complex Merging Scenarios
```r
# Different column names for joining
demographics <- data.frame(
  id = c("P001", "P002", "P003"),
  patient_age = c(45, 62, 38)
)

outcomes <- data.frame(
  patient_id = c("P001", "P002", "P004"),
  outcome_status = c("Recovered", "Recovered", "Hospitalized")
)

# Join with different column names
merged_data <- left_join(demographics, outcomes, by = c("id" = "patient_id"))
```

### Multiple Column Joins
```r
# Join on multiple columns
visit_data <- data.frame(
  patient_id = c("P001", "P001", "P002", "P002"),
  visit_number = c(1, 2, 1, 2),
  visit_date = as.Date(c("2023-01-01", "2023-01-15", "2023-01-02", "2023-01-16"))
)

lab_visits <- data.frame(
  patient_id = c("P001", "P001", "P002", "P002"),
  visit_number = c(1, 2, 1, 2),
  lab_value = c(7.2, 6.8, 8.1, 7.9)
)

# Join on both patient ID and visit number
complete_visits <- inner_join(visit_data, lab_visits, 
                             by = c("patient_id", "visit_number"))
```

### Handling One-to-Many Relationships
```r
# One patient can have multiple treatments
patient_treatments <- left_join(patients, treatments, by = "patient_id")
print(patient_treatments)
# Note: P001 appears twice (has 2 treatments)

# Summarize multiple treatments per patient
treatment_summary <- treatments %>%
  group_by(patient_id) %>%
  summarise(
    num_treatments = n(),
    treatments_list = paste(treatment, collapse = ", "),
    first_treatment_date = min(start_date),
    .groups = "drop"
  )

# Then merge summary
patients_with_treatment_summary <- left_join(patients, treatment_summary, by = "patient_id")
```

### Base R Merging (Alternative)
```r
# Base R equivalent of left_join
base_merge <- merge(patients, lab_results, by = "patient_id", all.x = TRUE)

# Full join equivalent
base_full_merge <- merge(patients, lab_results, by = "patient_id", all = TRUE)

# Different column names
base_diff_names <- merge(demographics, outcomes, 
                        by.x = "id", by.y = "patient_id", 
                        all.x = TRUE)
```

---

## 2.8 Date and Time Handling

### Loading and Converting Dates
```r
library(lubridate)

# Common date formats
date_examples <- data.frame(
  american = c("01/15/2023", "02/28/2023", "12/01/2023"),
  european = c("15/01/2023", "28/02/2023", "01/12/2023"), 
  iso = c("2023-01-15", "2023-02-28", "2023-12-01"),
  text_date = c("January 15, 2023", "Feb 28 2023", "1 Dec 2023")
)

# Convert different formats
date_examples <- date_examples %>%
  mutate(
    american_date = mdy(american),      # month/day/year
    european_date = dmy(european),      # day/month/year
    iso_date = ymd(iso),               # year-month-day
    text_parsed = mdy(text_date)       # Flexible parsing
  )
```

### Date Arithmetic and Calculations
```r
covid_data <- covid_data %>%
  mutate(
    # Convert character dates to Date objects
    symptom_onset = ymd(symptom_onset_date),
    test_date = ymd(test_date),
    hospital_admission = ymd(admission_date),
    
    # Calculate time intervals
    days_onset_to_test = as.numeric(test_date - symptom_onset),
    days_test_to_admission = as.numeric(hospital_admission - test_date),
    days_since_onset = as.numeric(Sys.Date() - symptom_onset),
    
    # Categorize by time periods
    test_timing = case_when(
      days_onset_to_test < 0 ~ "Test before onset",
      days_onset_to_test <= 3 ~ "Early testing (0-3 days)",
      days_onset_to_test <= 7 ~ "Moderate delay (4-7 days)", 
      days_onset_to_test > 7 ~ "Late testing (>7 days)",
      TRUE ~ "Unknown timing"
    )
  )
```

### Extracting Date Components
```r
covid_data <- covid_data %>%
  mutate(
    # Extract date components
    onset_year = year(symptom_onset),
    onset_month = month(symptom_onset),
    onset_day = day(symptom_onset),
    onset_weekday = weekdays(symptom_onset),
    onset_week_number = week(symptom_onset),
    onset_quarter = quarter(symptom_onset),
    
    # Create meaningful groupings
    onset_season = case_when(
      month(symptom_onset) %in% c(12, 1, 2) ~ "Winter",
      month(symptom_onset) %in% c(3, 4, 5) ~ "Spring",
      month(symptom_onset) %in% c(6, 7, 8) ~ "Summer",
      month(symptom_onset) %in% c(9, 10, 11) ~ "Fall"
    ),
    
    # Weekend vs weekday onset
    weekend_onset = weekdays(symptom_onset) %in% c("Saturday", "Sunday")
  )
```

### Time Series and Epidemic Curves
```r
# Prepare data for epidemic curve
epidemic_data <- covid_data %>%
  filter(!is.na(symptom_onset)) %>%
  count(symptom_onset, name = "daily_cases") %>%
  arrange(symptom_onset) %>%
  mutate(
    # Calculate moving averages
    cases_7day_avg = rollmean(daily_cases, k = 7, fill = NA, align = "center"),
    cumulative_cases = cumsum(daily_cases),
    
    # Epidemic week (CDC standard: Sunday start)
    epi_week = epiweek(symptom_onset),
    epi_year = epiyear(symptom_onset)
  )

# Create epidemic curve
ggplot(epidemic_data, aes(x = symptom_onset)) +
  geom_col(aes(y = daily_cases), alpha = 0.7, fill = "steelblue") +
  geom_line(aes(y = cases_7day_avg), color = "red", size = 1) +
  labs(
    title = "COVID-19 Epidemic Curve",
    subtitle = "Daily cases with 7-day moving average",
    x = "Date of Symptom Onset",
    y = "Number of Cases"
  ) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

### Working with Time Zones and Timestamps
```r
# Handle timestamps with time zones
covid_data <- covid_data %>%
  mutate(
    # Convert timestamp strings to datetime
    admission_datetime = ymd_hms(admission_timestamp, tz = "America/New_York"),
    
    # Extract just the date from datetime
    admission_date_only = as.Date(admission_datetime),
    
    # Extract time components
    admission_hour = hour(admission_datetime),
    admission_time_of_day = case_when(
      admission_hour >= 6 & admission_hour < 12 ~ "Morning",
      admission_hour >= 12 & admission_hour < 18 ~ "Afternoon", 
      admission_hour >= 18 & admission_hour < 24 ~ "Evening",
      TRUE ~ "Night"
    )
  )
```

---

## 2.9 Advanced Data Summaries and Cross-tabulations

### Comprehensive Group Summaries
```r
# Multi-level grouping with comprehensive statistics
detailed_summary <- covid_data %>%
  group_by(age_group, gender, vaccination_status) %>%
  summarise(
    # Counts and proportions
    n = n(),
    percent_of_total = n / nrow(covid_data) * 100,
    
    # Age statistics
    mean_age = mean(age, na.rm = TRUE),
    median_age = median(age, na.rm = TRUE),
    age_sd = sd(age, na.rm = TRUE),
    age_iqr = IQR(age, na.rm = TRUE),
    
    # Clinical outcomes
    hospitalization_rate = mean(hospitalized == "Yes", na.rm = TRUE) * 100,
    mortality_rate = mean(outcome == "Death", na.rm = TRUE) * 100,
    icu_rate = mean(icu_admission == "Yes", na.rm = TRUE) * 100,
    
    # Time-based measures
    mean_symptom_duration = mean(symptom_duration_days, na.rm = TRUE),
    median_time_to_test = median(days_onset_to_test, na.rm = TRUE),
    
    # Severity distribution
    mild_cases = sum(symptom_severity == "Mild", na.rm = TRUE),
    moderate_cases = sum(symptom_severity == "Moderate", na.rm = TRUE),
    severe_cases = sum(symptom_severity == "Severe", na.rm = TRUE),
    
    # Missing data patterns
    missing_outcome = sum(is.na(outcome)),
    complete_data_rate = mean(complete.cases(pick(everything()))) * 100,
    
    .groups = "drop"
  ) %>%
  arrange(desc(n))  # Sort by sample size
```

### Advanced Cross-tabulations
```r
# Multi-way cross-tabulation with percentages
cross_tab_detailed <- covid_data %>%
  count(age_group, gender, outcome) %>%
  group_by(age_group, gender) %>%
  mutate(
    total_in_group = sum(n),
    percent_within_group = n / total_in_group * 100
  ) %>%
  ungroup() %>%
  group_by(outcome) %>%
  mutate(
    total_outcome = sum(n),
    percent_of_outcome = n / total_outcome * 100
  ) %>%
  ungroup()

# Create publication-ready cross-tabulation table
cross_tab_wide <- cross_tab_detailed %>%
  select(age_group, gender, outcome, n, percent_within_group) %>%
  unite("count_percent", n, percent_within_group, sep = " (", remove = FALSE) %>%
  mutate(count_percent = paste0(count_percent, "%)")) %>%
  select(-n, -percent_within_group) %>%
  pivot_wider(
    names_from = outcome,
    values_from = count_percent,
    values_fill = "0 (0%)"
  )
```

### Statistical Testing in Summaries
```r
# Include statistical tests in group comparisons
statistical_comparison <- covid_data %>%
  group_by(treatment_group) %>%
  summarise(
    n = n(),
    mean_age = mean(age, na.rm = TRUE),
    sd_age = sd(age, na.rm = TRUE),
    median_recovery_days = median(recovery_days, na.rm = TRUE),
    iqr_recovery = IQR(recovery_days, na.rm = TRUE),
    hospitalization_rate = mean(hospitalized == "Yes", na.rm = TRUE) * 100,
    .groups = "drop"
  )

# Add statistical tests
age_test <- aov(age ~ treatment_group, data = covid_data)
recovery_test <- kruskal.test(recovery_days ~ treatment_group, data = covid_data)
hosp_test <- chisq.test(table(covid_data$treatment_group, covid_data$hospitalized))

# Note: In practice, you'd add these test results to your summary table
```

### Creating Analysis-Ready Datasets
```r
# Prepare final analysis dataset with all transformations
analysis_dataset <- covid_data %>%
  # Filter to analysis population
  filter(
    age >= 18,                          # Adults only
    !is.na(outcome),                    # Must have outcome data
    !is.na(symptom_onset),             # Must have onset date
    symptom_onset >= as.Date("2020-01-01"), # Exclude invalid dates
    symptom_onset <= Sys.Date()
  ) %>%
  
  # Create final analysis variables
  mutate(
    # Primary outcome (binary)
    severe_outcome = outcome %in% c("ICU", "Death", "Hospitalized"),
    
    # Primary exposure (categorical)
    vaccination_status = factor(
      vaccination_status,
      levels = c("Unvaccinated", "Partially Vaccinated", "Fully Vaccinated"),
      labels = c("Unvaccinated", "Partial", "Full")
    ),
    
    # Important covariates
    age_decades = floor(age / 10) * 10,
    bmi_category = factor(
      case_when(
        bmi < 25 ~ "Normal",
        bmi < 30 ~ "Overweight", 
        bmi >= 30 ~ "Obese",
        TRUE ~ "Missing"
      ),
      levels = c("Normal", "Overweight", "Obese", "Missing")
    ),
    
    # Time variables
    days_since_pandemic_start = as.numeric(symptom_onset - as.Date("2020-03-01")),
    pandemic_wave = case_when(
      symptom_onset < as.Date("2020-06-01") ~ "Wave 1",
      symptom_onset < as.Date("2020-12-01") ~ "Wave 2", 
      symptom_onset < as.Date("2021-06-01") ~ "Wave 3",
      TRUE ~ "Wave 4"
    )
  ) %>%
  
  # Select variables for analysis
  select(
    # IDs and administrative
    participant_id, study_site,
    
    # Demographics
    age, age_decades, gender, race_ethnicity, education, bmi_category,
    
    # Exposures
    vaccination_status, previous_infection, comorbidities,
    
    # Outcomes
    severe_outcome, outcome, symptom_severity, hospitalized, icu_admission,
    
    # Time variables
    symptom_onset, days_since_pandemic_start, pandemic_wave,
    
    # Clinical variables
    symptom_duration_days, recovery_days
  ) %>%
  
  # Final quality checks
  filter(
    complete.cases(age, gender, vaccination_status, severe_outcome)  # Complete case for key variables
  )

# Document the final dataset
analysis_summary <- analysis_dataset %>%
  summarise(
    total_participants = n(),
    date_range = paste(min(symptom_onset), "to", max(symptom_onset)),
    age_range = paste(min(age), "to", max(age), "years"),
    percent_severe_outcomes = mean(severe_outcome) * 100,
    percent_vaccinated = mean(vaccination_status != "Unvaccinated") * 100
  )

print("Final Analysis Dataset Summary:")
print(analysis_summary)

# Check balance across key variables
balance_check <- analysis_dataset %>%
  group_by(vaccination_status) %>%
  summarise(
    n = n(),
    mean_age = mean(age),
    percent_female = mean(gender == "Female") * 100,
    percent_comorbidities = mean(comorbidities == "Yes") * 100,
    .groups = "drop"
  )

print("Balance Check Across Exposure Groups:")
print(balance_check)
```

---

## Lesson Summary and Best Practices

### Key Concepts Mastered

**Lesson 1 - Foundation:**
- R and RStudio environment navigation
- Package management and loading
- Basic data types and structures
- Data import from multiple sources
- Initial data exploration and visualization
- Descriptive statistics and frequency tables

**Lesson 2 - Data Mastery:**
- Tidy data principles and implementation
- Comprehensive missing value strategies
- Advanced filtering and subsetting
- Variable creation and transformation
- Factor management for categorical data
- Data reshaping and merging
- Date/time handling for epidemiological data
- Advanced summaries and cross-tabulations

### Essential Best Practices

#### 1. Always Start with Data Exploration
```r
# Standard data exploration workflow
new_data %>%
  glimpse() %>%              # Quick overview
  summary() %>%              # Statistical summary
  sapply(function(x) sum(is.na(x))) %>%  # Missing values
  head(10)                   # First few rows
```

#### 2. Document Your Decisions
```r
# Always comment your reasoning
covid_data <- covid_data %>%
  filter(
    age >= 18,              # Analysis limited to adults per protocol
    !is.na(outcome),        # Primary outcome required for analysis
    symptom_onset >= as.Date("2020-03-01")  # Pandemic start date
  ) %>%
  mutate(
    # Create binary outcome for logistic regression
    severe_outcome = outcome %in% c("ICU", "Death", "Hospitalized")
  )
```

#### 3. Validate Your Transformations
```r
# Always check your work
before_transform <- covid_data %>% count(original_variable)
after_transform <- covid_data %>% count(new_variable)

# Verify transformations make sense
covid_data %>%
  count(age_group, age_continuous) %>%
  arrange(age_continuous)  # Check age grouping is correct
```

#### 4. Save Intermediate Steps
```r
# Save clean datasets at key points
write_csv(covid_raw, "data/covid_raw.csv")
write_csv(covid_clean, "data/covid_cleaned.csv") 
write_csv(analysis_dataset, "data/covid_analysis_ready.csv")
```

#### 5. Create Reproducible Workflows
```r
# Structure your analysis scripts
# 1. Load packages
# 2. Set parameters/constants
# 3. Read data
# 4. Clean data
# 5. Transform variables
# 6. Save analysis-ready data
# 7. Perform analysis

# Use consistent naming conventions
participant_id    # not ID, id, or participantID
symptom_onset    # not onset, symptom_date, or SymptomOnset
severe_outcome   # not severe, severity, or SevereOutcome
```

### Common Pitfalls to Avoid

1. **Not checking data types after import** - Always verify with `str()` or `glimpse()`
2. **Ignoring missing value patterns** - Understand why data is missing before deciding how to handle it
3. **Creating factors without specifying levels** - R's default alphabetical ordering may not be meaningful
4. **Not validating date conversions** - Always check date ranges and formats
5. **Losing data in joins** - Always check row counts before and after merging
6. **Not documenting variable transformations** - Future you (and collaborators) will thank you

This comprehensive foundation in R data management will serve you throughout your epidemiological career. The skills learned here apply to everything from simple descriptive analyses to complex multi-level modeling and everything in between.
