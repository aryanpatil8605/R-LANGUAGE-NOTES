# R-LANGUAGE-NOTES


# Data Science Notes

## 1. Introduction to Data Science

### 1.1 Introduction to Data Science

#### What is Data Science?
Data Science involves extracting insights and knowledge from data through various techniques, such as statistics, machine learning, and data visualization.

#### Defining Data Science Project Roles
- **Project Roles**:
  - **Data Scientist**: Develops models and algorithms.
  - **Data Engineer**: Manages data infrastructure.
  - **Data Analyst**: Analyzes data and creates visualizations.
  - **Business Analyst**: Defines project goals and ensures alignment with business needs.

#### Understanding the Stages of a Data Science Project
1. **Defining the Goal**: Establishing the objectives of the project.
2. **Data Collection and Management**: Gathering and organizing data.
3. **Modeling**: Developing predictive or descriptive models.
4. **Model Evaluation and Critique**: Assessing model performance and reliability.

### 1.2 Data Science Project Lifecycle

#### Presentation and Documentation
- Creating clear and comprehensive reports to communicate findings and insights.
- Documenting the data science process for future reference and reproducibility.

#### Model Deployment and Maintenance
- **Deployment**: Implementing the model in a production environment.
- **Maintenance**: Continuously monitoring and updating the model to ensure its effectiveness.

#### Setting Expectations for a New Data Science Project
- Determining the lower and upper bounds on model performance to set realistic expectations for stakeholders.

## 2. Basics of R and Loading Data into R

### 2.1 Getting Started with R

#### Installing R
Download and install R from the [CRAN website](https://cran.r-project.org/).

#### Using R
Start RStudio and begin writing R scripts or use the R console for interactive commands.

#### Creating and Using Vectors
```r
# Creating a vector
vec <- c(1, 2, 3, 4)
print(vec)
```

#### Creating Data Frames
```r
# Creating a data frame
df <- data.frame(name = c("John", "Doe"), age = c(25, 30))
print(df)
```

#### Exploring Data Frames
```r
# Exploring a data frame
str(df)
summary(df)
```

#### Accessing Columns in a Data Frame
```r
# Accessing a column
df$name
```

#### Reading a CSV Text File
```r
# Reading a CSV file
df <- read.csv("file.csv")
```

#### Removing Rows and Columns
```r
# Removing a row
df <- df[-1, ]

# Removing a column
df <- df[, -1]
```

#### Renaming Rows and Columns
```r
# Renaming columns
names(df) <- c("First_Name", "Age")
```

#### Sorting Data Frames
```r
# Sorting data frame by a column
df <- df[order(df$Age), ]
```

#### Understanding R’s Data Frame Structure
Data frames are 2-dimensional data structures in R, similar to tables in a database.

### 2.2 Working with Data from Files

#### Working with Well-Structured Data from Files or URLs
```r
# Reading data from a URL
df <- read.csv("https://example.com/data.csv")
```

#### Using R on Less-Structured Data
```r
# Reading data with irregular structures
data <- readLines("unstructured_data.txt")
```

#### Working with Relational Databases
```r
# Connecting to a database
library(RSQLite)
conn <- dbConnect(SQLite(), "database.sqlite")

# Loading data from a database
df <- dbGetQuery(conn, "SELECT * FROM table_name")
```

#### Working with the PUMS Data
Public Use Microdata Sample (PUMS) data can be loaded and analyzed in R using similar techniques as above.

## 3. Working with RStudio, Exploring Data, and Managing Data

### 3.1 Onward with RStudio

#### Creating R Scripts
Create R scripts (.R files) to write and save your R code for reuse.

#### Creating Functions using R
```r
# Creating a function
my_function <- function(x, y) {
  return(x + y)
}
print(my_function(3, 4))
```

#### Testing Functions
Ensure your functions work correctly by testing them with various inputs.

### Exploring Data

#### Using Summary Statistics to Spot Problems
```r
# Summary statistics
summary(df)
```

### Managing Data

#### Cleaning Data
```r
# Treating missing values
df[is.na(df)] <- 0
```

#### Data Transformations
```r
# Log transformation
df$log_age <- log(df$Age)
```

#### Sampling for Modeling and Validation
```r
# Creating training and test splits
set.seed(123)
train_index <- sample(seq_len(nrow(df)), size = 0.7 * nrow(df))
train_df <- df[train_index, ]
test_df <- df[-train_index, ]
```

## 4. Modeling Methods

### 4.1 Choosing and Evaluating Models

#### Mapping Business Problems to Machine Learning Tasks
- **Classification**: Predicting categorical labels.
- **Regression**: Predicting continuous values.
- **Clustering**: Grouping similar items.

#### Evaluating Models
```r
# Evaluating a classification model
library(caret)
model <- train(name ~ ., data = train_df, method = "rf")
predictions <- predict(model, newdata = test_df)
confusionMatrix(predictions, test_df$name)
```

### 4.2 Evaluating Different Types of Models

#### Evaluating Probability Models
Assess models that provide probability estimates.

#### Evaluating Ranking Models
Assess models that rank items or users.

#### Evaluating Clustering Models
Assess models that group similar items together.

### Validating Models

#### Identifying Common Model Problems
- Overfitting: When a model performs well on training data but poorly on test data.
- Underfitting: When a model performs poorly on both training and test data.

#### Quantifying Model Soundness
Use metrics like accuracy, precision, recall, and F1 score to evaluate model performance.

#### Ensuring Model Quality
Regularly monitor and update models to maintain their effectiveness.

## Example Workflow

### Load Data
```r
df <- read.csv("data.csv")
```

### Explore Data
```r
summary(df)
```

### Clean Data
```r
df <- df %>%
  filter(!is.na(age))
```

### Analyze Data
```r
model <- lm(age ~ name, data = df)
summary(model)
```

### Visualize Data
```r
library(ggplot2)
ggplot(df, aes(x = age, y = name)) + geom_point()
```

### Report Results
```markdown
---
title: "Analysis Report"
output: html_document
---

```{r}
summary(df)
ggplot(df, aes(x = age, y = name)) + geom_point()
```
```

By following these notes and practicing the code examples, you will gain a strong foundation in data science using R.
```
