# Python高级编程技巧

## 字典 列表 集合

### 在列表，字典，集合中根据条件筛选数据

* 使用列表解析式和filter函数来筛选数据

```python
#filter 函数参数有两个，一个为函数（常用lambda函数），另一个为可迭代对象，lambda函数根据条件返回Ture或False
import random
import timeit


# 筛选出列表中的非负数
# 生成15个范围在-20，20之间的整数

data = [random.randint(-20, 20) for _ in range(15)]

# 使用filter函数过滤，并转换为list
res_list_filter = list(filter(lambda x: x >= 0, data))

# 使用列表推导式过滤
res_list_list = [x for x in data if x >= 0]

t1 = timeit.timeit("list(filter(lambda x: x >= 0, data))",setup='data = {0}'.format(data),number=10000)
t2 = timeit.timeit("[x for x in data if x >= 0]",setup='data = {0}'.format(data),number=10000)
print(t1,t2)
# t1 = 0.024613799999999998 t2 = 0.008705000000000004,可以看出列表推导式的效率更高，因此推荐列表推导式

# 字典，选出成绩大于等于85的学生
# 生成20个学生的成绩，编号从1到20，作为键；成绩为值，范围60-100
mydict = {k: random.randint(60, 100) for k in range(1, 21)}

res_dict_filter = dict(filter(lambda k: k[1] >= 85, mydict.items()))
res_dict_list = {k: v for k, v in mydict.items() if v >= 85}

# 集合
myset = set(data)
myset_list = {x for x in myset if x >= 0}
myset_filter = set(filter(lambda x: x > 0, myset))
```