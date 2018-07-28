**项目概述**
利用泰坦尼克号上2224名乘客及船员的数据子集，包括了人口统计资料和乘客信息，对其进行分析以探索乘客的生还率主要与哪些因素有关。详细信息请访问链接 ：
[Titanic: Machine Learning from Disaster](https://www.kaggle.com/c/titanic/data)    
  
**Tableau故事：**
- [Initial Version](https://public.tableau.com/profile/cheng.ming1551#!/vizhome/story_initial/Story?publish=yes)
- [Final Version](https://public.tableau.com/profile/cheng.ming1551#!/vizhome/Titanic_story_final_0/Story?publish=yes)
 
**总结：**
对Titanic数据集进行探索，经一定程度的分析有如下四个小结：
- 探索性别因素对生还率的影响，发现女性生还的比例总体显著高于男性；
- 探索年龄因素对生还率的影响，发现年龄较小的生还率相对较高；
- 探索乘客兄弟姐妹/配偶数量对生还率的影响，发现乘客的兄弟姐妹/配偶数量越多，则相对生还率越低；
- 将船舱等级因素与性别因素联合分析，发现女性中社会等级高（数字小）的，生还比例极大。


总体结论：
- 总体来讲，生还率主要受三大因素影响：性别、年龄和社会阶层，女性高于男性，年龄小的高于年龄大的，社会阶层高的大于社会阶层低的。由此可见，虽然此事故在历史上有著名的“让妇女和孩子先走”的经典故事，但其真实情况也任然建立在社会阶层的基础上。

**设计：** 
 - 对于类别变量vs数值变量，可用箱型图展示三种社会等级的人群的不同年龄分布情况；
- 用饼状图有助于显示百分比，例如社会等级占比、不同性别/社会等级的生还率等可视化；
- 采用不同的颜色编码对人群的生还情况进行区别，考虑到红绿色盲人群的情况，用蓝色代表Live，灰色代表Dead；
- 用柱状图可以较为直观地展示显示变量的具体数目，且不同柱间的对比也可用于分析生还率的高低。

**反馈：** 
- 初始版本直接开始分析不同变量对生还率的影响，使观众不能清晰地了解数据背景。经反馈后，在开始位置利用箱型图和饼图来展现乘客基本的年龄和社会等级的分布。
- 初始版本中用红色/绿色来分别代表乘客的Dead/Live两种状态，经反馈该两种颜色对于红绿色盲人群不友好，且红绿色盲在人群中占比较高。经过反馈后，改用蓝色表示Live状态，灰色表示Dead状态。
- 初始版本中全部用柱状图来对比不同条件下的乘客存活率，对于百分比的表示不够直观。经反馈后改进，用饼状图并列对比的方式改进部分分析。
- 初始版本中将pclass按照“客舱等级”推理至“社会等级”进行解释，虽然社会等级和客舱等级有相关性，但此处不能对数据进行过度解读。经过反馈后，修改相关表述方法。
- 初始版本中故事1中的饼图需要拖拽，显示效果不够好。经反馈后在排版布局上做出适当调整，且为故事中所有的饼图均添加数量标签，使信息表达更全面。
- 初始版本中选择最终结果以故事呈现，其余过多的工作表将影响浏览体验。经过反馈后，隐藏所有工作表，只保留故事结构。

**资源：** 
- [Kaggle - Titanic: Machine Learning from Disaster](https://www.kaggle.com/c/titanic/data)
- [Tableau - Create a dashboard](https://onlinehelp.tableau.com/current/pro/desktop/en-us/dashboards_create.html)
- [个人Github - MLND项目](https://github.com/mchengny/Titanic_survival_exploration)
