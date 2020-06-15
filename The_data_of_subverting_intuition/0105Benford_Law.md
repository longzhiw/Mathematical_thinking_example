物理学家弗兰克.本福特在其研究发现，人口统计数字、计算机内的文件大小数字，如161974、14739、1980、1476820...首位数字是“1”的情形非常多，而2，3...9这些数字排在数据首位的比例是在不断降低的，数字越大出现的频率越低。

```python
from matplotlib import pyplot as plt
%matplotlib inline

# load price data from local file
with open('./stock_prices', 'r') as f:
    data = f.readlines()

prices = []
for aD in data:
    prices.append(aD.split(',')[1])
    
result = dict()

for i in prices:
    iStr = str(i)
    result.setdefault(iStr[0], []).append(iStr)

data = []
series = []
for i in range(1, 10):
    series.append(f'#{i}')
    data.append(len(result.get(str(i), [])))

plt.title(f'Ben Fort chart of {len(prices)} number', fontsize=16)
plt.bar(series, data)
plt.show()
```
抓取了A股上证的1359支股票的价格并排列后的确得到了一个很不错的下台阶图：

但是如果从随机数里面排列之后还是无法得到很好的下阶梯图像：如下

![png](0105BenFord_Law1.png)

但是这个定律并不符合所有案例，比如下面的随机数就得不到很好看的下降台阶。书中也提到了这点了，所以这个定律还是适合一些自然生成的数据。也正是这点，这个定律有可能能够识别出数据（比如财务数据）的作假，因为如果数据被人为修改过，那么“可能”不符合本福特定律。

```python
# Ben Fort Chart
import random
from matplotlib import pyplot as plt
%matplotlib inline

max_num = random.randint(1, 10000)
min_num = random.randint(1, max_num)
sec_max_num = random.randint(min_num, max_num)
int_list = random.sample(range(1, max_num), sec_max_num)

result = dict()

for i in int_list:
    iStr = str(i)
    result.setdefault(iStr[0], []).append(iStr)

data = []
series = []
for i in range(1, 10):
    series.append(f'#{i}')
    data.append(len(result.get(str(i), [])))

plt.title(f'Ben Fort chart of {len(int_list)} number', fontsize=16)
plt.bar(series, data)
plt.show()
```


![png](0105BenFord_Law1.png)