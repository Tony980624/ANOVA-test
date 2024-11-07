# ANOVA-test
ANOVA方法 ，主要用于比较多个组的均值，来判断这些组的均值是否显著不同。具体来说，ANOVA 检验的目的是测试不同组之间的均值差异是否大于组内的随机变异。如果各组均值之间的差异显著高于组内变异性，则可以认为组间存在显著差异。

## 生产三组数据

```{r}
Group_A = c(12,15,18,11)
Group_B = c(9,10,13)
Group_C = c(3,5,9,10,11)
```

## 计算三组分别的均值

```
mean_A = mean(Group_A)
mean_B = mean(Group_B)
mean_C = mean(Group_C)

```

$\bar{X}_A$ = 14

$\bar{X}_B$ = 10.67

$\bar{X}_C$ = 7.6

## 所有数据平均值

```
mean_total = sum(c(Group_A,Group_B,Group_C))/(4+3+5)
```

$\bar{X}_{Total} = \frac{12+15+18+11+9+10+13+3+5+9+10+11}{4+3+5}=10.5$ 

## 组内变异平方和

```
sum_of_square = function(v){
  mean = mean(v)
  sum = 0
  for (i in 1:length(v)) {
    sum = sum + (v[i]-mean)^2
  }
  return(sum)
}

sum_A = sum_of_square(Group_A)
sum_B = sum_of_square(Group_B) 
sum_B = sum_of_square(Group_C)
```

$SSW_{A} = (12-14)^2+(15-14)^2+(18-14)^2+(11-14)^2
= 4+1+16+9
=30
$

$SSW_{B} = (9-10.67)^2+(10-10.67)^2+(13-10.67)^2
= 8.67
$

以此类推

## Total sum of squares within group 组内变异平方和

$TSS = 30+8.67+47.2 = 85.87$

## Between group sum of squares

```
BSS = 4*(mean_A-mean_total)^2+3*(mean_B-mean_total)^2+5*(mean_C-mean_total)^2

```

$BSS = n_A \times (\bar{X_A}-\bar{X_{Total}})^2 + n_B \times (\bar{X_B}-\bar{X_{Total}})^2 +n_C \times (\bar{X_C}-\bar{X_{Total}})^2=91.33$

## 计算F值和p值

```
# 计算自由度
df_between <- 3 - 1  # 组间自由度
df_within <- 12 - 3  # 组内自由度

# 计算均方
MSB <- BSS / df_between
MSW <- TSS / df_within

# 计算 F 值
F_value <- MSB / MSW

# 计算 p 值
p_value <- pf(F_value, df_between, df_within, lower.tail = FALSE)

# 输出结果
cat("组间均方 (MSB):", MSB, "\n")
cat("组内均方 (MSW):", MSW, "\n")
cat("F 值:", F_value, "\n")
cat("p 值:", p_value, "\n")
```
p 值: 0.03857723 , 拒绝假设所有组均值相同

