
## Preprocessing
 I'll select the variable that I need for my project below and I'll change the name of the vairbale to a human readable variable name.

I'll select the variable that I need for my project below and I'll change the name of the vairbale to a human readable variable name.

```{r}
college_reduced <- college %>%
@@ -66,7 +67,7 @@ college_reduced <- college %>%
         Admission_Rate = ADM_RATE)
```

* Recoding the code that was listed in the original data
Re-coding the code that was listed in the original data

```{r}
college_reduced_1 <- college_reduced %>%
@@ -84,32 +85,38 @@ college_reduced_1 <- college_reduced %>%

## Visualization

*  The reason why i chose a histogram is because it allows me to visualize the distribution of the Average SAT Scores among the colleges in the dataset. 
The reason why i chose a histogram is because it allows me to visualize the distribution of the Average SAT Scores among the colleges in the dataset. 

```{r}

ggplot(college_reduced, aes(x = Average_SAT_Score)) +
ggplot(college_reduced_1, aes(x = Average_SAT_Score)) +
  geom_histogram(binwidth = 50, fill = "blue") +
  labs(title = "Distribution of Average SAT Scores", 
       x = "Average SAT Score",
       y = "Count")

```
The histogram above shows the distribution of the average SAT score across the three types of colleges listed.  

* The box plot below shows the distribution of Admission Rates across different types of colleges (Public, Private Nonprofit, Private For-profit). This boxplot can indicate differences in admission policies or competitiveness between different types of institution

```{r}


The box plot below shows the distribution of Admission Rates across different types of colleges (Public, Private Nonprofit, Private For-profit). This boxplot can indicate differences in admission policies or competitiveness between different types of institution

```{r}
ggplot(college_reduced_1) +
  geom_boxplot(mapping = aes(x = reorder(types_of_colleges, Admission_Rate, FUN = median), y = Admission_Rate)) +
  labs(title = "Admission Rates by College Type", 
       x = "Types of Colleges",
       y = "Admission Rate")
```
The box plot above shows private for-profit colleges tend to have higher and more consistent high admission rates. The few outliers indicate colleges with really low admission rates. Private nonprofit colleges have a median admission rate near 0.65, suggesting greater variability in how selective these institutions are. The outliers below suggest that there are several private nonprofit colleges with particularly low admission rates. There are several outliers for public colleges as well, indicating that a few public colleges have admission rates that are lower than the normal for public institutions


*To analyze how the SAT Score distributions vary across different types of colleges. I will use faceting to provide a clearer comparison. This will allow us to identify any distinct patterns across different categories.


To analyze how the SAT Score distributions vary across different types of colleges. I will use faceting to provide a clearer comparison. This will allow us to identify any distinct patterns across different categories.

```{r}
ggplot(college_reduced_1, aes(x = Average_SAT_Score, fill = types_of_colleges)) +
  geom_histogram(position = "identity", binwidth = 50) +
@@ -120,39 +127,48 @@ ggplot(college_reduced_1, aes(x = Average_SAT_Score, fill = types_of_colleges))
theme(axis.text.x = element_text(angle =38))

```

After looking at the graph, it's clear that the count of the private for-profit colleges is very low when compared to the others.


## Summary Statistics

In the code chunk below i used one of my caregorical varibales which was Type_of_college. Then, I used summarize(count = n()) to calculate the count of rows in each category of the Type_of_college variable.

```{r}
summary_stats <- college_reduced_1 %>%
  group_by(types_of_colleges) %>%
  summarize(Count = n())

view(summary_stats)
summary_stats

```


assignment 9 & 10


I calculated a summary statistics for the continuous variables that I chose which are Average_SAT_Score and Admission_Rate. I also grouped it by the categorical variable, types_of_colleges. The summary includes counts, means, medians, ranges, standard deviations, and interquartile ranges to analyze how these aspects differ across different types of colleges. After plenty of trials and research, i realized that I needed use of na.rm = TRUE in the functions and what it does is it ensures that any missing values do not affect the calculations.

```{r}
summary_admission_rates <- college_reduced_1 %>%
full_summary <- college_reduced_1 %>%
  group_by(types_of_colleges) %>%
  summarize(
    Count = n(),
    Mean = mean(Admission_Rate, na.rm = TRUE),
    Median = median(Admission_Rate, na.rm = TRUE),
    Range = max(Admission_Rate, na.rm = TRUE) - min(Admission_Rate, na.rm = TRUE),
    SD = sd(Admission_Rate, na.rm = TRUE),
    IQR = IQR(Admission_Rate, na.rm = TRUE)
  )
view(summary_admission_rates)
```

  summarize(Count = n(),
    Mean_SAT = mean(Average_SAT_Score, na.rm = TRUE),
    Median_SAT = median(Average_SAT_Score, na.rm = TRUE),
    Range_SAT = max(Average_SAT_Score, na.rm = TRUE) - min(Average_SAT_Score, na.rm = TRUE),
    SD_SAT = sd(Average_SAT_Score, na.rm = TRUE),
    IQR_SAT = IQR(Average_SAT_Score, na.rm = TRUE),
    Mean_Admission = mean(Admission_Rate, na.rm = TRUE),
    Median_Admission = median(Admission_Rate, na.rm = TRUE),
    Range_Admission = max(Admission_Rate, na.rm = TRUE) - min(Admission_Rate, na.rm = TRUE),
    SD_Admission = sd(Admission_Rate, na.rm = TRUE),
    IQR_Admission = IQR(Admission_Rate, na.rm = TRUE))
full_summary

```


private nonprofits have higher SAT scores and the lowest admission rates, which indicates a higher selectivity status. For profits colleges have a low SAT scores but higher admission rates, this show that for-profits colleges have less selectivity rate and it's easy for students to get into. Public institutions fall in between, with moderate SAT scores and admission rates.


## Data Analysis
