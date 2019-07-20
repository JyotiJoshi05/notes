# TidyVerse
Collection of data science tools for transforming and visualizing data

Gapminder dataset - GDP and human population data of different countries.

### Loading Packages
library(gapminder)
library(dplyr)

Tibble : special type of data frame

arrange - sorting
filter - subsetting
mutate - manipulating, adding, change existing/modifying
gapminder %>% filter(year==1957) %>% arrange(desc(pop))

gapminder %>% mutate(pop=pop/100000)
new df with pop column mutated

# Filter, mutate, and arrange the gapminder dataset
gapminder %>%
  filter(year == 2007) %>%
  mutate(lifeExpMonths = 12 * lifeExp) %>%
  arrange(desc(lifeExpMonths))