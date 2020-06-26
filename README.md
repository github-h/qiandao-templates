# 整理qiandao.today可用的har

#### 此分支为**自用备份**。只保留自己需要的。均经过测试，不定期更新，不保证可用

#### 此分支将尽量按照下列表格格式书写说明，懒了就不写了

## 模板书写规范

**以标准的Discuz论坛签到为例**

![抓取请求](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/抓取请求.jpg)

### 抓取请求

签到请求分为 **4** 部分

1. 首先使用用户提供的 **cookie** 登陆，获取页面的 **formhash** 值，进入签到界面

2. 将获取的 **formhash** 作为变量填入请求中，提交签到请求

3. 重新进入签到界面，判断是否签到成功和获取签到情况

4. 将签到情况提交到日志

#### 补充模板

补充部分信息使得模板具有纠错功能（判断签到是否成功、登陆是否成功、日志如何输出）

1. 对于**第一条**请求，获取 **formhash** 的同时，应该判断当前**登录信息/cookie**是否有效。有些网站会直接报其他的状态码 **400、300** 等。此时设置 **200**作为判断信息即可。对于一律返回 **200** 的，必须要以其他形式判断，如文字。

#### ``用空的 **cookie** 测试返回结果``

![第一条补充](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第一条补充.jpg)

2. 对于**第二条**请求，此为签到请求。应该判断签到请求是否正确，是否是假签到（签到失败，但返回**200**状态码，然后模板认为签到成功）对于此类的需要加以文字辅助判断。

#### ``用空的**formhash/cookie**测试返回结果``

![第二条补充](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第二条补充.jpg)

3. 对于**第三条**请求，此为验证是否签到成功+获取积分步骤。自行对比签到前后网站内容变化以抓取辨识信息。对于Discuz来说，开始签到按钮为图片无法捕获，便用其他文字替代。同时自行寻找需要获取的信息以便提交日志。同样对于Discuz来说，文字颜色为积分捕获的最佳标识。

#### ``需要用真实有效的 **cookie** 来提取积分，提前留存好签到前后网站样式以做对比判断是否签到成功``

![第三条补充](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第三条补充.jpg)

4. 对于**第四条**请求，此为提交日志。提交后的日志可以在签到平台日志选项中查看到，最常用的为[插入字符串替换](https://hexo.aragon.wang/2020/04/16/%E7%AE%80%E5%8D%95%E5%B7%A5%E5%85%B7api/#3-1-%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%9B%BF%E6%8D%A2-replace)，后续平台可能会上线本地转换功能，具体用法自行研究。

#### ``需要在上一个请求中获取到 **log_value** ,将此请求的变量写为 **__log__** 同时加以正则捕获即可提交日志，务必提前测试好是否正常显示``

![第四条补充 (1)](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第四条补充(1).jpg)
![第四条补充 (2)](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第四条补充(2).jpg)

## 网站

Tips:链接里最好使用raw.githubusercontent.com的模板地址，其他的链接没有测试过
网站|作者|链接|变量说明|备注/日志
:-: | :-: | :-: | :-: |:-:
summer-plus(原south-plus)|[AragonSnow](https://github.com/AragonSnow)<br>[github-h](https://github.com/github-h)|[summer-plus(原south-plus).har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/summer-plus(%E5%8E%9Fsouth-plus).har)|pwd 密码<br> user 用户名|https://www.summer-plus.net/
ZodGame论坛|[github-h](https://github.com/github-h)|[ZodGame论坛.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/ZodGame%E8%AE%BA%E5%9D%9B.har)|cookie|https://zodgame.xyz
星空论坛seikuu|[github-h](https://github.com/github-h)|[星空论坛seikuu.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%E6%98%9F%E7%A9%BA%E8%AE%BA%E5%9D%9Bseikuu.har)|cookie|https://bbs2.seikuu.com/
网易云音乐-电脑 AND 手机|[qiandao.today公共模板](https://qiandao.today/tpls/public)|[网易云音乐-电脑 AND 手机.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e7%bd%91%e6%98%93%e4%ba%91%e9%9f%b3%e4%b9%90-%e7%94%b5%e8%84%91+AND+%e6%89%8b%e6%9c%ba.har)|cookie|https://music.163.com/
吾爱破解|[github-h](https://github.com/github-h)|[吾爱破解.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e5%90%be%e7%88%b1%e7%a0%b4%e8%a7%a3.har)|cookie|https://www.52pojie.cn/
哥特动漫王国|[github-h](https://github.com/github-h)|[哥特动漫王国.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e5%93%a5%e7%89%b9%e5%8a%a8%e6%bc%ab%e7%8e%8b%e5%9b%bd.har)|cookie|https://www.gtloli.net/forum.php
萌出血动漫论坛|[github-h](https://github.com/github-h)|[萌出血动漫论坛.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e8%90%8c%e5%87%ba%e8%a1%80%e5%8a%a8%e6%bc%ab%e8%ae%ba%e5%9d%9b.har)|cookie|http://www.bbsmcx.com/forum.php
ArcTime字幕平台|[github-h](https://github.com/github-h)|[ArcTime字幕平台.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/ArcTime%e5%ad%97%e5%b9%95%e5%b9%b3%e5%8f%b0.har)|用户名<br>密码|http://m.arctime.cn/
柚坛社区|[github-h](https://github.com/github-h)|[柚坛社区.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e6%9f%9a%e5%9d%9b%e7%a4%be%e5%8c%ba.har)|cookie|http://www.miuibbs.cn/
keylol(原SteamCN蒸汽论坛)|[github-h](https://github.com/github-h)|[keylol(原SteamCN蒸汽论坛).har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/keylol(%e5%8e%9fSteamCN%e8%92%b8%e6%b1%bd%e8%ae%ba%e5%9d%9b).har)|cookie|https://keylol.com/
机锋论坛|[github-h](https://github.com/github-h)|[机锋论坛.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e6%9c%ba%e9%94%8b%e8%ae%ba%e5%9d%9b.har)|cookie|http://bbs.gfan.com/
HMOE俱乐部|[github-h](https://github.com/github-h)|[HMOE俱乐部.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/HMOE%e4%bf%b1%e4%b9%90%e9%83%a8.har)|cookie和Authorization|https://club.hmoe.club/
3DMGAME论坛|[github-h](https://github.com/github-h)|[3DMGAME论坛.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/3DMGAME%e8%ae%ba%e5%9d%9b.har)|cookie|https://bbs.3dmgame.com/
花火学院|[github-h](https://github.com/github-h)|[花火学院.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/%e8%8a%b1%e7%81%ab%e5%ad%a6%e9%99%a2.har)|cookie|https://www.say-huahuo.com/
QQNTR论坛|[github-h](https://github.com/github-h)|[QQNTR论坛.har](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/QQNTR%e8%ae%ba%e5%9d%9b.har)|cookie|https://iya.app/
CSDN-专业IT技术论坛|[github-h](https://github.com/github-h)|[CSDN-专业IT技术论坛.har](https://raw.githubusercontent.com/qiandao-today/templates/master/CSDN-%e4%b8%93%e4%b8%9aIT%e6%8a%80%e6%9c%af%e8%ae%ba%e5%9d%9b.har)|用户名+cookie|此为签到模块，记得定期抽奖<br>https://www.csdn.net/
