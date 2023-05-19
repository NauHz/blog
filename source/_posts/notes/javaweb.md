---
title: JavaWeb
tags:
  - JavaWeb
  - 编程
categories: 编程笔记
cover: /img/javaweb.JPG
abbrlink: 99720b1c
top_img: '#0f4c81'
---

{% timeline MyEclipse+JDK+Tomcat,blue %}

<!-- timeline JDK配置 -->
1. 解压JDK安装完后配置系统环境
2. 新建变量名：JAVAHOME，变量值：C:\Program Files\Java\jdk1.7.0_79
3. 新建变量名：CLASSPATH，变量值：.;%JAVAHOME%\lib\dt.jar;%JAVAHOME%\lib\tools.jar
4. 修改变量Path，变量值添加%JAVAHOME%\bin，原本后面没有分号加分号
5. cmd验证、输入java或javac，运行出现用法表示配置环境成功
<!-- endtimeline -->

<!-- timeline Tomcat -->
1. 安装Tomcat，所选项服务器启动端口需要的可以修改8088或8089之类
2. 选择需要的jdk路径
3. 最后安装成功有两个勾选项，取消勾选
<!-- endtimeline -->

<!-- timeline MyEclipse整合Tomcat -->
1. 打开Myeclipse默认文件路径打开，输入注册码名称sojson.com，序列号：fLR8ZC-855575-7850765797016498
2. 点击选项栏window打开preferences窗口找到Java拉开扩展打开Installed JREs选择需要的jdk
3. 继续往下翻找到Servers点击扩展选选择Runtime Environments导入（add）需要的Tomcat版本
4. 在下面信息框中的Servers中右键tomcat运行没有蓝字报错说明运行成功
<!-- endtimeline -->

{% endtimeline %}

# 实验一
```html
<fieldset>
<legend>注册新用户</legend>	
<!-- 表单数据的提交方式为POST -->
<form action="#" method="post">
    <table cellpadding="2" align="center">
        <tr>
            <td align="right">用户名:</td>
            <td>
                <!-- 1.文本输入框控件 -->
                <input type="text" name="username" />	 
            </td>
        </tr>
        <tr>
            <td align="right">密码:</td>
            <!-- 2.密码输入框控件 -->
            <td><input type="password" name="password" /></td>
        </tr>
        <tr>
            <td align="right">性别:</td>
            <td>
        <input type="radio" name="gender" value="male" /> 男 
        <input type="radio" name="gender" value="female" /> 女 
            </td>
        </tr>
        <tr>
            <td align="right">兴趣:</td>
            <td>
            <!-- 4.复选框控件 -->
  <input type="checkbox" name="interest" value="film" /> 看电影
  <input type="checkbox" name="interest" value="code" /> 敲代码
  <input type="checkbox" name="interest" value="game" /> 玩游戏
            </td>
        </tr>
        <tr>
            <td align="right">头像:</td>
            <td>
                <!-- 5.文件上传控件 -->
                <input type="file" name="photo" />
            </td>
        </tr>
        <tr>
            <td colspan="2"  align="center">
                <!-- 6.提交按钮控件 -->
                <input type="submit" value="注册" />  
                <!-- 7.重置按钮控件，单击后会清空当前form -->
                <input type="reset" value="重填" />    
            </td>
        </tr>
    </table>
</form>
</fieldset>

```