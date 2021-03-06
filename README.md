# gotunet
golang for TsinghuaUniversityNetwork 清华大学校园网循环检测登录

用于清华大学校园网的不间断连接，这样一来就可以使用远程连接实验室电脑。

# 实现方法

对auth4.tsinghua.edu.cn的网络请求进行分析，得到几个结论：

1. 清华大学校园网登录接口是dologin.php，其中密码采用了MD5加密
2. 登录时与以往的主要区别在于差了一个访问校外网络
3. 经研究，在登录时，不访问校外网络的登录采用的是用户名@tsinghua，而登录校外网络的用户名就是自己的用户名
4. 在进行登录前应先退出用户名@tsinghua的账号，不然无法登录
5. 通过rad_user_info.php进行分析，可以得到返回网页时是未登录，返回空时是不访问校外登录，返回用户名等信息时是正常登录
6. 登录时间间隔限制
6. gotunet检测rad_user_info.php的返回值进行判断是否在线，如果不在，则先进行一波退出操作，主要目的是退出@tsinghua的这个不访问校外登录，然后再进行登录
7. 登录后可以登录usereg.tsinghua.edu.cn查看在线状态确定ip地址，这样即使地址换了也没有关系

参考< https://yushuaizhao.github.io/2018/09/11/%E6%B8%85%E5%8D%8E%E6%A0%A1%E5%9B%AD%E7%BD%91%E8%BF%9C%E7%A8%8B/ >
