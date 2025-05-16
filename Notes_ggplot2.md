# 安裝與載入ggplot2 Package

```
install.packages("ggplot2") #安裝ggplot2 package
library(ggplot2) #載入ggplot2 package
```

# 添加標題與標籤

```
labs(title = "", x = "", y = "", caption = "數據來源")
```

# 散布圖

```
ggplot(data = mpg, aes(x = displ, y = hwy)) + geom_point(color = "blue", size = 2) +
  labs(title = "引擎排放量與油耗的散布圖", x = "排放量", y = "油耗")
```

# 箱形圖

```
ggplot(data = mpg, aes(x = factor(cyl), y = hwy)) + geom_boxplot(fill = "orange") +
  labs(title = "汽缸數與油耗的箱型圖", x = "汽缸數", y = "油耗")
```

# 柱狀圖

```
ggplot(data = mpg, aes(x = factor(cyl), fill = factor(drv))) + geom_bar(position = "dodge") +
  labs(title = "不同驅動方式的汽缸數", x = "汽缸數", fill = "驅動方式")
```

# 密度圖

```
ggplot(data = mpg, aes(x = hwy, fill = factor(cyl))) + geom_density(alpha = 0.5) +
  labs(title = "油耗的密度分布", x = "油耗", fill = "汽缸數")
```

# 直方圖

```
ggplot(data = mpg, aes(x = hwy)) + geom_histogram(binwidth = 2, fill = "yellow", color = "gray") +
  labs(title = "油耗的直方圖", x = "油耗")
```

# 折線圖

```
ggplot(data = economics, aes(x = date, y = unemploy)) + geom_line(color = "black") +
  labs(title = "失業人數變化", x = "時間", y = "失業人數")
```

# facet_wrap()、facet_grid()、theme()
## facet
to display smaller groups, or subsets, of the data. A facet is a side or section of an object, like the sides of a gemstone (寶石).
- facet_wrap: 一個變數分類
- facet_grid: 兩個變數交叉分組

```
ggplot(data = penguins) +
  geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g, color=species)) +
  facet_wrap(~species) + 
  theme(axis.text.x = element_text(angle = 45)) # x軸標籤轉45度
```

```
ggplot(data = penguins) +
  geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g, color=species)) +
  facet_grid(sex~species)
```

備註：data = penguins需要載入palmerpenguins package

## theme
美化自訂圖表的標題、邊界、字型等
- theme_minimal()
- theme_classic()

```
ggplot(data = mpg, aes(x = displ, y = hwy)) + geom_point() +
  labs(title = "引擎排放量與油耗的散布圖") + theme_minimal()
```
