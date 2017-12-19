```r
>install.packages('rvest')
>library('rvest')
>html <- read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")

>rank_data_html <- html_nodes(html,'.text-primary')
>rank_data <- html_text(rank_data_html)
>rank_data<-as.numeric(rank_data)
>rank_data
[1] "1."   "2."   "3."   "4."   "5."   "6."   "7."   "8."   "9."   "10."  "11."  "12."  "13."  "14."  "15."  "16."  "17."  "18." 
[19] "19."  "20."  "21."  "22."  "23."  "24."  "25."  "26."  "27."  "28."  "29."  "30."  "31."  "32."  "33."  "34."  "35."  "36." 
[37] "37."  "38."  "39."  "40."  "41."  "42."  "43."  "44."  "45."  "46."  "47."  "48."  "49."  "50."  "51."  "52."  "53."  "54." 
[55] "55."  "56."  "57."  "58."  "59."  "60."  "61."  "62."  "63."  "64."  "65."  "66."  "67."  "68."  "69."  "70."  "71."  "72." 
[73] "73."  "74."  "75."  "76."  "77."  "78."  "79."  "80."  "81."  "82."  "83."  "84."  "85."  "86."  "87."  "88."  "89."  "90." 
[91] "91."  "92."  "93."  "94."  "95."  "96."  "97."  "98."  "99."  "100."

>title_data_html <- html_nodes(html,'.lister-item-header a')
>title_data <- html_text(title_data_html)
>title_data
[1] "Зорянi вiйни: Останнi Джедаi"              "The Disaster Artist"                      
[3] "The Shape of Water"                        "Лiга справедливостi"                      
[5] "Jumanji: Welcome to the Jungle"            "Тор: Рагнарок"                            
[7] "Дюнкерк"                                   "Коко"                                     
[9] "Mother!"                                   "Wonder"                                   
[11] "Вбивство в Схiдному експресi"              "Bright"                                   
[13] "The Greatest Showman"                      "Kingsman: Золоте кiльце"                  
[15] "Вартовi Галактики 2"                       "Lady Bird"                                
[17] "Воно"                                      "The Killing of a Sacred Deer"             
[19] "Гора мiж нами"                             "Three Billboards Outside Ebbing, Missouri"
[21] "Darkest Hour"                              "Фердинанд"                                
[23] "I, Tonya"                                  "Call Me by Your Name"                     
[25] "Beyond Skyline"                            "El Camino Christmas"                      
[27] "The Snowman"                               "Той, хто бiжить по лезу 2049"    
...

>runtime_data_html <- html_nodes(html,'.text-muted .runtime')
>runtime_data <- html_text(runtime_data_html)
>runtime_data<-gsub(" min","",runtime_data)
>runtime_data<-as.numeric(runtime_data)
>runtime_data
[1] 152 104 123 120 119 130 106 105 121 113 114 117 105 141 136  94 135 121 112 115 125 106 119 132 105  89 119 164 118 112 137
[32] 137 104 115 115 119 113 115  93 130 135 141 133 100  91 112 116 143 107  85 132 104 140 109  93  86 118 123 129 140  92 120
[63] 111 101  97 109  95 134 142 104  90 122 118 104 129 110  90  98 103  92 101  90 116 155 121 116  99  96 124 111 133  94 122
[94] 102  97 111 105  85 122 118

>movies <- data.frame(Rank = rank_data, Title = title_data, Runtime = runtime_data, stringsAsFactors = FALSE )
```
1. Виведіть перші 6 назв фільмів дата фрейму.
```r
> head(movies$Title, 6)
[1] "Зорянi вiйни: Останнi Джедаi"  
[2] "The Disaster Artist"           
[3] "The Shape of Water"            
[4] "Лiга справедливостi"           
[5] "Jumanji: Welcome to the Jungle"
[6] "Тор: Рагнарок"    
```
2. Виведіть всі назви фільмів с тривалістю більше 120 хв.
```r
> movies[movies$Runtime > 120, ]$Title
 [1] "Зорянi вiйни: Останнi Джедаi"            
 [2] "The Shape of Water"                      
 [3] "Тор: Рагнарок"                           
 [4] "Mother!"                                 
 [5] "Kingsman: Золоте кiльце"                 
 [6] "Вартовi Галактики 2"                     
 [7] "Воно"                                    
 [8] "The Killing of a Sacred Deer"            
 [9] "Darkest Hour"                            
[10] "Call Me by Your Name"                    
[11] "Той, хто бiжить по лезу 2049"            
[12] "Валерiан i мiсто тисячi планет"          
[13] "Логан: Росомаха"                         
[14] "Phantom Thread"                          
[15] "Downsizing"                              
[16] "Диво-Жiнка"                              
[17] "Людина-павук: Повернення додому"         
[18] "Detroit"                                 
[19] "All the Money in the World"              
[20] "Molly's Game"                            
[21] "Сiм сестер"                              
[22] "Красуня i Чудовисько"                    
[23] "Вiйна за планету мавп"                   
[24] "Mudbound"                                
[25] "The Square"                              
[26] "Roman J. Israel, Esq."                   
[27] "Пiрати Карибського моря: Помста Салазара"
[28] "Трансформери: Останнiй лицар"            
[29] "Пострiл в безодню"                       
[30] "Power Rangers"                           
[31] "Hostiles"                                
[32] "Girls Trip"                              
[33] "Джон Уiк 2"   
```
3. Скільки фільмів мають тривалість менше 100 хв.
```r
> length(movies[movies$Runtime < 100, ]$Title)
[1] 20
```
