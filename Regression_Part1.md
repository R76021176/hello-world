---
title: "Regression_Part1"
author: "Howard_Yu"
date: "2016年1月19日"
output: html_document
---
Data Reference：[computer+hardware資料](https://archive.ics.uci.edu/ml/datasets/Computer+Hardware)

其他參考資料：

1. [美國南加大機器學習資料庫](https://archive.ics.uci.edu/ml/datasets.html)

2. [機器學習（一） 從一個R語言案例學線性迴歸](http://www.jasongj.com/2015/03/27/ml1_linear_regression/)

3. [迴歸分析](https://zh.wikipedia.org/wiki/%E8%BF%B4%E6%AD%B8%E5%88%86%E6%9E%90)

```{r}
cpu_data <- read.csv('cpu_data.csv', header = T)
```

```{r}
str(cpu_data)
```

> **先觀察資料趨勢-基本散佈圖**
```{r, echo=FALSE}
plot(cpu_data$PRP, cpu_data$ERP)
```

PRP為依變數 ERP為自變數

```{r}
slm.model <- lm(PRP ~ ERP, data = cpu_data, x = T )

summary(slm.model)

```

$Y_i = \beta_0 + \beta_1 X_i + \varepsilon_i$

經由計算可以看到MSE = ${41.4}^2$，$R^2 = 0.1963$

關係式：$Y_i = 5.85461 + 1.00440 X_i + \varepsilon_i$

從定義上來說，$R^2$ 告訴你在你的模型裡，有多少的
[variance](https://zh.wikipedia.org/wiki/%E6%96%B9%E5%B7%AE)
是可以被你的自變數解釋的。

$R^2$太低的話建議再加入一些變數來估計你的模型

p-value 0.00000000000000022 < 0.05 完全拒絕虛無假設 $H_0:\beta_1=0$

-----------------------------------------------------------------------------------
# 幾張迴歸分析常用的圖

> **配適值vs殘差 模型的差是否有一定趨勢貼近直線**
```{r, echo=FALSE}
plot(slm.model,1)
```

> **殘差的常態機率圖，通常多變量分析會先針對每個變數都做一張著個看他是不是常態分配**
```{r, echo=FALSE}
plot(slm.model,2)
```

> **配適值 vs 標準化殘差的平方根，用途：找離群值或影響點**
```{r, echo=FALSE}
plot(slm.model,3)
```

> **槓桿值 vs 標準化殘差，用途：找離群值或影響點**
```{r, echo=FALSE}
plot(slm.model,4)
```

綜合上述的四張圖後，可以看到R裡面有幫忙標出離群值
一般來說離群值可以拿掉，再建立模型。



