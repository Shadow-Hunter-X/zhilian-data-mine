# zhilian-data-mine
智联招聘网站爬取和挖掘
通过前期编写的Python爬虫持续爬起更多的数据；完善对Sqlserver多维数据集的处理，使用数据挖掘功能对多维数据进行挖掘，并使用PowerBI制作报表，产出Excel分析数据；使用Python对Excel数据进行再次分析；尝试使用Python scikit-learn进行数据挖掘。

在DatabaseDemo中有部分爬取的实例数据。

------------------------------------------------------------------------------------------------------------------------
工程结构图
![工程结构](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/1.png)

多维数据集
![多维数据集](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/2.png)

分析说明：
由于是进行多维分析，所以更加个人的意愿进行各个角度的分析，这里列举一些结果说明。

Excel链接多维数据集进行多维分析
使用excel进行多维分析（多维交叉分析可以得到很多复杂的结果，这里列举一个说明）
分析： 
对广州市有对IT运维有需求的企业，从工种，城市，企业3个维度对招聘计算进行分析。
将城市维度定位到 : 广州市
将工种维度定位到 : it运维
企业维度定位到  ： 民营
可以得到以下的数据分析表，通过张开感兴趣的企业标签，可以发现在 企业规模为10000人以上的企业中有：广东美的制冷设备有限公司；品骏控股有限公司等有需求。
![Excel分析](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/b.png)

数据挖掘分析
在构建好的多维数据基础上进行数据挖掘分析，使用微软内置的多种挖掘算法（也是目前最常见，主流的分析方法）进行构挖掘模型
![Excel分析](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/a.png)

PowerBI报表分析
热门城市需求及薪资（使用分段条形图）
结果： 北京各方面领先，前4名城市，北上深杭
![pwoerbi](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/3.png)

工种百分比（饼图）
在特定爬取几类职业中：软件，互联网开发，IT运维需求最大
![powerbi](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/4.png)

各城市企业分布（瀑布图）
分析：北京依旧是大哥，针对各城市民营企业都是主力军，对于北京其国企招聘需求较大，点击详细数据中，港澳台性质的企业在深圳和广州的招聘需求较大。
![powerbi](https://github.com/Shadow-Hunter-X/zhilian-data-mine/blob/master/ReportData/res/5.png)




