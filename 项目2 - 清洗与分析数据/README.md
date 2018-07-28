# 清洗与数据分析
----------------------------------------
## 项目概述

实世界的数据一般不干净。使用 Python 和 Python 库，你可以收集各种来源和形式的数据，评估质量和清洁度，然后进行清洗。这叫做数据清洗。你可以在 Jupyter 记事本中记录清洗过程，然后使用 Python (及其库) 和/或 SQL 进行分析和可视化，展示清洗过程。

你将要清洗 (分析和可视化) 的数据集是推特用户 [@dog_rates](https://twitter.com/dog_rates) 的档案, 也叫做 [WeRateDogs](https://en.wikipedia.org/wiki/WeRateDogs)。推特用户 WeRateDogs 以诙谐幽默的方式对人们的宠物狗评级。这些评级通常以 10 作为分母。但是分子呢？分子一般大于 10。 11/10、12/10、13/10 等，为什么呢？因为 "[Brent 它们是好狗](http://knowyourmeme.com/memes/theyre-good-dogs-brent)。" WeRateDogs 拥有四百多万关注者，曾受到国际媒体的报道。

WeRateDogs 为优达学城的这个项目提供他们推特资料的独占访问。这个档案包括基本的推特数据，如截止到 2017 年 4 月 1 日的 5000 多条推特。很快会有更多内容。  

![Alt text](https://github.com/CHENG-MING/Wrangle_and_Analyze_data/raw/master/report/Figures/dog-rates-social.jpg)

## 项目动机  
### 背景

你的目标：清洗 WeRateDogs 推特数据，创建有趣可靠的分析和可视化。推特档案很大，但是只包括基本的推特信息。对 "_Wow!_" 进行收集、评估和清洗，是分析和可视化应该做的。
  
### 数据

**完善推特档案**  

WeRateDogs 推特档案包括基本的推特信息，如 5000 多条推特，但并不包括所有数据。不过档案中有一列包括每个推特文本，我可以用来提取评级、狗的名字和 "地位" (即 doggo、floofer、pupper 和 puppo)。  
  
![Alt text](https://github.com/CHENG-MING/Wrangle_and_Analyze_data/raw/master/report/Figures/extract.png)

**Twitter API 的附加数据**  

回到推特档案的基础信息：转发用户和喜爱用户是两个遗漏的列。幸运的是，从推特 API 中，任何人都可以收集到附加数据。其实，"任何人" 都能获取至少最近的 3000 条推特数据。但是因为你拥有 WeRateDogs 推特档案和专门的推特 ID，你可以收集到所有的 5000 多条推特。你将会查询推特的 API 收集这个重要数据。

_特别提示：_ 如果你无法访问 Twitter的话，我们将直接给你提供返回的 Twitter 数据。你可以 [右键点击这里选择另存为](https://raw.githubusercontent.com/udacity/new-dand-advanced-china/master/%E6%95%B0%E6%8D%AE%E6%B8%85%E6%B4%97/WeRateDogs%E9%A1%B9%E7%9B%AE/tweet_json.txt) 下载。该文件为 `txt` 格式，每一行为一条独立的 twitter 信息，格式为 `JSON` 。该文件比较大，下载可能需要几分钟。  

**图像预测文件**

一件更酷的事情：我通过一个 [神经网络](https://www.youtube.com/watch?v=2-Ol7ZB0MmU) 运行 WeRateDogs 推特档案中的所有图片，这个神经网络可以对狗的品种分类。结果：对图片预测 (只含前三名) 的表格包括每个推特 ID、图片 URL 和最自信预测对应的图片编号 (由于推特最多包含 4 个图片，所以编号为 1 到 4)。  

所以在这个图标的最后一个中：

*   tweet_id 是推特 URL 最后一部分，位于 "_status/_" 后面 → [https://twitter.com/dog_rates/status/889531135344209921](https://twitter.com/dog_rates/status/889531135344209921)
*   p1 是对推特中图片算法 #1 的预测 → **金毛犬**
*   p1_conf 是 #1 预测中算法的可信度 → **95%**
*   p1_dog 是 #1 预测是否是狗的品种 → **真**
*   p2 是算法的第二个最有可能的预测 → **拉布拉多犬**
*   p2_conf 是 #2 预测中算法的可信度 → **1%**
*   p2_dog 是 #2 预测是否是狗的品种 → **真**
*   等等

### 关键要点

清洗这个项目的数据时要牢记几个要点：

*   我们只需要含有图片的原始评级 (不包括转发)。
*   充分评估和清洗整个数据集需要巨大努力，所以只有一些问题 (至少 8 个质量问题和 2 个清洁度问题) 的子集需要进行评估和清洗。
*   根据 [清洗数据](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html) 的规则，清洗包括合并数据的独立内容。
*   如果分子评级超过分母评级，不需要进行清洗。这个 [特殊评级系统](http://knowyourmeme.com/memes/theyre-good-dogs-brent) 是 WeRateDogs 人气度较高的主要原因。  

## 项目细节  
  
你在这个项目中的任务如下：

*   清洗数据包括：
    *   收集数据
    *   评估数据
    *   清洗数据
*   对清洗过的数据进行储存、分析和可视化
*   汇报 1) 你的数据清洗过程 和 2) 你的数据分析和可视化

### 收集项目数据

收集下面描述的三份数据，在 Jupyter Notebook 命名为 `wrangle_act.ipynb` ：

1.  WeRateDogs 推特档案。这个数据都可以从[Github repo](https://github.com/udacity/new-dand-advanced-china/tree/master/%E6%95%B0%E6%8D%AE%E6%B8%85%E6%B4%97/WeRateDogs%E9%A1%B9%E7%9B%AE)中下载到。
2.  推特图片预测，即根据神经网络，出现在每个推特中狗的品种 (或其他物体、动物等)。这个文件目前也在[Github repo](https://github.com/udacity/new-dand-advanced-china/tree/master/%E6%95%B0%E6%8D%AE%E6%B8%85%E6%B4%97/WeRateDogs%E9%A1%B9%E7%9B%AE)中，你需要使用Python 的 Requests 和对应的URL ([https://raw.githubusercontent.com/udacity/new-dand-advanced-china/master/%E6%95%B0%E6%8D%AE%E6%B8%85%E6%B4%97/WeRateDogs%E9%A1%B9%E7%9B%AE/image-predictions.tsv](https://raw.githubusercontent.com/udacity/new-dand-advanced-china/master/%E6%95%B0%E6%8D%AE%E6%B8%85%E6%B4%97/WeRateDogs%E9%A1%B9%E7%9B%AE/image-predictions.tsv)) 来进行编程下载。
3.  每条推特的数据，至少要包含转发数（retweet_count）和喜欢数（favorite_count），以及任何你觉得有趣的额外数据。在 WeRateDog 推特档案中的推特 ID 中，使用 Python [Tweepy](http://www.tweepy.org/) 库查询 API 中每个 JSON 数据，把每个推特的 JSON 数据的完整集合存储到一个名为 `tweet_json.txt` 的文件中。每个推特的 JSON 数据应当写入单独一行。然后将这个 .txt 文件逐行读入一个 pandas DataFrame 中，（至少）包含 tweet ID、retweet_count 和 favorite_count 字段。_注释：不要包含你项目提交的推特 API 密钥和访问令牌。_

### 评估项目数据

收集上述数据的每个内容后，从视觉上和程序上，对质量和清洁度进行数据评估。在你的 `wrangle_act.ipynb`Jupyter Notebook 中查找和记录至少 **8 个质量问题** 和 **2 个清洁度问题**。为了符合规范，必须评估符合项目动机的问题 (参见上一页的 _关键要点_ 标题)。

### 清洗项目数据

评估时清洗你记录的每个问题。在 `wrangle_act.ipynb` 完成清洗。结果应该为优质干净的主要 pandas DataFrame (如有，或为多个 DataFrame)。必须评估符合项目动机的问题。

### 存储、分析和可视化项目数据

在 CSV 文件中存储洁净的数据，命名为 `twitter_archive_master.csv`。如果因为清洁需要多个表格，存在附加文件，要给这些文件合理命名。另外，你可以把清洗后的数据存储在 SQLite 数据库中 (如有需要也可以提交)。

在 `wrangle_act.ipynb` Jupyter Notebook 中对清洗后的数据进行分析和可视化。必须生成至少 **3 个见解和 1 个可视化**。

### 项目汇报

创建一个 **300-600 字书面报告** 命名为 `wrangle_report.pdf`，可以简要描述你的清洗过程。这可以作为内部文档。

创建一个 **250 字以上的书面报告** 命名为 `act_report.pdf`，可以沟通观点，展示你清洗过数据后生成的可视化内容。这可作为外部文档，如博客帖子或杂志文章。
