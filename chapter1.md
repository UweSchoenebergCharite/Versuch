---
title       : Insert the chapter title here
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## Recap of last session

```yaml
type: NormalExercise
lang: r
xp: 50
skills: 1
key: 20613ec5b8
```
100 men and 100 women agreed to have their brain volume as well as their body weight measured. We put the resulting data into variable `my.data` in your R workspace. `my.data` is of type `data frame` (see Chapter 5 of course "Introduction to R")

`@instructions`
 Use `summary()` on `my.data` to have a look at its structure.
Calculate the mean ($\mu$) of brain volume in the my.data dataframe.
Use `aggregate()` to calculate the mean for each gender.
Do the same for the standard deviation ($\sigma$).

`@hint`
Have a look at the plot. Which color does the point with the lowest rating have?

`@pre_exercise_code`
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer
library(tidyr)
library(dplyr)
n<-100
set.seed(123)
my.data<-data.frame(gender=c(rep("male",n),rep("female",n)), brain=c(rnorm(n,1273,100),rnorm(n,1131,100)))
my.data <-
  my.data %>% 
  mutate(body=brain+25+rnorm(n*2,0,100))
```
`@sample_code`
```{r}
# summary(my.data)


#average brain


#aggregate over gender and calculate the brain volume


#aggregate over gender and calculate the standard deviation

```

`@solution`
```{r}
# summary(my.data)
summary(my.data)

#average brain
mean(my.data$brain)

#aggregate over gender and calculate the brain volume
aggregate(my.data$brain,list(my.data$gender),mean)

#aggregate over gender and calculate the standard deviation
aggregate(my.data$brain,list(my.data$gender),sd)
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

success_msg("Good work!")
```

---
## Barplot

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 7aec81280b
```

We created a new dataframe (`p.bar.data`) that contains the mean and its standard error ($\frac{\sigma}{\sqrt{N}}$) for the brain volume of each gender.

`@instructions`
1. Make a simple bar plot and assign it to variable `p.bar`
2. Add error bars to the bar plot.

`@hint`
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

`@pre_exercise_code`
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer
library(tidyr)
library(dplyr)
n<-100
set.seed(123)
my.data<-data.frame(gender=c(rep("male",n),rep("female",n)), brain=c(rnorm(n,1273,100),rnorm(n,1131,100)))
my.data <-
  my.data %>% 
  mutate(body=brain+25+rnorm(n*2,0,100))
p.bar.data<-
  my.data %>% 
  group_by(gender) %>% 
  summarise(N=n(),
  		 mean_brain=mean(brain),         
         sem_brain=sd(brain)/sqrt(N)) %>% 
  mutate(ymin=mean_brain-sem_brain,ymax=mean_brain+sem_brain)
```

`@sample_code`
```{r}
```

`@solution`
```{r}
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
