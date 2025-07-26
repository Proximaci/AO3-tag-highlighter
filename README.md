# AO3-tag-highlighter
一个指导文档：通过自定义Site Skin实现对于特定tag的高亮显示。

优点：全平台同步、不需要额外安装插件。电脑上设置完成后登录同一个ao3账号的所有设备都能产生相关效果。

## 步骤
### 1. 创建新的站点皮肤（Site Skin）：
   
   点击ao3首页右上角用户名，在下拉栏选择```Dashboard```，而后选择第四个选项```Skin```。
   在```My Site Skins```下面一行点击```Create Site Skin```。

### 2. 在CSS栏内输入以下代码：
   ```
   a.tag[href*="关键词1" i]:not([href*="no%20" i]):not([href*="not%20" i]),  
   a.tag[href*="关键词2" i]:not([href*="no%20" i]):not([href*="not%20" i]),
   a.tag[href*="关键词3" i]:not([href*="no%20" i]):not([href*="not%20" i])
   {
    color: #20B2AA !important;
   }
   ```
   将以上的```关键词1``` ```关键词2``` ```关键词3```替换为你想高亮的tag关键词，大小写无所谓，如果需要区分大小写则删去关键词后面的```i```。如果想要多种颜色就整段复制粘贴并重新写。增减关键词数量/行数时小心行末的逗号，但最后一个行末没有逗号。
   
   注意，关键词内部所有空格``` ```需要用```%20```代替，斜线```/```必须用```*s*```代替。其他符号可以参考浏览器地址栏内的写法。
   
   如果需要改变颜色，请修改color一行的颜色代码。
   
   如果需要更多样式，请在color一行下面、```{``` ```}```这两个括号之间添加：
   
   - 加粗：```font-weight: bold;```
     
   - 背景色：```background-color: #252525;```
     
   - 边框：```border: 1px solid #b30000;```
     
   解释：
   
   - 以Omega Verse为例，```a.tag[href*="Omega%20Verse" i]```即为选中所有精确包含“Omega Verse”的tag；只有omega或只有verse或OmegaVerse都不算在内。
   - 后面紧跟着的```:not([href*="no%20" i])```意为去除所有包含“no ”（注意这个空格）的tag，所以形如“No Omega Verse”的tag就会被排除，但不会去除“Now Omega Verse”。
   - 如果需要进一步自定义规则，请小心所有的标点符号。
   - 如果多个规则重复，请把需要优先生效的规则后面加上```!important```，例如```color: #20B2AA !important;```会覆盖掉其他的规则，如```color: #015AB9;```。
     
### 3. 如果正在使用非默认皮肤：
   
   在CSS栏下方点击```Advanced```旁边的```Show ↓```，点击```Parent Skins```一栏内的```Add parent skin```，输入并选择正在使用的皮肤名称。可以在 首页-My Preferences-Your site skin 找到相关名称。

### 4. 如果想要统一改变所有relationships、characters、additional tags的样式：

   另开一段，输入代码，以改变颜色为例：
   - relationships（关系/配对）：
     ```
     .tags .relationships a
     {
      background-color: #015AB9;
     }```
   - characters（角色）：
     ```
     .tags .characters a
     {
      background-color: #009191;
     }```
   - additional tags（其他tag）：
     ```
     .tags .freeforms a
     {
      background-color: #06982D;
     }```

### 5. 提交：

   回到上面，在```Title*```一栏输入名称。名称为必填项并且不可重复。如果重名，之后点击```Submit```提交后将在页面上方看见相关提示（```Sorry! We couldn't save this skin because:
Title must be unique```）；此时换一个名字重新提交。

   此后可以在 首页-Dashboard-Skins 中修改或编辑创建的皮肤。

   如果有其他报错/代码相关问题请寻求AI帮助。

### 6. 参考资料：

   https://www.reddit.com/r/AO3/comments/oxjpiv/highlight_specific_tags_using_a_skin/
