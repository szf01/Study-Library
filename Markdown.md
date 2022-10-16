#***Markdown基本语法*** {#index}

##1.粗体和斜体
######代码：
        *斜体*
        **粗体**
        ***加粗斜体***
        ~~删除线~~

######显示效果：
- *斜体*
- **粗体**
- ***加粗斜体***
- ~~删除线~~


##2.分级标题
#####代码：
    ####1.#一级标题
    ####2.##二级标题
    ####3.###......


##3.超链接
####3.1 行内式
######语法说明：
[]里写链接文字，()里写链接地址, ()中的”“中可以为链接指定title属性，title属性可加可不加。title属性的效果是鼠标悬停在链接上会出现指定的 title文字。[链接文字](链接地址 “链接标题”)’这样的形式。链接地址与链接标题前有一个空格。(注意都要是英文标点)
######代码：
    1.这个是[csdn原帖](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)
    2.这个是[csdn原帖](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187 "csdn原帖")

######显示效果：
- 1.这个是[csdn原帖](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)
- 2.这个是[csdn原帖](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187 "csdn原帖")

####3.2参考式
######语法说明：
参考式链接分为两部分，文中的写法 [链接文字][链接标记]，在文本的任意位置添加[链接标记]:链接地址 “链接标题”，链接地址与链接标题前有一个空格。

如果链接文字本身可以做为链接标记，你也可以写成[链接文字][] 
[链接文字]：链接地址的形式，见代码的最后一行。
######代码:
    1. 我经常去的几个网站[Google][1]、[Leanote][2]以及[自己的博客][3]
    2. [Leanote 笔记][2]是一个不错的[网站][]。
    3. [1]:http://www.google.com "Google"
    4. [2]:http://www.leanote.com "Leanote"
    5. [3]:http://http://blog.leanote.com/freewalk "梵居闹市"
    6. [网站]:http://http://blog.leanote.com/freewalk
######显示效果：
1..我经常去的几个网站[Google][1]、[Leanote][2]
2.[Leanote 笔记][2]是一个不错的[网站][]。

[1]:https://www.google.cn/"Google"
[2]:https://leanote.com/ "Leanote"

[网站]:https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187

####3.3自动链接
######语法说明：
Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用<>包起来， Markdown 就会自动把它转成链接。一般网址的链接文字就和链接地址一样，例如：

######代码：
    1. <http://example.com/>
    2. <address@example.com>

######显示效果：
- 1. <http://example.com/>
- 2. <address@example.com>

##4.锚点
######描述：
- 网页中，锚点其实就是页内超链接，也就是链接本文档内部的某些元素，实现当前页面中的跳转。比如我这里写下一个锚点，点击回到目录，就能跳转到目录。 在目录中点击这一节，就能跳过来。还有下一节的注脚。这些根本上都是用锚点来实现的。


######注意： 
1. Markdown Extra 只支持在标题后插入锚点，其它地方无效。 
2. Leanote 编辑器右侧显示效果区域暂时不支持锚点跳转，所以点来点去发现没有跳转不必惊慌，但是你发布成笔记或博文后是支持跳转的。

######语法描述： 
- 在你准备跳转到的指定标题后插入锚点{#标记}，然后在文档的其它地方写上连接到锚点的链接。

######代码:
    跳转到[目录]（#index）
######显示效果：
- 跳转到[目录]（#index）
##5.列表
####5.1无序列表
######描述：
- 使用 *，+，- 表示无序列表。
######代码：
    - 无序列表项 一
    - 无序列表项 二
    - 无序列表项 三
######显示效果：
- 无序列表项一
- 无序列表项 二
- 无序列表项 三

####5.2有序列表
######描述：
- 有序列表则使用数字接着一个英文句点，再加空格
######代码：
    1. 有序列表项 一
    2. 有序列表项 二
    3. 有序列表项 三
######显示效果：
1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三
####5.3定义型列表
######语法说明：
- 定义型列表由名词和解释组成。一行写上定义，紧跟一行写上解释。解释的写法:紧跟一个缩进(Tab),注意冒号是英文
######代码：
    名词
    :  这里是名词的解释
######显示效果：
名词
:  这里是名词的解释
####5.4列表缩进
######语法说明：
- 列表项目标记通常是放在最左边，但是其实也可以缩进，最多 3 个空格，项目标记后面则一定要接着至少一个空格或制表符。
- 要让列表看起来更漂亮，你可以把内容用固定的缩进整理好（显示效果与代码一致）
######代码：
    *   轻轻的我走了， 正如我轻轻的来； 我轻轻的招手， 作别西天的云彩。
    那河畔的金柳， 是夕阳中的新娘； 波光里的艳影， 在我的心头荡漾。 
    软泥上的青荇， 油油的在水底招摇； 在康河的柔波里， 我甘心做一条水草！ 
    *   那榆荫下的一潭， 不是清泉， 是天上虹； 揉碎在浮藻间， 沉淀着彩虹似的梦。 
    寻梦？撑一支长篙， 向青草更青处漫溯； 满载一船星辉， 在星辉斑斓里放歌。 
    但我不能放歌， 悄悄是别离的笙箫； 夏虫也为我沉默， 沉默是今晚的康桥！ 
    悄悄的我走了， 正如我悄悄的来； 我挥一挥衣袖， 不带走一片云彩。
######显示效果：
*   轻轻的我走了， 正如我轻轻的来； 我轻轻的招手， 作别西天的云彩。
那河畔的金柳， 是夕阳中的新娘； 波光里的艳影， 在我的心头荡漾。 
软泥上的青荇， 油油的在水底招摇； 在康河的柔波里， 我甘心做一条水草！ 
*   那榆荫下的一潭， 不是清泉， 是天上虹； 揉碎在浮藻间， 沉淀着彩虹似的梦。 
寻梦？撑一支长篙， 向青草更青处漫溯； 满载一船星辉， 在星辉斑斓里放歌。 
但我不能放歌， 悄悄是别离的笙箫； 夏虫也为我沉默， 沉默是今晚的康桥！ 
悄悄的我走了， 正如我悄悄的来； 我挥一挥衣袖， 不带走一片云彩。
####5.5包含段落的列表
######语法说明：
- 列表项目可以包含多个段落，每个项目下的段落都必须缩进 4 个空格或是 1 个制表符（显示效果与代码一致）：
- 如果你每行都有缩进，看起来会看好很多，当然，再次地，如果你很懒惰，Markdown 也允许(好像不太对)
######代码：
    *   轻轻的我走了， 正如我轻轻的来； 我轻轻的招手， 作别西天的云彩。
    那河畔的金柳， 是夕阳中的新娘； 波光里的艳影， 在我的心头荡漾。 
    软泥上的青荇， 油油的在水底招摇； 在康河的柔波里， 我甘心做一条水草！

        那榆荫下的一潭， 不是清泉， 是天上虹； 揉碎在浮藻间， 沉淀着彩虹似的梦。 
    寻梦？撑一支长篙， 向青草更青处漫溯； 满载一船星辉， 在星辉斑斓里放歌。 
    但我不能放歌， 悄悄是别离的笙箫； 夏虫也为我沉默， 沉默是今晚的康桥！ 
    *    悄悄的我走了， 正如我悄悄的来； 我挥一挥衣袖， 不带走一片云彩。
######显示效果：
*   轻轻的我走了， 正如我轻轻的来； 我轻轻的招手， 作别西天的云彩。
那河畔的金柳， 是夕阳中的新娘； 波光里的艳影， 在我的心头荡漾。 
软泥上的青荇， 油油的在水底招摇； 在康河的柔波里， 我甘心做一条水草！

    那榆荫下的一潭， 不是清泉， 是天上虹； 揉碎在浮藻间， 沉淀着彩虹似的梦。 
寻梦？撑一支长篙， 向青草更青处漫溯； 满载一船星辉， 在星辉斑斓里放歌。 
但我不能放歌， 悄悄是别离的笙箫； 夏虫也为我沉默， 沉默是今晚的康桥！ 
*    悄悄的我走了， 正如我悄悄的来； 我挥一挥衣袖， 不带走一片云彩。
####5.6包含代码区块的引用
####5.7一个特殊情况
- 见[csdn原文](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)

##6.引用
- 见[csdn原文](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)

##7.插入图像
####7.1行内式
######语法说明：
- 语法说明：![图片Alt](图片地址 “图片Title”)
- 语法中图片Alt的意思是如果图片因为某些原因不能显示，就用定义的图片Alt文字来代替图片。 图片Title则和链接中的Title一样，表示鼠标悬停与图片上时出现的文字。 Alt 和 Title 都不是必须的，可以省略，但建议写上。
######代码：
    ![美丽花儿](http://ww2.sinaimg.cn/large/56d258bdjw1eugeubg8ujj21kw16odn6.jpg "美丽花儿")
######显示效果：
![海贼王](https://image.so.com/view?q=%E5%9B%BE%E7%89%87%E9%BB%91%E7%99%BD%20%E6%B5%B7%E8%B4%BC%E7%8E%8B&src=tab_www&inact=0&correct=%E5%9B%BE%E7%89%87%E9%BB%91%E7%99%BD%20%E6%B5%B7%E8%B4%BC%E7%8E%8B&ancestor=list&cmsid=d2b28f3b4c6b16d34c90a30dfb5626c6&cmras=6&cn=0&gn=0&kn=0&crn=0&bxn=0&fsn=60&cuben=0&pornn=0&manun=0&adstar=0&clw=267#id=024d4cbf1c35ed5580bd152af36ca34f&prevsn=0&currsn=60&ps=118&pc=59)
####7.2参考式
- 见[csdn原文](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)

##内容目录、注脚、LaTeX公式
- 见[csdn原文](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)

##流程图
- 语法参考[网站](http://flowchart.js.org/)
##表格
######语法说明：
1. 不管是哪种方式，第一行为表头，第二行分隔表头和主体部分，第三行开始每一行为一个表格行。
2. 列于列之间用管道符|隔开。原生方式的表格每一行的两边也要有管道符。
3. 第二行还可以为不同的列指定对齐方向。默认为左对齐，在-右边加上:就右对齐。
######代码：
1. 简单方式

        学号|姓名|分数
        -|-|-
        小明|男|75
        小红|女|79
        小陆|男|92
2. 原生方式

        |学号|姓名|分数|
        |-|-|-|
        |小明|男|75|
        |小红|女|79|
        |小陆|男|92|
3. 为表格第二列指定方向：

        产品|价格
        -|-:
        Leanote 高级账号|60元/年
        Leanote 超级账号|120元/年
######显示效果：
学号|姓名|分数
-|-|-
小明|男|75
小红|女|79
小陆|男|92

|学号|姓名|分数|
|-|-|-|
|小明|男|75|
|小红|女|79|
|小陆|男|92|

产品|价格
-|-:
Leanote 高级账号|60元/年
Leanote 超级账号|120元/年

##分割线、代码
- 见[csdn原文](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166485966716782417095701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166485966716782417095701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-52551362-null-null.142^v51^new_blog_pos_by_title,201^v3^control_2&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187)






