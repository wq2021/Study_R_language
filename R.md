# Introduction of R



This file captures all notes of a free online course on openclassrooms called **Initiez-vous au langage R pour analyser vos données**. In this course, we get basic concepts of R language. 

[Course Link](https://openclassrooms.com/fr/courses/4525256-initiez-vous-au-langage-r-pour-analyser-vos-donnees/6250881-importez-des-fichiers-externes)



### Get started

- Get current work directory 

```R
getwd()
```



- Set current work directory

```R
setwd()
```



- Install packages

```R
install.packages("package_name")
```



- Import a package

```R
library(package_name)
```



- Update packages 

```R
update.packages()
```



- Operators 

```R
<- ,  ->,  =
```



### Different object type in R

- Import data

```R
data(iris)
```



- Delete objects

```R
rm(objet1,objet2,objet3)
```



- Get mode of an object

```R
mode(x)
```



- Get the object type

```R
is.null(x)
is.logical(x)
is.numeric(x)
is.complex(x)
is.character(x)
is.factor(x)
```



- Convert the object type

```R
as.logical(x)
as.numeric(x)
as.complex(x)
as.character(x)
attributes(objet)
```



- Missing values : NA (Not Available). Know the position of missing values in an object :

```R
is.na(x) 
```



#### Vector

Vector is a kind of one-row table that can stock several values named elements, it's a monotyped object : all elements share the same data type. (Le **vecteur** est une sorte de tableau d’une ligne (ou une colonne) pouvant stocker plusieurs valeurs appelées **composantes, coordonnées** ou **éléments**. C’est un objet **monotype :** tous les éléments d’un vecteur sont donc du même type.)

There are several ways of creating a vector, eithr using the **operator**, or using a **suitable function**. You can convert the type of a vector from one to another with a suitable function. 

There are three types of vector :

1. Numeric vector
2. String vector
3. Logical vector (boolean)



- Create a vector

```R
1:6
```

```R
c(1,4,10)
c("bonjour","hello","hej")
```



- Get length of a vector

```
length(vec)
```



- Concatnate two vectors 


```R
c(x,y)
```

```
nom <- paste(rep("ind",10),1:10,sep=".")

paste(c("X","Y"),1:5,sep=".",collapse="+")
```



- Extract a part of vector

```R
substr("freerider",5,9)
```



- Create a vector of all values from a to b, attributes : `length` or `by`

```R
seq(1,6,by=0.5)
```



- Create a vector repeating certain values 

```R
rep(c(1,2),each=3)
x <- rep(c("rouge","jaune","bleu"),times=2)
y <- rep(c("rouge","jaune","bleu"),each=2)
z <- rep(c("rouge","jaune","bleu"),times=c(1,4,2))
```



#### Factor 

Factor is a particular type of vector that can be used for stock qualitative variables, there are three functions to create a factor :

1. `factor` and `as.factor()` for non-ordered factors

```r
yf <- factor(c("M","F","F","M","F"))

# different attributs of factor
attributes(yf)
# $levels
# [1] "F" "M"
# $class
# [1] "factor"

levels(yf)
# [1] "F" "M"

nlevels(yf)
# [1] 2

# rename levels
levels(yf) <- c("Femme","Homme")
yf
# [1] Homme Femme Femme Homme Femme
# Levels: Femme Homme
```

```R
salto <- c(1:5,5:1)
salto.f <- as.factor(salto)
```



2. `ordered` for ordered orders

```R
niveau <- ordered(c("débutant","débutant","champion",
                    "champion","moyen","moyen","moyen",
                    "champion"),
levels=c("débutant","moyen","champion"))

niveau
```



We can convert a factor to a classic vector using `as.numeric`  or `as.character`.

```R
X <- c(rep(10,3),rep(12,2),rep(13,4))
Xqual <- factor(X)
as.numeric(Xqual)

provisoire <- as.character(Xqual)
as.numeric(provisoire)
```



Find data type of a vector with three methods.

```R
is.factor(X)
is.numeric(X)
summary(X)
```



#### Matrix

Matrix is a two-dimension monotype value (numeric or character) table. Therefore, matrix is defined by its rows and columns. Matrix has two attributs :

`length` : total number of elements in the matrix

`mode` : mode of elements in this matrix

`dim`: dimension of matrix(number of row and column)



We can create a matrix from elements using `matrix`or from an exsiting object (espacially vector). 

```R
x <- matrix(c(1:6),nrow=2,ncol=3,byrow=TRUE) # arrange the values by row (by column in default)
y <- matrix(1:2,ncol=1)
z <- matrix(3:1,ncol=3)
```



When the length of the vector is different from the number of elements in the matrix, R fills the entire matrix. 

```R
m <- matrix(1:4,nrow=3,ncol=3)
```



We can check matrix dimension.

```R
ncol(X)
nrow(X)
dim(X)
```



A vector is not considered as a matrix in R, but we can transform a vector to a matrix using `as.matrix`.

```R
x <- seq(1,10,by=2)
as.matrix(x)
```



Concatenate two matrix

```R
cbind(c(1,2),c(3,4))
```



Special function `apply` to apply a function to rows (`MARGIN=1`)  or columns (`MARGIN=2`) of a matrix. 

```R
apply(X,MARGIN=2,sum) # sum of col
apply(X,1,mean) # average of row
```



Operations on matrix

```R
m <- matrix(1:4,ncol=2)
n <- matrix(3:6,ncol=2,byrow=T)
m+n
m*n
sin(m) # sinus element by element
exp(m) # exponential
m^4 # fourth power
```



Other functions : 

| **Fonction**    | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| X%*%Y           | matrix product                                               |
| t(X)            | transpose a matrix                                           |
| diag(5)         | 5th-order identity matrix                                    |
| diag(vec)       | diagonal matrix with the values of the vector `vec` in the diagonal |
| crossprod(X, Y) | cross product (t(X)%*%Y)                                     |
| det(X)          | determinant of the matrix                                    |
| svd(X)          | singular value decomposition                                 |
| eigen(X)        | diagonalization of a matrix                                  |
| solve(X)        | inversion of matrix                                          |
| solve(A, b)     | solving linear systems                                       |
| chol(Y)         | Cholesky decomposition                                       |
| qr(Y)           | QR decomposition                                             |



#### List

A list is an ordered set of objects which do not always have the same mode or length. The different objects are called **components** and can be **associated** with a specific name (a bit like a variable).

Lists have the two **attributes** of vectors (`length` and `mode`) and the additional attribute `names`. Lists are indispensable objects, as all functions that return several objects do so in the form of a list.

```R
maliste <- list(c("A","B","C","A"),matrix(1:4,2,2))

# attributes
length(maliste)
mode(maliste)
is.list(maliste)
```



Rename of components with a specific name

```R
names(maliste) # no name at present, the function returns a NULL
names(maliste) <- c("vec","mat")
names(maliste)
```



Create a list from an empty list 

```R
li <- list()
li[[1]] <- 1:4
li$nouv <- matrix(1:4,nrow=2)
names(li)
```



Useful functions

`lapply` : apply a function on every composant of a list.

`unlist(maliste)` : create a vector containing all elements of a list. Be aware that every element need to have the same mode.

`c(liste1, liste2)` : concatenate two lists. 



#### Dataframe 

Dataframe is a list of vectors which have the same length.



Concatenate vectors of the same size and possibly of different modes.

```R
x <- c("A","B","C","A")
y <- 1:4
m <- data.frame(x,y)
length(mondf)
attributes(mondf)
```



Import a data table from an external file (csv, txt, etc.)

```R
read.table()
```



` as.data.frame` : transformation from an object of 2 dimensions (like matrix) to dataframe

`data.matrix` : transformation from a dataframe to matrix



Dataframe visualization

```r
str(mondf) # a simple summary
```

```R
View(mondf) # a more complete summary
```



### Select elements in R objects

There are two ways of select elements in an object of R : by **position** or by **condition**. Conditions can be construted by comparison operators or logical operators. 



Some operators can mix several boolean values :

- `&` : and
- `|` : or
- `!` : not



#### Select elements in vector

The grammar of **selection by position** is `x[selection_vector]`, the selection vector can be positive or negative integer or logical vector. Positive integer is used to select elements that we want to keep using index. 

```R
x <- c(2,-1,15)
x[2]
x[c(1,3)] 
x[c(3,1,2,2,1)]
```



Negative integer is used to move out vector elements that we don't want to keep in the final result. 

```R
x[-2]
```



**Selection by condition** can extract elements with a logical condition, like the value of a element is over 5 but under 12. 

```R
x[!(x<0)]
```



We can also select values of a vector using another vector of same length. 

```R
T <- c(23, 28, 24, 32)
O3 <- c(80, 102, 87, 124)
O3[T>25]
```



#### Select elements in matrix

Select elements by postive index

```R
m[i,] # return row i as a vector 
m[i,, drop = F] # return row i as a matrix using drop = F
m[,c(2,2,1)] # return a 3-column matrix : 2 times of second column and first column.
```



Like vector, we can move out elements in our final result by using negative index. 

```R
m[-1,] # matrix without first row
m[1:2,-1] # first 2 rows without 1st column
```



Select elements by condition

```R
X <- matrix(1:12,nrow=3,ncol=4)
X[,X[1,]>2]
X[X>2]
X[X<5] <- NA
```



#### Select elements in list

First of all, we need to distinguish between `[]` and `[[]]`.  For example :

`[1]` : select the first element of the list which is a sublist, the length is always 1.

`[[1]]` : select the first composant of the list, the length mesures the first object of the list.

```R
x <- c("a","a","b","c") # character vector
X <- matrix(1:8,ncol=4) # numeric matrix
y <- c(T,T,T,F,F) # logical vector 
z <- matrix(c("A","B","C","D"),ncol=2) #character matrix

maliste <- list(comp1=x,comp2=X,comp3=y,element4=z)

maliste[2] # return a sublist
# $comp2
#      [,1] [,2] [,3] [,4]
# [1,]    1    3    5    7
# [2,]    2    4    6    8

length(maliste[2])
# [1] 1

maliste[[2]] # extract the second element of the list
#      [,1] [,2] [,3] [,4]
# [1,]    1    3    5    7
# [2,]    2    4    6    8

length(maliste[[2]])
# [1] 8 
# because the second composant of the list have 8 elements.
```



In addition, we can select elements by object name using `[""]` or operator `$`.

```R
maliste["comp2"]
# $comp2
#      [,1] [,2] [,3] [,4]
# [1,]    1    3    5    7
# [2,]    2    4    6    8

maliste[["comp2"]]
#      [,1] [,2] [,3] [,4]
# [1,]    1    3    5    7
# [2,]    2    4    6    8

maliste$comp2
#      [,1] [,2] [,3] [,4]
# [1,]    1    3    5    7
# [2,]    2    4    6    8
```



#### Select elements in dataframe

We start with creating a new dataframe.

```R
x <- c("A","B","C",rep("D",3))
y <- 1:6
z <- c(seq(10,45,length=5),-10)
mondf <- data.frame(x,y,z)
mondf
#   x y      z
# 1 A 1  10.00
# 2 B 2  18.75
# 3 C 3  27.50
# 4 D 4  36.25
# 5 D 5  45.00
# 6 D 6 -10.00
```

##### Select by position

```R
mondf[1:4,2:3]
#   y     z
# 1 1 10.00
# 2 2 18.75
# 3 3 27.50
# 4 4 36.25

mondf$z
# [1] 10.00 18.75 27.50 36.25 45.00 -10.00

mondf["z"]
#        z
# 1  10.00
# 2  18.75
# 3  27.50
# 4  36.25
# 5  45.00
# 6 -10.00

mondf$x[2:4]
# [1] B C D
# Levels: A B C D
```

Note here that the character vector was automatically changed to a factor by R when the dataframe was created. If you ever want to avoid this, you need to specify the argument `stringsAsFactors = FALSE` when creating the dataframe.



##### Select by condition

```R
mondf[mondf$y>4,]
#   x y   z
# 5 D 5  45
# 6 D 6 -10

mondf[(mondf$y>4)|(mondf$z>17),]
#   x y      z
# 2 B 2  18.75
# 3 C 3  27.50
# 4 D 4  36.25
# 5 D 5  45.00
# 6 D 6 -10.00

mondf[(mondf$y>4)&(mondf$z>17),]
#   x y   z
# 5 D 5  45
```

```R
mondf[mondf$y>4,1:2] # equals to
mondf[mondf$y>4,c('x','y')]
#   x y
# 5 D 5
# 6 D 6
```



### Data manipulation with R

#### Import external files

Data tables can be stored in a delimited text file. We generally use `read.table()` to import files, several attributes needed to be clarified in this function :

- `sep` : separator of columns, can be `\t`, `;`,`" "`, etc.
- `header` : indicates whether or not the first line contains variable headings. By definition, this argument is set to FALSE (i.e. it will not fetch the column names in the first line by default; it must be set to TRUE to change this).
- `dec`:  indicates the decimal separator,   `.` by default.  If you are using a file from a French Excel spreadsheet, for example, you may need to change this argument to `,`.
- `row.names`:  indicates whether a column contains row id. Where there are no column names, R creates them by assigning a row number to each row.

```R
dt1 <- read.table("dataframe1.txt", sep=";", row.names=1, header=TRUE)
dt1
#           age sexe taille poids
# Raoul      21    M    172    80
# Fred       22    M    185    85
# Dominique  20    F    179    75
# Rachel     22    F    165    69
```



Then we could get a summary of dataframe.

```R
summary(dt1)
```



#### Export your work 

There are two ways to export data or object in R: external file or RDS file.



##### Export work in an external file

We generally use `write.table()` to export files, several attributes needed to be clarified in this function :

- `row.names` (default = True) : keep column names as the first row

- `col.names` (default = True) : keep row id
- `quote`(default = True) : . If `TRUE`, any character or factor columns will be surrounded by double quotes. If a numeric vector, its elements are taken as the indices of columns to quote. In both cases, row and column names are quoted if they are written. If `FALSE`, nothing is quoted.
- `dec` (default = ".") : decimal separator.
- `na`: the string to use for missing values in the data.

Examples: 

```R
write.table(tableau,"monfichier.csv",sep=";",row.names=FALSE)
```

```R
ozoneR <- ozone[1:4,c("maxO3","T9","vent")]
write.table(ozoneR,"montableau.txt",row.names=F,col.names=F,quote=F,sep='\t')
```



##### Export work in RDS file

`RDS` is an R format for storing a single R object. It is also possible to go further, using the `RData` format for storing the entire current environment on R (all the objects, functions, etc. currently in memory in the session) and re-importing it into another session.

```R
x <- c("a","a","b","c")
X <- matrix(1:8,ncol=4)
y <- c(T,T,T,F,F)
z <- matrix(c("A","B","C","D"),ncol=2)
maliste <- list(comp1=x,comp2=X,comp3=y,element4=z)

# save RDS file
saveRDS(maliste,"maliste.rds")

# read RDS file
maliste2 <- readRDS("maliste.rds")
```



#### Concatenate data tables

There are two ways of combining tables :

- **vertically**  by placing the tables one below the other (juxtaposition of rows)

- **horizontally** by placing the tables next to each other (juxtaposition of columns)



##### `rbind` : concatenation by rows,  two tables need to have the same length of columns. 

A example of two matrix:

```R
X <- matrix(c(1,2,3,4),2,2)
rownames(X) <- paste("ligne",1:2,sep="")
colnames(X) <- paste("X",1:2,sep="")
X
#        X1 X2
# ligne1  1  3
# ligne2  2  4

Y <- matrix(11:16,3,2)
colnames(Y) <- paste("Y",1:2,sep="")
Y
#      Y1 Y2
# [1,] 11 14
# [2,] 12 15
# [3,] 13 16

Z <- rbind(X,Y)
Z
#        X1 X2
# ligne1  1  3
# ligne2  2  4
#        11 14
#        12 15
#        13 16
```

When R concatenates the matrix, it retain only the names of the rows or row.names in the first matrix.



A example of two dataframes: 

```R
x <- c("A","B","C","A")
y <- 1:4
mondf <- data.frame(x,y)
mondf
#   x y
# 1 A 1
# 2 B 2
# 3 C 3
# 4 A 4

mondf2 <- data.frame("C",1)
mondf2
#   X.C. X1
# 1    C  1

rbind(mondf,mondf2)
# Error in match.names(clabs, names(xi)) : 
#  les noms ne correspondent pas aux noms précédents
```

We can see that variable names of two dataframes need to be the same.

```R
mondf2 <- data.frame(x="C",y=1)
rbind(mondf,mondf2)
#   x y
# 1 A 1
# 2 B 2
# 3 C 3
# 4 A 4
# 5 C 1
```



##### `cbind` : concatenation by columns, two tables need to have the same length of rows. 

```R
mondf3 <- data.frame(taille=c(182,170,172,194),age=c(22,18,33,25))
cbind(mondf,mondf3)
#   x y taille age
# 1 A 1    182  22
# 2 B 2    170  18
# 3 C 3    172  33
# 4 A 4    194  25

cbind(mondf3,mondf)
#   taille age x y
# 1    182  22 A 1
# 2    170  18 B 2
# 3    172  33 C 3
# 4    194  25 A 4
```



##### `merge`: Merge serveral tables using a key

```R
mondf4 <- data.frame(x=c("A","A","D"),taille=seq(180,190,by=5))
merge(mondf,mondf4)
#   x y taille
# 1 A 1    180
# 2 A 1    185
# 3 A 4    180
# 4 A 4    185
```

There are four main types of joints:

1. **Internal join**: only keeps the key values that are in both the first and second tables. This is the basic join performed by the `merge` function.

2. **Right or left join**: retains all the key values in the first table (left join) or the second table (right join). If these values are found in the other table, it completes with the information, as in an internal join; otherwise, the uninformed values are replaced by `NA`s. To do this, you need to specify the arguments `all.x=T` in the case of a left join, and `all.y=T` in the case of a right join.

3. **Outer join**: keeps all the key values from both tables, even if they don't appear in the other table. All the values not entered in the other table are replaced by `NA` . To do this, use the argument `all=T`.  

   

A example of outer join :

```R
merge(mondf,mondf4,all=TRUE)
#   x  y taille
# 1 A  1    180
# 2 A  1    185
# 3 A  4    180
# 4 A  4    185
# 5 B  2     NA
# 6 C  3     NA
# 7 D NA    190
```



#### Generate random numbers

R can simulate data according to any probability distribution. The normal distribution is one of the most appropriate probability distributions for modelling natural phenomena resulting from several random events. These are all phenomena in which the majority of individuals are around an average, with decreasing proportions below and above this average.



As `rnorm`  can construct a normal distribution, there are different prefix defines different calculations of all distributions, we take `rnorm` as a good example :

- `rnorm` : simulate data,  `r` means random. 
- `dnorm` : density of distribition.
- `pnorm` : probability of distribution.
- `qnorm`: calculate quantiles of distribution.



Examples : 

```R
set.seed(12345)
rnorm(5)
# [1]  0.5855288  0.7094660 -0.1093033 -0.4534972  0.6058875

set.seed(12345)
rnorm(5)
# [1]  0.5855288  0.7094660 -0.1093033 -0.4534972  0.6058875
```

```R
pnorm(0)
# [1] 0.5
pnorm(1.96)
# [1] 0.9750021

gx <- seq(-3,3,length=100)
plot(gx,dnorm(gx),type="l")

qnorm(c(0.025,0.5,1))
# [1] -1.959964  0.000000       Inf
```



- `unif` pour **uniforme**
- `t` pour la loi de **Student**
- `f` pour la loi de **Fisher**
- `exp` pour l’**exponentielle**
- `pois` pour la loi de **Poisson**
- `binom` pour la loi **binomiale**



#### Find missing values

Missing values is represented by `NA` in R, we can find it using `is.na()`.

```R
ozR <- ozoneNA[1:4,1:7]
ozR
#     maxO3   T9  T12  T15 Ne9 Ne12 Ne15
# 601    87 15.6 18.5 18.4   4    4    8
# 602    82 17.0 18.4 17.7   5    5    7
# 603    NA   NA   NA 19.5   2    5    4
# 604    NA 16.2   NA 22.5   1   NA    0

is.na(ozR)
#     maxO3    T9   T12   T15   Ne9  Ne12  Ne15
# 601 FALSE FALSE FALSE FALSE FALSE FALSE FALSE
# 602 FALSE FALSE FALSE FALSE FALSE FALSE FALSE
# 603  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
# 604  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE
```



We can get the postion of missing values using `which`, with attribute  `arr.ind` ( *« array indices »*) .

```R
which(is.na(ozR),arr.ind=TRUE)
#     row col
# 603   3   1
# 604   4   1
# 603   3   2
# 603   3   3
# 604   4   3
# 604   4   6
```

Delete missing values.

```R
indligneNA <- which(is.na(ozR),arr.ind=TRUE)[,1]
indligneNA
# 603 604 603 603 604 604 
#   3   4   3   3   4   4

ozRsansNa <- ozR[-indligneNA,]
```



#### Use specific data analysis functions

- `set.seed()` : set the seed of the random number generator, it does not intrinsically generate random numbers.

- `sample` : draw `n` random numbers ( `n` is a positive integer) from a defined vector, with the option of defining whether the number is drawn with or without repetition (using the`replace` argument).

- `summary ` : return a summary on each variable with different descriptive statistics on a dataframe.
- `table` : the distribution of a variable (when the function is used on a single variable), or a cross-table (when the function is used on two variables).
- `sort`:  sort a variable in ascending or descending order (using `decreasing` argument).
- `unique`: return a list of unique individuals
- `duplicate` : duplicate a list of individuals.
- `subset` : extract a subset.
- `split` : truncate the data with a condition.
- `aggregate` : make calculations based on a condition.
- `demo(graphics)` : see different functions to draw graphic plots.



```R
sample(1:10, 3, replace=F)

set.seed(1234)
df <- data.frame(nb = sample(1:10, 100, replace = TRUE),
                 LT = sample(LETTERS[1:3], 100, replace = TRUE),
                 lt = sample(letters[1:3], 100, replace = TRUE))
df[1:10,]

summary(df)

table(df$lt)
table(df$lt,df$LT)

plot(df[,1])

mean(df[,1])
# [1] 4.95

min(df[,1])
# [1] 1

sort(df[1:20,1], decreasing=T) #descending order
# [1] 10  9  9  7  7  7  7  7  7  6  6  3  3  3  3  3  3  2  2  1
```



Attribute `na.rm = True` can make calculations without missing values. Here is an example : 

```R
mean(infosNotes[infosNotes$sexe == 'F', 'notes'], na.rm=TRUE)
```

