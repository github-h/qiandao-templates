# 整理qiandao.today可用的har

#### 此分支为**自用备份**。只保留自己需要的。均经过测试，不定期更新，不保证可用

#### ~~此分支将尽量按照下列表格格式书写说明，懒了就不写了~~  懒得写了，直接删了

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

#### ``用空的 cookie 测试返回结果``

![第一条补充](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第一条补充.jpg)

2. 对于**第二条**请求，此为签到请求。应该判断签到请求是否正确，是否是假签到（签到失败，但返回**200**状态码，然后模板认为签到成功）对于此类的需要加以文字辅助判断。

#### ``用空的 formhash/cookie 测试返回结果``

![第二条补充](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第二条补充.jpg)

3. 对于**第三条**请求，此为验证是否签到成功+获取积分步骤。自行对比签到前后网站内容变化以抓取辨识信息。对于Discuz来说，开始签到按钮为图片无法捕获，便用其他文字替代。同时自行寻找需要获取的信息以便提交日志。同样对于Discuz来说，文字颜色为积分捕获的最佳标识。

#### ``需要用真实有效的 cookie 来提取积分，提前留存好签到前后网站样式以做对比判断是否签到成功``

![第三条补充](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第三条补充.jpg)

4. 对于**第四条**请求，此为提交日志。提交后的日志可以在签到平台日志选项中查看到，最常用的为[插入字符串替换](https://hexo.aragon.wang/2020/04/16/%E7%AE%80%E5%8D%95%E5%B7%A5%E5%85%B7api/#3-1-%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%9B%BF%E6%8D%A2-replace)，后续平台可能会上线本地转换功能，具体用法自行研究。

#### ``需要在上一个请求中获取到 log_value ,将此请求的变量写为 __log__ 同时加以正则捕获即可提交日志，务必提前测试好是否正常显示``

![第四条补充 (1)](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第四条补充(1).jpg)
![第四条补充 (2)](https://raw.githubusercontent.com/github-h/qiandao-templates/self-bak/pic/第四条补充(2).jpg)

## Tips

1. 但凡是以 **Authorization** 作为认证标识的，大多都可在登录请求返回的包中找到该值，可能参数为 **Token** 。也就是说可以把定期会过期的 **Authorization** 转为用户名密码登录模板达到不过期效果（如果登陆时不需要验证码）
2. **Authorization** 该值通常以 **Bearer** 开头，可以去头放到 [JSON Web Tokens](https://jwt.io/#debugger-io) 尝试解密
