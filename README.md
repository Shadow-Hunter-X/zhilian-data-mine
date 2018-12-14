# zhilian-data-mine

一、      爬取前的页面分析

首先查看”智联招聘”网站首页，在首页上可以发现各职业分类的列表，如下图所示。
![分类](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/res1.jpg)

	查看网页源代码，并可以直接看到网页源代码（如下图样例），这样对于爬取操作就变得简单一些。
![源码](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/res2.jpg)
即在有源码的情况下，可以先将首页上所有的职业链接都爬取下来后存放到数据库中，后在有选择性的进行对感兴趣的职业进行爬取。

	进入到特定的职业页面上，查看页面信息（如跳转到“网站构架师”），如下图。
![样式](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/res3.jpg)

查看网页源代码，进行提取对应招聘信息列表的 Xpath或Css Selector表达式，如下图的所示。
![选择](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/res4.jpg)

详细查看列表中的每项中包含的信息，筛选提取有用信息，并在scrapy框架中的items文件中指定对应的存储结构体。

	在爬取完一页后，需要跳转到下一页
由于在每种类型下的工作岗位数不同，所以需要在爬取前，先将需要爬取的页数读取出。
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/res5.jpg)

二、	编写爬虫

以“软件”标签下的职业链接进行说明爬取操作。
	首先对从首页抓取所有链接进行处理，构建起url关系的字典，如下所示，在实际爬取过程中，就遍历字典进行操作，对应的字典可以存放到setting文件中。
	程序设计：item设计，根据前期对页面分析，构建相对应的item，在item文件中定义的数据就是要进行爬取和存储的数据。但数据爬取完毕后，将数据存储到数据库中，分别存放到 sqlserver 和 mongodb中。
	当Item在Spider中被收集之后，它将会被传递到Item Pipeline，一些组件会按照一定的顺序执行对Item的处理。对应的pipeline文件的代码如下，主要是进行SQLServer和mongodb的存储操作。对于Sqlserver插入数据时可能会报错，一般是由于构建SQL语句中的一些符号问题，这类问题难以直接通过输出信息进行排查，所以需要连接到SQLServer进行日志查看或sql语句抓取。
	编写爬虫
为了让http请求更接近真实浏览器的请求情况，可以添加模拟的http消息请求头。

三、	分析数据
通过抓取几类数据，得到120万条数据，分别在SQLServer和mongodb中存储，对于存储在SQLServer中的数据可以结合SQLServer BI进行数据分析，而在mongodb中的数据可以和spark结合进行数据，在mongodb中有接近100万个文档。
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/ana1.jpg)

	使用 SQLServer BI分析
	打开SSDT，创建 Integration Services工程，创建一个SSIS包，构建“数据事件探查任务”。
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/ana2.jpg)
	通过“数据事件探查任务”处理后得到分析结果，挑选一些分析结果进行说明。
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/ana3.jpg)
招聘企业规模分布情况:
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/ana4.jpg)
招聘企业类型分布情况：
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/ana5.jpg)
应聘者教育背景的要求
![分页](https://github.com/Shadow-Hunter-X/Crawl-Recruit-Data/blob/master/res/ana6.jpg)


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




