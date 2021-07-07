# Notes taken while learning R from multiple sources (plus some Statistics concepts)
## (throughout this document, the marking -- is used to designate a function, even though -- should not be used when actually running an R code)

# Code Academy

## 10-October-2019

## R basics

Order of operations: PEMDAS (Parenthesis, Exponents, Multiplication, Division, Addition, Subtraction)

Comments #

R data types: number, integer, character, complex, logical

> Numeric data type (e.g., 4)

> Logical data type, capitalized, no quotes (TRUE or FALSE), also booleans - think of it as on/off switches or answers to yes/no questions.

> Character or string - always in quotations, so a number in quotations is read as a character.

> NA - numeric NA, character NA, logical NA

Packages - install.packages('package_name') only need to do once for each package

Libraries - library('package_name') to imports a package

CRAN is a network that stores identical, up-to-date versions of code and documentation for R, use the CRAN mirror nearest to you.

## Conditionals

Conditional ("if statement", "if true statement"), if true do this (=execute code); if false do nothing, 

> Example: (n == 5) {print ('n is equal to five')}

Conditional ("if else statement"), if true do this, if false do that; binary decisions

## Operators

**Comparison operators**

\== is used instead of = to mean 'equal to'

\= means 'assign meaning to a variable' (also <-) 

\>= means 'greater than or equal to'

\<= means 'smaller than or equal to'

\!= not equal to

**Logical operators**

\& means and

\| means or

\! Means not

\! Means bang


## Vectors

Vector - a list of related data that are all the same type; separate vector components with a comma , and wrap the components inside a c() 

To check the type of elements inside a vector: typeof(vector_name)

To check the length of a vector: length(vector_name)

To access individual elements inside a vector: use \[ ] for example, to access the second element, call their position inside c. Example: in a vector called spring_months <- c("March", "April", "May", "June"), type spring_month\[2] to get "April".


## Print

To print a value, always put that value inside ()

Print ()

Print (1000)

Print ('1000')


## Variables

Assign variables using an assignment operator (= or <-)

Variables cannot have spaces or other special characters/symbols in their names other than the underscore _

Variables cannot begin with numbers, but can have numbers after the first letter.


## Functions = actions

--sort

--length

--sum

--uniq

--sqrt

--floor - returns the largest integer not greater thant he given number (-25.26 returns 26; 256.94 returns 256; -136.42 returns -137; 183.999 returns 183; -155.89 returns -156)

--ceiling - returns the smallest integer larger than the parameter (2.5 returns 3; 2.7 returns 3; 2.2 returns 3)




## 31-October to 4-November 2019

## Data cleaning

--head() display first 6 rows by default

--summary() display summary statistics

--colnames() display column names

--listfiles followed by a regular expression 

> Example to create variables and use them in sub-sequential functions

> step 1 files <- list.files("pattern = file_.*csv")

> *This will find any file named as defined by 'pattern' that are located inside your current directory and store the name of each file inside 'files'.*

> step 2 df_list <- lapply(files, read_csv)

> *Uses the lapply package to read each file listed in 'files' using another function 'read_csv()' and then stores the data frames inside df_list*

> step 3 df <- bind_rows(df_list)

> *Use the function bind_row to concatenate all data frames from those files and to save them as 'df'.*


## R commands and functions

--nrow return the number of rows in a data frame

--print(filename) to see the content of filename

> Example: print (nrow_studentsinmyclass) returns 1000

--gather()

--count() takes a data frame and a column as arguments ant returns a table with ocounts of unique values in that column

--duplicated() returns a logical factor (TRUE, FALSE) telling us which rows are duplicated

--distinct() removes all rows of a data frame that are exact duplicate of another row

*Note: to remove rows with duplicate values in a given column (example: column1) we can specify a subset* 

> Example: Dataset %>% distinct(column1,.keep_all = TRUE)

> *This will keep the first occurrence of a duplicate*

--select() will delete a column

> Example: dataset %>% select(-column 33)

> *will delete column 33 from the data frame named 'dataset'*

--table() will return a table with the counts fo each unique value in any R object

_______________________________
NOTE the use of %>% is equivalent to pipe, so 
Duplicates <- duplicated(students) 

is the same as

Duplicates <- students %>% duplicated()
_______________________________

--str_sub() will split strings into separate columns, example MMDDYYYY for birthday info can be split into a column for MM another for DD another for YYYY

--separate() does the same as str_sub but when strings are not same length and separated by an underscore, 

> Example: one column 'user_type' becomes two columns named 'user' and 'type'

> df %>% separate(type,c('user_type','country'),'\_')

> *Where type is the column we want to split up; c('user_type','country') is a vector with the names of the new columns that we want to crate;'_' is the character to split on.*

--str(df) shows the types of each column of a df, the internal structure o an R object (character, numeric, integer, logical or complex)

--gsub and mutate is equivalent fo find and replace

> Example: to replace a $ with a space, do:

> df %>% mutate(price=gsub('\\$',' ',price))

> *Where price is the column where the changes are to be made; '\\$',' ' means replace $ with a space (the empty space inside quotations).*

--as.numeric and --mutate converts character strings containing numerical values to numeric

> Example: df %>% mutate (price=as.numeric(price))

## GGplot2

Some components of GGplot2 are:

Data

Geometrics: dots, bars, lines, etc (geoms)

Aesthetics: scale on axis, color, fill, etc

Viz <- ggplot(data=df)

Viz

--aes() mapping function adds x and y

--geom_point adds points to the plot

--geom_smooth adds line of best fit

To bring it together:

Viz <- ggplot(data=air_quality, aes(x=Ozone, y=Temp)) + geom_point(aes(color = month)) + geom_smooth

break it down to:

> ggplot(data=air_quality, aes(x=Ozone, y=Temp)) 

> *this part tells you what data to plot and the mapping (x,y) of the data*

> NOTE: *The mapped data can be seen as 'canvas'*

> *plus signs mean add-ons to the mapped data*

> (aes(color = month)) 

> *this part needs to be inside 'geom_point' because it is specific to the geom_point "layer", that means it only changes the color of the datapoint (not the rest of the plot).*

To mannually change a specific aesthetic characteristic, provide a named aesthetic parameter and a value for it without wrapping it inside aes(), 

> Example: geom_point(color="darkred") instead of geom_point(aes(color="darkred"))

Other aesthetics for geom_point are:

x

Y

Alpha (opacity of the points)

Shape (other than dots)

Color

Fill

Group

Size

Stroke

The line below shows what looks like when one characteristic is wrapped inside aes and another isn't:

geom_point(aes(color=month),alpha = 0.5)

> aes(color=month) 

> is data-drive

> alpha = 0.5 

> is assigned manually

--labs() assign x an y labels to axis as well as title, subtitle and captions, 

> Example: ...labs(title="This is my plot", subtitle="So pretty", x="sunny days", y="spent money($)"

--geom_bar() = bar graph, x = category, y = counts for each category

--ggsave(fine_to_save.pgn") will save as local file.


## Aggregate statistics

Group data into subset data

General syntax:

**df %>% summarize (var_name = funtion(column_name))**

> Example: Inventory %>% summarize (mean_price = mean(price))

> *Where*

> df in this example is inventory = the original dataset

> var_name in this example is mean_price = the namem of the column where results will be stored

> function in this example is the function mean = what to do with the data 

> column_name in this example is the column Price = the column that currently has the data to be summarized

## Common summary functions

--mean()

--median()

--sd()

--var()

--min()

--max()

--IQR()

--n_distinct()

--n()

--n_distinct = count single

_____________________
Notes

--head(df) shows 6 first columns by default, to show a different number of columns, do head(df, n) where n is the number of columns you want to see.

--n() does not require an argument, but it always needs to be followed by ()

When running the function summarize, add na.rm = TRUE, to ignore any missing (NA) data, as an additional argument in the function

> Example: Inventory %>% summarize (mean_price = mean(price, na.rm=TRUE)) 
_____________________


--group_by = get summarized data for a subset group within the dataset, 

> Example: df %>% group_by(column_1) %>% summarize(mean_grade = mean(grade))

> *Where column_1 is the column that we want to group by.*

--group_by can take more than one argument (group, or column) at the same time,

> Example: df %>% group_by(location.day of week) %>% %>% summarize...

--group_by can be used in combination with filter()

> Example1: df %>% group_by(courses) %>% filter(mean(quiz_score)<80)

> *Where filter(mean means that rows will be filtered by their group value (not individually) because the summarize functions in action*

> and

> Example2: df %>% group_by(courses) %>% filter(n()>16)

> *Where filter (n() will filter by count and return the number of rows within a group.*

--group_by can be used with mutate() to add columns to a data frame that involve a value relative to "per group" metrics. A "per group" metric, such as difference between each grade and the average of all grades, 

> Example: Enrollments %>% group_by(course) %>% mutate (diff_from_course_mean = quiz_score - mean(quiz_scores, na.rm=TRUE))

## Work with data stored in multiple tables.

--inner_join() method looks for columns that are common between 2 df then looks for common rows, then combines the matching rows into a single row in a new table, thus inner_join() requires 2 df,

> Example: joined_df <- orders %>% inner_join(costumes)

> *Where first df is orders, second df is costumes. To join another df, add another line to the above*

> Example: joined_df <- orders %>% inner_join(costumes) %>% inner_join(another_df)

__________________________
NOTE
--inner_join only works when all tables have columns with the same column name. When they don't, there are a couple things you can do:

Rename a column using rename(column_name = new_name)

Or

Use --by when calling --inner_join, 

> Example: df1 %>% inner_join(df2, by = c(column_from_df1 = ('column_from_df2))

> When putting this together, remember right-left-right-left (df1, df2, df1, df2).


R won't let you have 2 columns with the same name thus will automatically change they names to column_x and column_y; because x and y are not necessarily informative, you can change column names using suffix.

--suffix = c('_temperature', '_salinity')

If there's a mismatch between tables (meaning a row that exists in one table but not in the other) inner_join will ignore the mismatched row, meaning the unmatched rows are absent from the joined table. To keep these rows use:

--full_join keeps all rows, even the ones that don't have a match, and fills missing data with NA.

--left_join includes all rows from df1(=left) but only matching rows from the df2(=right) (read as "which rows in df2 are also present in df1, plus all others in df1); in other words, the order of the arguments matters here.


--right_join includes all rows from df2(=right) but only matching rows from df1(=left) (read as "which rows in df1 are also present in df2 plus all others in df2); again, the order of the arguments matters.

--bind_rows method (only works if all columns are named the same in all dis) makes on df from multiple smaller dfs, 

> Example: file_name_dfs <- df1 %>% bind_rows(df2)

## 14-November-2019

## Calculate mean, median

--mean()

--mean(dataset)

--mode(dataset) in package Desctools

--var variance; distances (note: square the values of distances to get rid of negative values).

___________
NOTE

Variance units are different from units of means the datas itself, example:  

Height, inches

Mean height, inches

Variance height, squared inches
________________

--sd standard deviation; square root of the variance to get rid of the 'squaring'

## Quartiles, split the data into four groups of equal size

The second quartile (Q2) is the median

The first quartile (Q1) is the median of all datapoints smaller than Q2

The third quartile (Q3) is the median of all datatpoints greater than Q2

Q1 and Q3 may or may not include the value of the median itself.

--quantile() requires a df and a fraction between 0 and 1

> Quartiles, deciles and percentiles are types of quantiles.

> Example: ten_percent <- quantile(dataset, c(0.2,0.4,0.6,0.8))

--nquantiles equals n+1 groups

--IQR() is the interquartile range ignore the tails (outliers) of the dataset so you know the range amount which your data is centered; IQR = Q3-Q1

## Sample mean vs population mean

Sample mean depends on how many individuals are measured its a subset of the population.

Population mean is constant, may be unknown.

Sampling error when a sample is not representative of the population it comes from; minimize by having a larger sample set.

## 19-November-2019

## Errors

Error type 1 the test finds a correlation between things that are not related; a false positive.

Error type 2 the test fails to find a correlation between things that do relate; a false negative.

--intersect() takes 2 vectors and return a vector containing the common elements.

Stats package 

t.test() takes 2 arguments, 

One Sample T-test - the 2 arguments are: the first is a distribution of values and the second is an expected mean;

Or

Two Sample T-test - the 2 arguments are distribution of values.


The p-value is the probability of incorrectly rejecting the null hypothesis.

The more t-tests the higher the likelihood of getting a false positive; 

Error probability of running 2 t-tests for a p-value of 0.05 is 1-0.05 = 0.95; 0.95\*2 = 0.9025; 1-0.9025 = ~10%

Error probability of running 3 t-tests for a p-value of 0.05 is 1-0.05 = 0.95; 0.95\*3 = 0.857375; 1-0.857375 = ~14%


ANOVA compare more than 2 numerical datasets without increasing the error probability, ie, maintaining it at 0.05.

## ANOVA

Null hypothesis - all datasets have the same mean

If null hypothesis is rejected, ie at least one mean is different, it will not tell which one it is.

Stats package

--aov() takes the multiple datasets combined into a df as an argument, 

> Example:

> Datasets combined = df_scores

> Results <- aov(score ~ group, data = df_scores)

> *Where score ~group indicates the relationship you want to analyze = how each group (column named 'group' in your combined df) relates to score on video game (column 'score' in your combined df).

Then to find ANOVA's p-value, use summary(); in the example above, summary(results).

ANOVA is good for 

Normal distributed datasets;

Datasets with similar sd (by similar, it is meant: sd_df1 divided by sd_df2 should be close to 1, where close means wishing 10%);

Sample sets must be independent.

--hist() displays distribution.

___________________
___________________
18-November-2019

# R studio

Top left corner - **Code Editor** - where you write your code

Bottom left corner - **Console** - where code is executed and results are displayed

Top right corner - **Environment Workspace** - where you see all environment variables and work history

Bottom right corner - **Plots, packages, files and help** - here you can change your working directory, view and activate packages, read help docs.

# Bioinformatics data skills - chapter 10

$ means you need to use the terminal to run the command in R
\>>> means you're in phyton

----------- codes in R can be run in R studio, to do that:

1. set directory in R studio - navigate to your working folder (Bottom Right Corner) then under "more" select "Set as Working Directory" 

2. to start and save your work in R studio - New > Markdown File - that's where you write and or updated your code.

3. When creating a new markdown file, enter the title (this is the title of the document, not hte file name) > Save > then give it a location and name the file.  You may delete everything that 'comes with' the new file, except the title.

4. in a new markdown file type \```{R} \```

5. Your block or chunk of code needs to be written between \```{R}    and    \``` chunks are grey-shaded.

6. anything outside of these boundaries is not code, it is comment (comments can be created inside code chunk by starting the line with a #).


TIP: in R-studio, tell it to show plot in the Console everytime you restart r-studio; the default is to plot in the notebook: to change that, go to Settings (top of markdown) and select "Chunk Output in Console".






