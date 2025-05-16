```
install.packages("dplyr")
library(dplyr)
```

# dplyr Package
用於數據清理與整理，以下是常見的函數：

- select() selecting columns (variables) <---> SELECT (in SQL)
- filter() Filter (subset) rows <---> WHERE (in SQL)
- mutate() Creating new columns (variables) <---> COLUMN ALIAS (in SQL)
- arrange() Sort the data <---> ORDER BY (in SQL)
- group_by() Group the data <---> GROUP BY (in SQL)
- summarise() Summarise (or aggregate) the data
- join() Joining data frames (tables) <---> JOIN (in SQL)


```
p <- head(mtcars) # 取資料集前6列
p <- head(mtcars, n = 10) # 取資料集前10列
```

# select()
選擇數據框(data frame)中指定的行

```
p %>% select(mpg, cyl) # a 10 x 2 data frame, recall: %>% pipe
```

# filter()
選擇數據框中滿足給定條件的列

```
p %>% filter(mpg > 20)
```

# mutate()
增加或修改數據框的行

```
p %>%
  select(mpg, cyl) %>%
  mutate(mpg = mpg + 1) # a 10 x 2 data frame with 2 variables: mpg (editted) & cyl
```

# arrange()
對指定行進行次序排序

```
# from small to large
p %>% arrange(disp)
arrange(p, disp)

# from large to small
p %>% arrange(desc(disp))

# 首先按照cyl升序排列，然後在每個cyl內按照disp升序排列
arrange(mtcars, cyl, disp)
```

# group_by()
由原本資料集產生一個新的分群過的資料集，通常會與summarise函數一起運用

```
p %>% group_by(cyl) %>% summarise(mean_mpg = mean(mpg))
```

# summarise()
根據指定的行進行統計，可能需要用到其他函數，像是：
- min(), max(), mean(), sum()
- sd(), median, IQR(), n(), n_distinct()：標準差，中位數，四分位距，觀察個數，相異觀察個數
- first(), last(), nth()：第一個觀察值，最後的觀察值，查

```
p %>% summarise(mean_mpg = mean(mpg), mean_disp = mean(disp)) # a 1 x 2 data frame
```

# join()
合併資料集

```
df1 <- data.frame(CustomerId = c(1:5), Product = c(rep("Toaster", 3), rep("Radio", 2))) # a 5 x 3 data frame
df2 <- data.frame(CustomerId = c(2, 4, 6), State = c(rep("Alabama", 2), rep("Ohio", 1))) # a 3 x 3 data frame
```

Remark: rep(x, n) for x: vector, n = repetition times

```
inner_join(df1, df2) # key 取交集
full_join(df1, df2) # key 取聯集
left_join(df1, df2) # 取左邊資料集的key，右邊類似
```

# 比較：Data Frame & tibble
## Data Frame
- 默認string轉換為factor，除非設定stringsAsFactors = FALSE
- 顯示全部內容
- 基礎 R
## tibble
- 不會自動轉換string為factor
- 只顯示前10列，並標明數據類型
- Tidyverse Package
