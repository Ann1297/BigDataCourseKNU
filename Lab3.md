Лабораторна робота № 3. Зчитування даних з WEB.
================

В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі 100 фільмами 2017 року виходу за посиланням «<http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature>». Необхідно створити data.frame «movies» з наступними даними: номер фільму (rank\_data), назва фільму (title\_data), тривалість (runtime\_data). Для виконання лабораторної рекомендується використати бібліотеку «rvest». CSS селектори для зчитування необхідних даних: rank\_data: «.text-primary», title\_data: «.lister-item-header a», runtime\_data: «.text-muted .runtime». Для зчитування url використовується функція read\_html, для зчитування даних по CSS селектору – html\_nodes і для перетворення зчитаних html даних в текст - html\_text. Рекомендується перетворити rank\_data та runtime\_data з тексту в числові значення. При формуванні дата фрейму функцією data.frame рекомендується використати параметр «stringsAsFactors = FALSE».

``` r
library(rvest)

html_page = read_html('http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature')

rank_data_text <- html_text(html_nodes(html_page,'.text-primary'))
rank_data <- as.numeric(rank_data_text)

title_data <- html_text(html_nodes(html_page,'.lister-item-header a'))

runtime_data_text <- html_text(html_nodes(html_page,'.text-muted .runtime'))
runtime_data <- as.numeric(gsub(" min", "", runtime_data_text))

movies <- data.frame(rank = rank_data, title = title_data, runtime = runtime_data, stringsAsFactors = FALSE)
```

Завдання 1
----------

Виведіть перші 6 назв фільмів дата фрейму.

``` r
head(movies$title, 6)
```

    ## [1] "Тор: Рагнарок"                   "Людина-павук: Повернення додому"
    ## [3] "Вартовi Галактики 2"             "Unicorn Store"                  
    ## [5] "1+1: Нова iсторiя"               "Найвеличнiший шоумен"

Завдання 2
----------

Виведіть всі назви фільмів с тривалістю більше 120 хв.

``` r
movies[movies$runtime > 120, ]$title
```

    ##  [1] "Тор: Рагнарок"                           
    ##  [2] "Людина-павук: Повернення додому"         
    ##  [3] "Вартовi Галактики 2"                     
    ##  [4] "1+1: Нова iсторiя"                       
    ##  [5] "Диво-Жiнка"                              
    ##  [6] "Зорянi вiйни: Епiзод 8 - Останнi Джедаi" 
    ##  [7] "Воно"                                    
    ##  [8] "Той, хто бiжить по лезу 2049"            
    ##  [9] "Пiрати Карибського моря: Помста Салазара"
    ## [10] "Форма води"                              
    ## [11] "Call Me by Your Name"                    
    ## [12] "Джон Уiк 2"                              
    ## [13] "Чужий: Заповiт"                          
    ## [14] "Красуня i Чудовисько"                    
    ## [15] "Логан: Росомаха"                         
    ## [16] "Король Артур: Легенда меча"              
    ## [17] "Форсаж 8"                                
    ## [18] "Мати!"                                   
    ## [19] "Трансформери: Останнiй лицар"            
    ## [20] "The Shack"                               
    ## [21] "Kingsman: Золоте кiльце"                 
    ## [22] "Гра Моллi"                               
    ## [23] "Валерiан i мiсто тисячi планет"          
    ## [24] "Пострiл в безодню"                       
    ## [25] "Метелик"                                 
    ## [26] "Примарна нитка"                          
    ## [27] "Вороги"                                  
    ## [28] "Brawl in Cell Block 99"                  
    ## [29] "Вбивство священного оленя"               
    ## [30] "Only the Brave"                          
    ## [31] "Темнi часи"                              
    ## [32] "Saban's Могутнi рейнджери"               
    ## [33] "Сiм сестер"                              
    ## [34] "Усi грошi свiту"                         
    ## [35] "The Glass Castle"                        
    ## [36] "Вiйна за планету мавп"                   
    ## [37] "Дружина доглядача зоопарку"

Завдання 3
----------

Скільки фільмів мають тривалість менше 100 хв.

``` r
nrow(movies[movies$runtime < 100, ])
```

    ## [1] 15
