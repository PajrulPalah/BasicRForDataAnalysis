# Data Analysis With R

---
Title: "Lesson R Sandbox Activity"
output: html_document
---

## Background for this activity
Welcome to the sandbox! This activity is going to provide you with the opportunity to preview some of the cool things you can do in `R` that you will be learning in this course. You will learn more about working with packages and data and try out some important functions.  

In this activity, you are going to install and load `R` packages; practice using functions to view, clean, and visualize data; and learn more about using `R markdown` to document your analysis. `R` is a powerful tool that can do a lot of different things; this sandbox activity will help you get more comfortable using `R` while demonstrating some of its functions in action. In later activities, you will also get the opportunity to write your own R code!   

## Step 1: Using `R packages`
`Packages` are a key part of working with `R.`They contain bundles of code called `functions` that allow you to perform a wide range of tasks in `R.` Some of them even contain datasets that you can use to practice the skills you have been learning throughout this course.

Some `packages` are installed by default, but many others can be downloaded from an external source such as the Comprehensive R Archive Network, or CRAN.

In this activity, you will be using a package called `tidyverse.` The `tidyverse` package is actually a collection individual `packages` that can help you perform a wide variety of analysis tasks.

To install the `tidyverse` package, execute the code in the code chunk below by clicking on the green arrow button in the top right corner. When you execute a code chunk in RMarkdown, the output will appear in the .rmd area and your console.

```{r}
install.packages("tidyverse")
```

Once a package is installed, you can load it by running the `library()` function with the package name inside the parentheses, like this:

```{r}
library(tidyverse)
```

Installing and loading the `tidyverse` package may take a few minutes-- be sure to wait for it to finish running before moving on to the next steps!

Once the chunk above has finished running, you will get a report that summarizes what packages were loaded because you ran the `library()` function. The report will also let you know you if there are any `functions` that have a conflict, but you don't need to worry about that for now.  

Now that you have loaded an `R package,` you can start exploring some data. 

# Step 2: Viewing data

Many of the `tidyverse` packages contain sample datasets that you can use to practice your `R` skills. The `diamonds` dataset in the `ggplot2` package is a great example for previewing `R` functions. 

Because you already loaded this package in the last step, the `diamonds` dataset is ready for you to use.

One common function you can use to preview the data is the `head()` function, which displays the columns and the first several rows of data. You can test out how the `head()` function works by running the chunk below:

```{r}
head(diamonds)
```
The result will show
![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/ac038f63-72e1-4203-ad4e-5aa17ed31f5c)


In addition to `head()` there are a number of other useful functions you can use to summarize or preview the data. For example, the `str()` and `glimpse()` functions will both return summaries of each column in your data arranged horizontally. You can try out these two functions by running the code chunks below:

```{r}
str(diamonds)
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/7367aac9-a8ff-4be5-b137-6260af93f851)

```{r}
glimpse(diamonds)
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/eb2260f2-7fa2-44a1-af80-9ee40d54bff8)


Another simple function that you may use regularly is the `colnames()` function. It returns a list of column names from your dataset. You can check out this function by running the code chunk below:

```{r}
colnames(diamonds)
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/ec3921b2-2097-4e08-9719-42baafda32f5)

After running the code chunk, you may have noticed a number in brackets. This number helps you count the number of columns in your dataset. If you have data with lots of columns and `colnames()` prints the results on multiple lines, each line will have a number in brackets at the start of the line indicating what number column that is! So, for example, "carat" is the first column in the `diamonds` dataset. On the second line, there is the number seven in brackets; "price" is the seventh column. 

## Step 3: Cleaning data

One of the most frequent tasks you will have to perform as an analyst is to clean and organize your data. `R` makes this easy! There are many functions you can use to help you perform important tasks easily and quickly. 

For example, you might need to rename the columns, or variables, in your data. There is a function for that: `rename().` You can check out how it works in the chunk below:

```{r}
rename(diamonds, carat_new = carat)
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/475dcdee-d523-4da3-a505-0f8ff7faa7e3)

Here, the function is being used to change the name of `carat` to `carat_new`. This is a pretty basic change, but `rename()` has many options that can help you do more complex changes across all of the variables in your data.

For example, you can rename more than one variable in the same `rename()` code. The code below demonstrates how:

```{r}
rename(diamonds, carat_new = carat, cut_new = cut)
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/db51b22f-056d-4ae1-8102-4a49f453e289)


Another handy function for summarizing your data is `summarize().` You can use it to generate a wide range of summary statistics for your data. For example, if you wanted to know what the mean for `carat` was in this dataset, you could run the code in the chunk below:

```{r}
summarize(diamonds, mean_carat = mean(carat))
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/0c920d40-bc8d-4235-b7f9-233dabbf398f)

These functions are a great way to get more familiar with your data and start making observations about it. But sometimes, previewing tables isn't enough to understand a dataset. Luckily, `R` has visualization tools built in. 

## Step 4: Visualizing data
With `R,` you can create data visualizations that are simple and easy to understand or complicated and beautiful just by changing a bit of code. `R` empowers you to present the same data in so many different ways, which can help you create new insights or highlight important data findings.  One of the most commonly used visualization packages is the `ggplot2` package, which is loaded automatically when you install and load `tidyverse.` The `diamonds` dataset that you have been using so far is a `ggplot2` dataset.

To build a visualization with `ggplot2` you layer plot elements together with a `+` symbol. You will learn a lot more about using `ggplot2` later in the course, but here is a preview of how easy and flexible it is to make visuals using code:

```{r}
ggplot(data = diamonds, aes(x = carat, y = price)) +
  geom_point()
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/fd0374e8-8ed8-4bcb-aa7e-fcbdae3bf8e3)

The code above takes the `diamonds` data, plots the carat column on the X-axis, the price column on the Y-axis, and represents the data as a scatter plot using the `geom_point()` command. 

`ggplot2` makes it easy to modify or improve your visuals. For example, if you wanted to change the color of each point so that it represented another variable, such as the cut of the diamond, you can change the code like this:

```{r}
ggplot(data = diamonds, aes(x = carat, y = price, color = cut)) +
  geom_point()
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/fbe3dc80-adcb-4ae1-ac27-69e063bc353d)


Wow, that's a busy visual! Sometimes when you are trying to represent many different aspects of your data in a visual, it can help to separate out some of the components. For example, you could create a different plot for each type of cut. `ggplot2` makes it easy to do this with the `facet_wrap()` function:

```{r}
ggplot(data = diamonds, aes(x = carat, y = price, color = cut)) +
  geom_point() +
  facet_wrap(~cut)
```
The result

![image](https://github.com/PajrulPalah/My-First-Project-Data-Analysis/assets/143974279/70791c39-c51d-4cff-9c36-699783dd89ac)


You will learn many other ways of working with `ggplot2` to make functional and beautiful visuals later on. For now, hopefully you understand that it is both flexible and powerful!

## Thank You
