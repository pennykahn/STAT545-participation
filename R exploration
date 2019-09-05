#Variables
out1 <- 5 + 2
out2 <- 10 / 2
out1 * 15
out3 * 2

#Vectors
times_min <- c(60, 40, 33, 15, 20, 55, 35)
times_min * 2
times_min + 2
times_hr <- times_min / 60

#Functions, Part I
mean(times_min)
mean(times_hr)
sqrt(times_min)
range(times_min)

#Comparisons
times_min < 30 
times_min == 20 #equals to
times_min !=20 #not equals to
times_min > 20 & times_min < 50 #and
times_min <20 | times_min > 50 #or
which(times_min < 30) #which entries in the vector are...
any(times_min < 30) #are any entries in the vector... (T/F)
all(times_min < 30) #are all entries in the vector... (T/F)
sum(times_min < 30) #how many entries in the vector are...

#Subsetting
times_min[3] #3rd entry in the vector
times_min[-3] #everything but the 3rd entry
times_min[c(2,4)] #2nd and 4th entry in the vector - need to specify it's a vector with c()
times_min[1:5] #1st through 5th entries
times_min[times_min<30] #values of entries which are...
times_min[times_min > 50] <- 50 #cap off an upper limit that will change higher values to the limit
times_min[8] <- NA #assigning a missing value

#Functions, Part II
mean(times_min) #returns NA because we added an entry with a value of NA
mean(times_min, na.rm = TRUE) #add na.rm=TRUE to disregard NA values while performing a function
mean(times_min, 0, TRUE) #you can also just specify all arguments so you don't have to name the arguments. don't do this

#Data frames
mtcars
str(mtcars) #tells about structure of table
names(mtcars) #extracts a vector of the names of the variables
mtcars$mpg #extracts one variable of a table into a vector
