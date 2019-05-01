Лабораторна робота № 1. Завантаження та зчитування даних
================

``` r
#install and use needed package to work with xls and xml files
packages = c('XML', 'readxl');

for (package in packages) {
  is_installed = any(grepl(package, installed.packages()))
  if (!is_installed) {
    install.packages(package)
  }
}
```

Завдання 1
----------

За допомогою download.file() завантажте любий excel файл з порталу <http://data.gov.ua> та зчитайте його (xls, xlsx – бінарні формати, тому встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму даних.

``` r
library(readxl)

download.file('https://data.gov.ua/dataset/64579ef8-633c-4752-8f21-75231b3bdbc5/resource/2d4b578f-866e-4133-9fe2-213eb2aaa261/download/nuclear_production_02_2019.xlsx', mode='wb', destfile='lab1_task1.xlsx');
data_task1 <- read_excel('lab1_task1.xlsx', sheet=1);
head(data_task1, 6);
```

    ## # A tibble: 6 x 8
    ##    year month     code enterprise       activity    product  amount    cost
    ##   <dbl> <dbl>    <dbl> <chr>            <chr>       <chr>     <dbl>   <dbl>
    ## 1  2018     1 14309787 "ДП \"СхідГЗК\"" видобуток   УР      60095       NA 
    ## 2  2018     1 14309787 "ДП \"СхідГЗК\"" виробництво УОК       139.  429966.
    ## 3  2018     2 14309787 "ДП \"СхідГЗК\"" видобуток   УР      57140       NA 
    ## 4  2018     2 14309787 "ДП \"СхідГЗК\"" виробництво УОК       162.  504702.
    ## 5  2018     3 14309787 "ДП \"СхідГЗК\"" видобуток   УР      61277       NA 
    ## 6  2018     3 14309787 "ДП \"СхідГЗК\"" виробництво УОК        93.2 285268.

Завдання 2
----------

За допомогою download.file() завантажте файл getdata\_data\_ss06hid.csv за посиланням <https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv> та завантажте дані в R. Code book, що пояснює значення змінних знаходиться за посиланням <https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0> Необхідно знайти, скільки property мають value $1000000+

``` r
download.file('https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv', destfile='lab1_task2.csv');
data_task2 <- read.csv("lab1_task2.csv")
sum(data_task2$VAL == 24, na.rm = TRUE)
```

    ## [1] 53

Завдання 3
----------

Зчитайте xml файл за посиланням <http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml>. Скільки ресторанів мають zipcode 21231?

``` r
library(XML)

download.file('http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml', mode='wb', destfile='lab1_task3.xml');
data_task3 <- xmlParse('lab1_task3.xml')
zipcodes <- xpathSApply(data_task3, '//zipcode', xmlValue)
length(zipcodes[zipcodes == '21231'])
```

    ## [1] 127
