- 选择合适的前缀索引长度：
  1. 逐步尝试：
```
1. select count(*) as cnt, city from citys group by city order by cnt limit 10;
2. select count(*) as cnt, LEFT(city, 3) as pref from citys group by pref order by cnt limit 10;
3. 直到两个结果很接近即可
```

  2. 精确计算：
```
1. 计算完整列的选择性：
select count(distinct city) / ocunt(*) from city;
2. 计算不同长度前缀的选择性:
select count(distinct city) / ocunt(*) as sel_all
       count(distinct left(city, 3)) / count(*) as sel3,
       count(distinct left(city, 4)) / count(*) as sel4,
       count(distinct left(city, 5)) / count(*) as sel5
from city;
3. 选择最靠近的
```



- 查索引为什么失效：
  1. 原因：索引失效，一般情况是where条件的选择性不高，导致这个索引基本没什么用
  2. 语句：
```
1. 获取选择性值：
select count(distinct name) / count(*) as name_sel from user;
2. 查看值的具体情况：
select count(*) as count , count(name) as name_count from user where name = 'admin';
```
