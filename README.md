# ZhihuSpider
知乎爬虫，可用于爬取知乎上大部分由用户创建的内容，并且将爬取的内容解析为markdown保存到本地硬盘。目前支持爬取的内容包括：
- 特定问题下的所有回答，如果使用过滤器可以爬取点赞数比较多的优质回答，剔除部分点赞数较少的回答。
- 特定用户的所有回答、文章
- 专栏里的所有文章
- 话题精华
- 收藏夹
- 单个回答
- 单篇文章

## 爬虫工作方式
知乎的问题、回答、文章、专栏、收藏夹、话题等都有唯一对应的id，利用id和知乎api获得相应的内容。内容以json文件的形式返回，包含作者公开的部分个人信息（头像链接、姓名等）、问题信息（题目、链接等）、回答或文章信息（发表、更新时间，点赞数等）。其中回答及文章的的主体内容以html标签的形式包含在json文件中。提取主体内容，使用BeautifulSoup库将这部分内容解析成标签，再由parse模块转换成markdown文件保存到本地。

## 内容组织样式

文章的排版样式几乎与知乎一致，由标题（问题题目）、作者头像、作者姓名、发表时间、点赞数构成题头，点击文章标题可以阅读原文，点击作者姓名可以打开作者的知乎主页。受markdown的限制，目前还不支持视频，处理方式是展示视频的封面、标题（缺省标题将命名为“无题”）以及视频url，点击该url可以用浏览器打开观看该视频。

## 使用方式

GrandConcourse.py是爬虫的入口，将id填入对应的位置即可：

```python
answer_id = ''
column_id = ''
article_id = ''
question_id = ''
topic_id = ''
user_id_for_answers = ''
user_id_for_articles = ''
collection_id = ''
```

同一类型的id只能填写一个，可同时填写多个不同类型的id。

## 最后

该项目仅用于学习交流，请尊重知乎用户的版权，不要随意爬取、随意传播内容。为此，项目中的api模块仅保留单个回答和单篇文章的api，其余api未发布，后期可能会提供极少量爬取的json文件，完全移除api模块。


## 更新
- 添加新功能，可以将一个问题的所有或部分回答合并成一个markdown文件。