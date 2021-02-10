# Homework1Empiricalclass
 #exercises3.2.4
> #data
> attach(mpg)
> #plot of data
> ggplot(data = mpg)
> #number of rows and colums
> nrow(mpg)
[1] 234
> ncol(mpg)
[1] 11
> 
> #description of variable
> ?mpg
> 
> #The drv variable is a categorical variable which categorizes cars into front-wheels, rear-wheels, or four-wheel drive
> 
> #scatterplot hwl and cyl
> ggplot(data = mpg, aes(x= cyl, y= hwy)) + geom_point()
> ggplot(data = mpg) + geom_point(mapping = aes(x= cyl, y= hwy, color = manufacturer))
> #scatterplot class and drv
> ggplot(mpg, aes(x = drv, y= class)) + geom_point()
> 
> # the last scatterplot is useless for it does not describe any pattern or demonstarte a type of relationship between the two variables  such as the sctatterplot of hwy and cyl. this is caused by the fact that those variables are categorical variables with limited categories
> ggplot(data= mpg)+ geom_point(mapping = aes(x= displ, y= hwy, colour = "blue"))
> 
> # the code above is running with the colour blue such as a categorical variable with one categorie blue. them mapping consider blue such as. However the code below is running differenltly with blue as colour not variable.
> 
> ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy),colour = "blue")
> 
> #The following list contains the categorical variables in mpg:
> ?mpg
> #manufacturer,model,trans,drv,fl,class
> 
> #The following list contains the continuous variables in mpg:
> 
> #displ,year,cyl,cty,hwy
> 
> ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy,colour = cty))
> ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy, size = cty))
> #ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy, shape = cty))
> 
> #When a continuous value is mapped to shape, it gives an error. Though we could split a continuous variable into discrete categories and use a shape aesthetic, this would conceptually not make sense. A numeric variable has an order, but shapes do not.
> 
> 
> 
> #4-What happens if you map the same variable to multiple aesthetics?
> ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy ,colour = hwy, size =  displ))
> 
> #What does the stroke aesthetic do? What shapes does it work with? (Hint: use ?geom_point)
> ?geom_point
> #Stroke changes the size of the border for shapes (21-25). These are filled shapes in which the color and size of the border can differ from that of the filled interior of the shape.
> 
> 
> #What happens if you map an aesthetic to something other than a variable name, like aes(colour = displ < 5)? Note, you’ll also need to specify x and y.
> ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy ,colour = displ<5))
> 
> # the result of displ < 5 is a logical variable which takes values of TRUE or FALSE.
> 
> #1-What happens if you facet on a continuous variable?
> ggplot(data = mpg) + geom_point(mapping = aes(x= displ , y= hwy)) + facet_grid(.~cty)
> #The continuous variable is converted to a categorical variable, and the plot contains a facet for each distinct value.
> 
> #2-What do the empty cells in plot with facet_grid(drv ~ cyl) mean? How do they relate to this plot?
> ggplot(data = mpg) + 
+   geom_point(mapping = aes(x = drv, y = cyl))
> 
> ggplot(data = mpg) + 
+   geom_point(mapping = aes(x = drv, y = cyl)) + facet_grid(drv~cyl)
> 
> #The empty cells (facets) in this plot are combinations of drv and cyl that have no observations. These are the same locations in the scatter plot of drv and cyl that have no points.
> 
> 
> #3-What plots does the following code make? What does . do?
> ggplot(data = mpg) + 
+   geom_point(mapping = aes(x = displ, y = hwy)) +
+   facet_grid(drv ~ .)
> 
> ggplot(data = mpg) + 
+   geom_point(mapping = aes(x = displ, y = hwy)) +
+   facet_grid(. ~ cyl)
> #The symbol . ignores that dimension when faceting. For example, drv ~ . facet by values of drv on the y-axis. While, . ~ cyl will facet by values of cyl on the x-axis.
> 
> 
> #4-Take the first faceted plot in this section:What are the advantages to using faceting instead of the colour aesthetic? What are the disadvantages? How might the balance change if you had a larger dataset?
> 
> ggplot(data = mpg) + 
+   geom_point(mapping = aes(x = displ, y = hwy)) + 
+   facet_wrap(~ class, nrow = 2)
> 
> #Advantages of encoding class with facets instead of color include the ability to encode more distinct categories. 
> #Disadvantages of encoding the class variable with facets instead of the color aesthetic include the difficulty of comparing the values of observations between categories since the observations for each category are on different plots.
> #The benefit of encoding a variable with facetting over encoding it with color increase in both the number of points and the number of categories.
> 
> 
> 
> #5-Read ?facet_wrap. What does nrow do? What does ncol do? What other options control the layout of the individual panels? Why doesn’t facet_grid() have nrow and ncol variables?
> ?facet_wrap
> #The arguments nrow (ncol) determines the number of rows (columns) to use when laying out the facets. It is necessary since facet_wrap() only facets on one variable.
> 
> #The nrow and ncol arguments are unnecessary for facet_grid() since the number of unique values of the variables specified in the function determines the number of rows and columns.
> 
> 
> 
> #6-When using facet_grid() you should usually put the variable with more unique levels in the columns. Why?
> 
> #There will be more space for columns if the plot is laid out horizontally (landscape).
> 
> #1-What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?
> 
> #line chart: geom_line()
> #boxplot: geom_boxplot()
> #histogram: geom_histogram()
> #area chart: geom_area()
> 
> 
> #2-Run this code in your head and predict what the output will look like. Then, run the code in R and check your predictions.
> ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
+   geom_point() + 
+   geom_smooth(se = FALSE)
> 
> #This code produces a scatter plot with displ on the x-axis, hwy on the y-axis, and the points colored by drv. There will be a smooth line, without standard errors, fit through each drv group.
> 
> 
> 
> #3-What does show.legend = FALSE do? What happens if you remove it? Why do you think I used it earlier in the chapter?
> 
> #The theme option show.legend = FALSE hides the legend box.
> 
> #Consider this example earlier in the chapter.
> ggplot(data = mpg) +
+   geom_smooth(
+     mapping = aes(x = displ, y = hwy, colour = drv),
+     show.legend = FALSE
+   )
> #> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
> 
> ggplot(data = mpg) +
+   geom_smooth(mapping = aes(x = displ, y = hwy, colour = drv))
> #> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
> 
> #In the chapter, the legend is suppressed because with three plots, adding a legend to only the last plot would make the sizes of plots different. Different sized plots would make it more difficult to see how arguments change the appearance of the plots. The purpose of those plots is to show the difference between no groups, using a group aesthetic, and using a color aesthetic, which creates implicit groups. In that example, the legend isn’t necessary since looking up the values associated with each color isn’t necessary to make that point.
> 
> 
> #4-What does the se argument to geom_smooth() do?
> ?geom_smooth
> #It adds standard error bands to the lines.
> ggplot(data = mpg, mapping = aes(x = displ, y = hwy, colour = drv)) +
+   geom_point() +
+   geom_smooth(se = TRUE)
> #> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
> 
> 
> 
> #5-Will these two graphs look different? Why/why not?
> ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
+   geom_point() +
+   geom_smooth()
> 
> ggplot() +
+   geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) +
+   geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
> 
> #No. Because both geom_point() and geom_smooth() will use the same data and mappings. They will inherit those options from the ggplot() object, so the mappings don’t need to specified again.
> 
> 
> ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
+   geom_point() +
+   geom_smooth()
> #> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
> 
> 
> ggplot() +
+   geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) +
+   geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
> #> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
> 
> 
> #3.6.6
> 
> #6-Recreate the R code necessary to generate the following graphs.
> #>The following code will generate those plots.
> 
> ggplot(mpg, aes(x = displ, y = hwy)) +
+   geom_point() +
+   geom_smooth(se = FALSE)
> 
> 
> ggplot(mpg, aes(x = displ, y = hwy)) +
+   geom_smooth(mapping = aes(group = drv), se = FALSE) +
+   geom_point()
> 
> 
> ggplot(mpg, aes(x = displ, y = hwy, colour = drv)) +
+   geom_point() +
+   geom_smooth(se = FALSE)
> 
> 
> ggplot(mpg, aes(x = displ, y = hwy)) +
+   geom_point(aes(colour = drv)) +
+   geom_smooth(se = FALSE)
> 
> 
> ggplot(mpg, aes(x = displ, y = hwy)) +
+   geom_point(aes(colour = drv)) +
+   geom_smooth(aes(linetype = drv), se = FALSE)
> #> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
> 
> 
> ggplot(mpg, aes(x = displ, y = hwy)) +
+   geom_point(size = 4, color = "white") +
+   geom_point(aes(colour = drv))
