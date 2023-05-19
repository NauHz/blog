---
title: C#
date: '2022-11-9 7:11:9'
tags:
  - 实验报告
categories: 博客笔记
cover: /img/A1.JPG
abbrlink: 38ea7f4b
top_img: 'FF6D70'
---

{% progress 90 color 已更上机实验 %}

{% tip warning faa-horizontal animated %}
源码运行环境为win10，vs studio2022
使用源码的同学记得修改：窗口名。（单击学号姓名窗口在Text中把学号姓名修改）
在运行其他实验时请右键实验设为启动项目
{% endtip %}

源码下载：
百度网盘：[C#源码](https://pan.baidu.com/s/19el4I6kZ5hH4dr4MGD6U6A?pwd=fl7o ) 提取码：fl7o
[VS Studio2022](https://visualstudio.microsoft.com/zh-hans/vs/)

# 导入项目
将需要实验的源码下载到指定路径，文件中找到后缀名为`.slh`的文件并打开选择VS Studio运行项目
你也可以在VS Studio中依次点击：{% kbd 文件 %} {% kbd 打开 %} {% kbd 打开项目/解决方案 %}找到源码下载的路径点击后缀名为`.slh`的文件，VS Studio就会直接加载整个项目

{% folding cyan open, 连接数据库方法 %}
创建数据库在视图中没有SQL server对象资源管理的请去Visual Studio Installer中勾选服务器更新
方法一：
在`视图`点击`服务器资源管理器`,右键`数据连接` `添加连接`选择数据源`Microsoft SQL Server 数据库文件 (SqlClient)`在添加连接窗口预览选择源码当中后缀名为`.mdf`的文件，最后一步也是连接数据库最重要的一步在SQLhelper类修改`connStr=“右键数据库属性中复制连接字符串粘贴到此处”`

如果导入数据库还是无法正常运行，那么请自己用方法二创建一个数据库。

方法二：
在`SQL server对象资源管理`中打开下拉框自带的MSSQLLocalDB服务器右键数据库选择`添加新数据库`位置随意，添加好后右键创建好的数据库新建查询，输入SQL语句（对应实验文章中有代码）点执行，跟上面方法一样在SQLhelper类修改`connStr=“右键数据库属性中复制连接字符串粘贴到此处”`

{% endfolding %}


# 实验一
## 四则运算

```c#
//双击即可按钮进入窗体逻辑类（From1.cs）
private void btnResult_Click(object sender, EventArgs e)
{
    int num1 = Convert.ToInt32(txtNum1.Text);
    int num2 = Convert.ToInt32(txtNum2.Text);
    int result = 0;
    switch (cmbOp.SelectedItem.ToString())
    {
        case "+":
        result = num1 + num2;
        break;
        case "-":
        result = num1 - num2;
        break;
        case "*":
        result = num1 * num2;
        break;
        case "/":
        result = num1 / num2;
        break;
    }
        txtResult.Text = result.ToString ();
}
```

## 判断年份是否是闰年

```c#
private void btnJudging_Click(object sender, EventArgs e)
    {
        int year = Convert.ToInt32(txtYear .Text);
        if (year % 4 == 0 && year / 100 != 0 || year % 400 == 0)
        {
            lblShow.Text = string.Format("{0}年是闰年！", year);
        }
        else
        {
            lblShow.Text = string.Format("{0}年是非闰年！", year);
        }
    }
```

# 实验二
## 用户注册

```c#
//注意!名字没有6位英文字母的同学，请把名字长度6改为自己名字对应的数字
private void btbSubmit_Click(object sender, EventArgs e)
{
    string userName = txtName.Text;
    string userPwd = txtPwd.Text;
    string userRsetPwd = txtResetPwd.Text;
    string email = txtEmail.Text;
    Regex regex = new Regex(@"^[A-Za-z]{6,}$");//名字长度
    if (regex.IsMatch(userName))
    {
        MessageBox.Show("用户名格式正确！");
    }
    else
    {
        MessageBox.Show("用户名格式不正确!");
        return;
    }
    if (userPwd.Length >= 6 && userPwd.Length <= 14)
    {
        MessageBox.Show("密码长度符合要求！");
    }
    else
    {
        MessageBox.Show("密码长度不符合要求！");
        return;
    }
    //判断前后两次输入的密码是否一致
    if (txtPwd.Text == txtResetPwd.Text)
    {
        MessageBox.Show("两次输入的密码一致！");
    }
    else
    {
        MessageBox.Show("两次输入的密码不一致！");
        return;
    }

    regex = new Regex(@"^(\w)+(\.\w)*@(\w)+((\.\w+)+)+$");
    if (regex.IsMatch(email))
    {
        MessageBox.Show("邮箱格式正确！");
    }
    else
    {
        MessageBox.Show("邮箱格式不正确！");
        return;
    }
    string message = string.Format("用户注册的信息是:\n用户名：{0}\n密码：{1}\n邮箱：{2}\n", userName, userPwd, email);
    MessageBox.Show("用户信息注册成功！\n" + message);
}
```

## 求输入以英文逗号隔开的整数字符串中最大数最小数元素和

```c#
//不能直接在button1_Click中直接粘贴其他button的事件代码得逐个添加
int[] array1;
string str = "";
string[] strArray;
private void button1_Click(object sender, EventArgs e)
    {
        str = Convert.ToString(txtname.Text);
        strArray = str.Split(',');
        array1 = new int[strArray.Length];
        lblShow.Text += "输入的原始数据为：";
        for (int i = 0; i < strArray.Length; i++)
        {
            array1[i] = Convert.ToInt32(strArray[i]);
            lblShow.Text += (" " + array1[i]);
        }
    }

    private void button2_Click_1(object sender, EventArgs e)
    {
        str = Convert.ToString(txtname.Text);
        strArray = str.Split(',');
        array1 = new int[strArray.Length];
        int max = 0;
        for (int i = 0; i < strArray.Length; i++)
        {
            array1[i] = Convert.ToInt32(strArray[i]);
        }
        for (int i = 2; i < strArray.Length; i++)
        {
            if (array1[max] < array1[i])
            {
                max = i;
            }
        }
        lblShow.Text += ("\n最大值为：" + array1[max]);
    }

    private void button3_Click_1(object sender, EventArgs e)
    {
        str = Convert.ToString(txtname.Text);
        strArray = str.Split(',');
        array1 = new int[strArray.Length];
        int min = 0;
        for (int i = 0; i < strArray.Length; i++)
        {
            array1[i] = Convert.ToInt32(strArray[i]);
        }
        for (int i = 2; i < strArray.Length; i++)
        {
            if (array1[min] > array1[i])
            {
                min = i;
            }
        }
        lblShow.Text += ("\n最小值为：" + array1[min]);
    }

    private void button4_Click_1(object sender, EventArgs e)
    {
        str = Convert.ToString(txtname.Text);
        strArray = str.Split(',');
        array1 = new int[strArray.Length];
        int add = 0;
        for (int i = 0; i < strArray.Length; i++)
        {
            array1[i] = Convert.ToInt32(strArray[i]);
        }
        for (int i = 0; i < strArray.Length; i++)
        {
            add += array1[i];
        }
        lblShow.Text += ("\n和为：" + add);
    }
}
```

# 实验三
## 显示添加学生信息
```c#
private void btnAdd_Click(object sender, EventArgs e)
{
    Student stu = new Student(txtNo.Text, txtName.Text, txtSex.Text, Convert.ToInt32(txtAge.Text), txtSpecialty.Text);
    lblShow.Text = stu.GetMessage();
}
/*单独添加Student类
//注意是public可以在命名空间外访问,Internal只能在命名空间内访问
public class Student
    {
        //1.定义5个私有字段
        private string stuNo;
        private string stuName;
        private string stuSex;
        private int stuAge;
        private string stuSpecialty;
        //2.构造函数初始化字段
        public Student(string myNo, string myName, string mySex, int myAge, string mySpecialty)
        {
            this.stuNo = myNo;
            this.stuName = myName;
            this.stuSex = mySex;
            this.stuAge = myAge;
            this.stuSpecialty = mySpecialty;
        }
        //3.只读属性读取学号、姓名、性别
        public string StuNo
        {
            get { return stuNo; }
        }
        public string StuName
        {
            get { return stuName; }
        }
        public string StuSex
        {
            get { return stuSex; }
        }
        //4.读写属性读写年龄、专业
        public int StuAge
        {
            get
            {
                if (stuAge <= 0) { return 0; }
                else { return stuAge; }
            }
            set { stuAge = value; }
        }
        public string StuSpecialty
        {
            get
            {
                if (stuSpecialty == null) { return "未输入"; }
                else { return stuSpecialty; }
            }
            set { stuSpecialty = value; }
        }
        //5.通过访问属性返回学生信息的方法GetMessage()
        public string GetMessage()
        {
            return string.Format("添加学生信息为：\n学号：{0}\n姓名：{1}\n性别：{2}\n年龄：{3}\n专业：{4}\n", StuNo, StuName, StuSex, StuAge, StuSpecialty);
        }
    }
*/
```

## 实现调用系统时间
```c#
private void btnAdd_Click(object sender, EventArgs e)
{
    Time tm = new Time(Convert.ToInt32(txtHour.Text), Convert.ToInt32(txtMinute.Text), Convert.ToInt32(txtSecond.Text));
    tm.AddSecond();
    txtSecond.Text = tm.Second.ToString();
    txtMinute.Text = tm.Minute.ToString();
    txtHour.Text = tm.Hour.ToString();
}

private void Form1_Load(object sender, EventArgs e)
{
    Time tm = new Time();
    txtHour.Text = Convert.ToString(tm.Hour);
    txtMinute.Text = tm.Minute.ToString();
    txtSecond.Text = tm.Second.ToString();
}

/*单独添加Time类
public class Time
    {
        //1.定义时分秒3个私有字段
        private int hour;
        private int minute;
        private int second;
        //2.读写时分秒属性
        public int Hour
        {
            get { return hour; }
            set { hour = value; }
        }
        public int Minute
        {
            get { return minute; }
            set { minute = value; }
        }
        public int Second
        {
            get { return second; }
            set { second = value; }
        }
        //3.默认构造函数获得系统时间
        public Time()
        {
            hour = DateTime.Now.Hour;
            minute = DateTime.Now.Minute;
            second = DateTime.Now.Second;
        }
        //4.定义带参数的构造函数对时间初始化
        public Time(int myHour, int myMinute, int mySecond)
        {
            this.hour = myHour;
            this.minute = myMinute;
            this.second = mySecond;
        }
        //5.定义秒加1的方法AddSecond()
        public void AddSecond()
        {
            second++;
            if (second >= 60) { second = second % 60; minute++; }
            if (minute >= 60) { minute = minute % 60; hour++; }
        }
    }
*/
```

# 实验四
## 学生成绩平均值
```c#
//事件代码
Student[] stu = new Student[100];
public void  Display(Student stu)
{
    string type = "";
    if (stu  is CollegeStu) 
    { type = "大学生"; }
    else if (stu is MiddleStu) 
    { type = "中学生"; }
    else if (stu is Pupil) 
    { type = "小学生"; }
    lblShow.Text += string.Format("总人数：{0},姓名：{1}，年龄：{2}，{3}，平均成绩为：{4}\n", Student.count , stu.StuNanme ,stu.StuAge , type, stu.GetAverage ());
}
private void btnPupil_Click(object sender, EventArgs e)
{
    Pupil pl = new Pupil(txtName.Text, Convert.ToInt32(txtAge.Text), Convert.ToDouble(txtChinese.Text), Convert.ToDouble(txtMath.Text));
    Display(pl);
    
}

private void btnMiddle_Click(object sender, EventArgs e)
{
    MiddleStu mds = new MiddleStu(txtName.Text, Convert.ToInt32(txtAge.Text), Convert.ToDouble(txtChinese.Text), Convert.ToDouble(txtMath.Text), Convert.ToDouble(txtEnglsh.Text));
    Display(mds);
}

private void btnCollege_Click(object sender, EventArgs e)
{
    CollegeStu cls = new CollegeStu(txtName.Text, Convert.ToInt32(txtAge.Text), Convert.ToDouble(txtChinese.Text), Convert.ToDouble(txtMath.Text));
    Display(cls);
}
/*单独添加Student，Pupil，MiddleStu，CollegeStu类
//定义学生抽象基类
public abstract class Student  
{
    private string stuName;
    private int stuAge;
    public static int count;
    public string StuNanme
    {
        get { return stuName; }
        set { stuName = value; }
    }
    public int StuAge
    {
        get 
        { 
            if (stuAge <= 0) { return 0; }
            else { return stuAge; }
        }
    }
    public Student(string Myname, int Myage)
    {
        this.stuName = Myname;
        this.stuAge = Myage;
        count++;
    }
    public abstract double GetAverage(); //抽象方法
}

//小学生类
public  class Pupil:Student 
{
    private double chinese;
    private double math;
    public double Chinese
    {
        get { return chinese; }
        set { chinese = value; }
    }
    public double Math
    {
        get { return math; }
        set { math = value; }
    }
    public Pupil(string Myname, int Myage, double Mychinese, double Mymath)
        : base(Myname, Myage)
    {
        this.chinese = Mychinese;
        this.math = Mymath;
    }
    public override double GetAverage()//重写学生抽象类中抽象方法
    {
        return (chinese + math) / 2;
    }
}

//中学生类
public  class MiddleStu:Student 
{
    private double chinese;
    private double math;
    private double english;
    public MiddleStu(string myname, int myage, double mychinese, double mymath, double myenglish)
        : base(myname, myage)
    {
        chinese = mychinese;
        math = mymath;
        english = myenglish;
    }
    public override double GetAverage()
    {
        return (chinese + math + english) / 3;
    }
}

//大学生类
class CollegeStu:Student 
{
    private double obligatory;
    private double elective;
    public CollegeStu(string myname, int myage, double myobligatory, double myelective)
        : base(myname, myage)
    {
        obligatory = myobligatory;
        elective = myelective;
    }
    public override double GetAverage()
    {
        return (obligatory +elective ) / 2;
    }
}
```

## 酒店人员管理信息系统
```c#
//单击事件代码
private void btnWaiter_Click(object sender, EventArgs e)
{
    Waiter wt = new Waiter(Convert.ToInt32(txtCount.Text), Convert.ToDouble(txtWage.Text), txtId.Text, txtName.Text, txtIdNumber.Text, txtHealth.Text, txtPhone.Text);
    lblShow.Text += wt.ToSalary() + "\n工资：" + wt.GetSalary() + "\n";
}

private void button1_Click(object sender, EventArgs e)
{
    Cook ck = new Cook(txtLevel.Text, Convert.ToDouble(txtsalary.Text), txtId.Text, txtName.Text, txtIdNumber.Text, txtHealth.Text, txtPhone.Text);
    lblShow.Text += ck.ToSalary() + "\n" + ck.GetSalary();
}
/*单独添加Student，Employee，Waiter，Cook类
//员工信息抽象类
public abstract class Employee //定义员工抽象类
{
    //1.定义员工的信息字段
    private string empId;        //员工编号
    private string empName;      //员工姓名
    private string empIdNumber;  //员工身份证号
    private string empHealth;    //员工健康证号
    private string empPhone;     //员工电话
    //2.属性封装字段
    public string EmpId
    {
        get { return empId; }
        set { empId = value; }
    }
    public string EmpName
    {
        get { return empName; }
        set { empName = value; }
    }
    public string EmpIdNumber
    {
        get { return empIdNumber; }
        set { empIdNumber = value; }
    }
    public string EmpHealth
    {
        get { return empHealth; }
        set { empHealth = value; }
    }
    public string EmpPhone
    {
        get { return empPhone; }
        set { empPhone = value; }
    }
    //3.构造函数对字段进行初始化
    public Employee(string id, string name, string idNumber, string health, string phone)
    {
        this.empId = id;
        this.empName = name;
        this.empIdNumber = idNumber;
        this.empHealth = health;
        this.empPhone = phone;
    }
    //4.计算员工工资的抽象方法
    public abstract double GetSalary();
    //5.获取员工信息的方法
    public string ToSalary()
    {
        return string.Format("员工编号：{0}\n员工姓名：{1}\n员工身份证号：{2}\n员工健康证号：{3}\n电话：{4}",EmpId ,EmpName ,EmpIdNumber ,EmpHealth ,EmpPhone );
    }
}

//服务员类
public  class Waiter:Employee //定义一个服务员类
{
    private int watCount;    //工作小时数
    private double watWage;  //每小时工资标准
    public int WatCount
    {
        get { return watCount; }
        set { watCount = value; }
    }
    public double WatWage
    {
        get { return watWage; }
        set { watWage = value; }
    }
    public Waiter(int count, double wage, string id, string name, string idNumber, string health, string phone)
        : base(id, name, idNumber, health, phone)
    {
        this.watCount = count;
        this.watWage = wage;
    }
            public override double GetSalary()
    {
        return WatCount * WatWage;
    }
}

//厨师类
public  class Cook:Employee 
{
    //1.扩展私有字段
    private string ckLevel;
    private double ckSalary;
    //2.属性保护字段
    public string CkLevel
    {
        get { return ckLevel; }
        set { ckLevel = value; }
    }
    public double CkSalary
    {
        get { return ckSalary; }
        set { ckSalary = value;}
    }
    //3.构造函数初始化字段
    public Cook(string level, double salary, string id, string name, string idNumber, string health, string phone)
        : base(id, name, idNumber, health, phone)
    {
        this.ckLevel = level;
        this.ckSalary = salary;
    }
    //4.重写员工工资的抽象方法（按月计算工资额）
    public override double GetSalary()
    {
        return ckSalary;
    }
}
*/
```

## 添加学生基本信息
```c#
//事件代码
private void btnAdd_Click(object sender, EventArgs e)
{
    Message ms = new Message();
    Student stus = new Student(txtNo.Text, txtName.Text, txtSex.Text, Convert.ToInt32(txtAge.Text), txtSpecialty.Text);
    lblShow.Text +="\n"+ ms.AddStudent(stus)+stus .Display ();
}      

/*单独添加Student类，IMessage接口类，Message接口类
//学生类
public  class Student
{
    //1.声明学生信息的私有字段
    private string stuNo;
    private string stuName;
    private string stuSex;
    private int stuAge;
    private string stuSpec;       
    //2.属性封装字段
    public string StuNo
    {
        get { return stuNo; }
        set { stuNo = value; }
    }
    public string StuName
    {
        get { return stuName; }
        set { stuName = value; }
    }
    public string StuSex
    {
        get { return stuSex; }
        set { stuSex = value; }
    }
    public int StuAge
    {
        get { return stuAge; }
        set { stuAge = value; }
    }
    public string StuSpec
    {
        get { return stuSpec; }
        set { stuSpec = value; }
    }
    
    //3.构造函数初始化字段
    public Student() { }
    public Student(string No, string Name, string Sex, int Age, string Spec)
    {
        this.stuNo = No;
        this.stuName = Name;
        this.stuSex = Sex;
        this.stuAge = Age;
        this.stuSpec = Spec;
    }
    //4.显示学生信息的方法
    public string Display()
    {
        return string.Format("学生信息：\n学号：{0}\n姓名：{1}\n性别：{2}\n年龄：{3}\n专业：{4}",StuNo ,StuName ,StuSex ,StuAge ,StuSpec );
    }
}

//IMessage接口
interface IMessage //定义信息接口
{
    /// <summary>
    /// 1.添加学生信息的方法
    /// </summary>
    /// <param name="stu"></param>
    /// <returns ></returns>
    string AddStudent(Student stu);
}

//实现接口Message类
public  class Message:IMessage //定义实现接口的类
{
    //1.定义存放添加学生的数组
    private Student[] s = new Student[3];
    //2.学生信息数组下标
    private static int count = 0;
    //3.重写接口中添加学生信息的方法
    public string  AddStudent(Student stu)
    {
        string mes = null;
        //4.判断学号是否重复
        foreach (Student st in s )
        {
            if (st != null && st.StuNo == stu.StuNo)
            {
                mes=  string.Format("学生学号重复!");
                
            }
        }
        if (count < s.Length)
        {
            s[count++] = stu;
            
            mes = string.Format("\n添加成功！");
        }
        else
        {
            mes=string.Format("\n学生信息已经录满！");
                
        }
        return mes;
    }
}
```

# 实验五

## 商品信息添加改查排序
```c#
//按钮单击事件
Grade<Student> stus = new Grade<Student>();
private void btnPupli_Click(object sender, EventArgs e)
{
    stus.student.Add(new Pupil(txtstuNo.Text, txtstuName.Text, txtstuSex.Text, Convert.ToInt32(txtstuAge.Text)));
    lblShow.Text += string.Format("\n添加小学生：学号：{0} 姓名：{1} 性别：{2}  年龄：{3}", txtstuNo.Text, txtstuName.Text, txtstuSex.Text, txtstuAge.Text);
}

private void btnMiddle_Click(object sender, EventArgs e)
{
    stus.student.Add(new Middle (txtstuNo.Text, txtstuName.Text, txtstuSex.Text, Convert.ToInt32(txtstuAge.Text)));
    lblShow.Text += string.Format("\n添加中学生：学号：{0} 姓名：{1} 性别：{2}  年龄：{3}", txtstuNo.Text, txtstuName.Text, txtstuSex.Text, txtstuAge.Text);
}

private void btnCollege_Click(object sender, EventArgs e)
{
    stus.student.Add(new College (txtstuNo.Text, txtstuName.Text, txtstuSex.Text, Convert.ToInt32(txtstuAge.Text)));
    lblShow.Text += string.Format("\n添加大学生：学号：{0} 姓名：{1} 性别：{2}  年龄：{3}", txtstuNo.Text, txtstuName.Text, txtstuSex.Text, txtstuAge.Text);
}

private void btnDisplay_Click(object sender, EventArgs e)
{
    lblShow.Text += stus.GetListMessage();
}
/*
//学生抽象类
public abstract  class Student
{
    //1.定义学生信息字段
    private string stuNo;
    private string stuName;
    private string stuSex;
    private int stuAge;
    //2.属性封装字段
    public string StuNo
    {
        get { return stuNo; }
        set { stuNo = value; }
    }
    public string StuName
    {
        get { return stuName; }
        set { stuName = value; }
    }
    public string StuSex
    {
        get { return stuSex; }
        set { stuSex = value; }
    }
    public int StuAge
    {
        get { return stuAge; }
        set { stuAge = value; }
    }
    //3.构造函数初始化字段
    public Student(string No, string Name, string Sex, int Age)
    {
        this.stuNo = No;
        this.stuName = Name;
        this.stuSex = Sex;
        this.stuAge = Age;
    }
    //4.定义抽象方法由继承的类重写
    public abstract string Study();
}

//小学生类
public  class Pupil:Student 
{
    //1.构造函数初始化字段
    public Pupil(string No, string Name, string Sex, int Age)
        : base(No, Name, Sex, Age)
    {

    }
    //2.重写抽象方法，返回小学生的学习信息
    public override string Study()
    {
        return string.Format(" 学号：{0} 姓名：{1} 我是名小学生，现正在学习语文、数学基础课程！", StuNo, StuName);
    }
}

//中学生类
public  class Middle:Student 
{
    //1.构造函数初始化字段
    public Middle(string No, string Name, string Sex, int Age)
        : base(No, Name, Sex, Age)
    {

    }
    //2.重写抽象方法，返回中学生的学习信息
    public override string Study()
    {
        return string.Format(" 学号：{0} 姓名：{1} 我是名中学生，现正在学习语文、数学、英语基础课程！", StuNo, StuName);
    }
}

//大学生类
public class College:Student 
{
    //1.构造函数初始化字段
    public College(string No, string Name, string Sex, int Age)
        : base(No, Name, Sex, Age)
    {

    }
    //2.重写抽象方法，返回大学生的学习信息
    public override string Study()
    {
        return string.Format(" 学号：{0} 姓名：{1} 我是名大学生，现正在学习专业课程！", StuNo, StuName);
    }
}

//泛型班级类(Grade)
public class Grade<T> where T:Student  //定义一个泛型班级类，类型参数约束条件为Student
{
    //1.创建一个班级泛型集合
    public List<T> student = new List<T>();
    //2.定义一个只读属性返回泛型集合student
    public List<T> Students
    {
        get { return student ; }
    }
    //3.遍历泛型集合student中每个成员调用一次的Study方法
    public string GetListMessage()
    {
        string msg = string.Empty;
        foreach (T stu in student)
        {
            msg += "\n" + stu.Study();
        }
        return msg;
    }
}
*/
```

## 泛型集合应用
```c#
//按钮单击事件
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }
    GetMessage message = new GetMessage();
    private void btnProductAdd_Click(object sender, EventArgs e)
    {
        Product prod = new Product(txtProNo.Text, txtProName.Text, Convert.ToDouble(txtProPrice.Text), txtProTime.Text);
        lblShow.Text += "添加商品信息：\n";
        lblShow .Text += message.AddProduct(prod)+"\n";
    }

    private void btnUpdate_Click(object sender, EventArgs e)
    {
        Product prod = new Product(txtProNo.Text, txtProName.Text, Convert.ToDouble(txtProPrice.Text), txtProTime.Text);
        lblShow.Text += "\n修改商品信息成功！\n";
        lblShow.Text += message.UpdateProduct(prod );
    }

    private void btnDelete_Click(object sender, EventArgs e)
    {
        string proNo = txtProNo.Text;
        message.DeleteProduct(proNo);
        lblShow.Text += "\n删除成功！";
    }

    private void btnSearch_Click(object sender, EventArgs e)
    {
        string proNo = txtProNo.Text;
        message.SearchProduct(proNo);
        lblShow.Text +="\n查找的商品信息如下：\n"+ message.SearchProduct(proNo );
    }

    private void btnSort_Click(object sender, EventArgs e)
    {
        lblShow.Text +="\n商品按价格排序信息如下：\n"+ message.ForeachProduct();
    }  
}
/*
//Product类
{
class Product:IComparable<Product >  
{
    //1.定义商品信息字段
    private string proNo;
    private string proName;
    private double  proPrice;
    private string proTime;
    //2.属性封装字段
    public string ProNo
    {
        get { return proNo;  }
        set { proNo = value; }
    }
    public string ProName
    {
        get { return proName; }
        set { proName = value; }
    }
    public double ProPrice
    {
        get { return proPrice; }
        set { proPrice = value; }
    }
    public string ProTime
    {
        get { return proTime; }
        set { proTime = value; }
    }
    //3.构造函数初始化字段
    public Product(string No, string Name, double Price, string Time)
    {
        this.proNo = No;
        this.proName = Name;
        this.proPrice = Price;
        this.proTime = Time;
    }
    //4.返回商品信息方法
    public string GetProdouctMessage()
    {
        return string.Format("商品编号：{0} 商品名称：{1} 商品价格：{2} 入库时间：{3}", proNo, proName, proPrice, proTime);
    }
    //5.添加按商品价格比较的比较器
    public int CompareTo(Product other)
    {
        if (this.proPrice < other.proPrice)
        {
            return -1;
        }
        else
        {
            return 1;
        }
    }    
}
}

//GetMessage类
{
    class GetMessage
    { 
        public List<Product> productList = new List<Product>();
        //1.定义添加商品信息的方法
        public string  AddProduct(Product prodt)
        {
             productList.Add(prodt);
             return prodt.GetProdouctMessage();
        }
        //2.定义查询所有商品信息，按从小到大的顺序输出的方法
        public string ForeachProduct()
        {
            string ms=null;
            productList.Sort();
            foreach (Product pro in productList)
            {
               ms+= string.Format("{0}\n", pro.GetProdouctMessage ());
            }
            return ms;
        }
        //定义根据商品编号修改商品信息的方法，方法参数为商品对象
        public string  UpdateProduct(Product prot)
        {
            foreach (Product pro in productList)
            {
                if (pro.ProNo == prot.ProNo)
                {
                    pro.ProPrice = prot.ProPrice;
                }
            }
            return prot.GetProdouctMessage();

        }
        //定义根据商品编号删除商品的方法
        public void DeleteProduct(string No)
        {
            for (int i = 0; i < productList.Count; i++)
            {
                if (productList[i].ProNo == No)
                {
                    productList.RemoveAt(i);
                }
            }
        }
        //定义根据商品编号查询商品信息的方法
        public string SearchProduct(string No)
        {
            string mes=null;
            foreach (Product pro in productList)
            {
                if (pro.ProNo.Equals(No))
                {
                   mes= string.Format("{0}\n",pro.GetProdouctMessage ());
                }    
            }
            return mes;
        }
    }
}
*/
```

# 实验六

## 用户注册

```C#
private void btnSubmit_Click(object sender, EventArgs e)
{
    {
        if (txtPwd.Text != txtRePwd.Text)
        {
            MessageBox.Show("前后两次输入的密码不一致，请重新输入！");
        }
        string type = string.Empty;
        switch (cmbType.SelectedIndex)
        {
            case 0: type = "管理员"; break;
            case 1: type = "教师"; break;
            case 2: type = "学生"; break;
        }
        string sex = string.Empty;
        if (rdoMale.Checked) { sex = rdoMale.Text; }
        else { sex = rdoFemale.Text; }
        //4.省市选择代码。在窗体加载事件完成省的加载，在cmbProvince控件的改变事件中实现市加载
        string address = string.Empty;
        address = cmbProvince.SelectedItem.ToString() + ":" + cmbCity.SelectedItem.ToString();

        CheckBox[] body = new CheckBox[] { chkMusic, chkSport, chkFilm, chkInternet };
        string mes = string.Empty;
        for (int i = 0; i < body.Length; i++)
        {
            if (body[i].Checked)
            {
                mes += body[i].Text + " ";
            }
        }
        string message = string.Format("用户名：{0}\n用户类型:{1}\n性别：{2}\n地址：{3}\n业余爱好\n:{4}", txtName.Text, type, sex, address, mes);
        DialogResult result = MessageBox.Show(message, "确认信息", MessageBoxButtons.OKCancel, MessageBoxIcon.Information, MessageBoxDefaultButton.Button1);
    }

    private void Form1_Load(object sender, EventArgs e)
    {
        cmbProvince.Items.Add("湖北");
        cmbProvince.Items.Add("湖南");
    }

    private void txtName_TextChanged(object sender, EventArgs e)
    {
        if (txtName.Text == string.Empty)
        {
            MessageBox.Show("用户名不得为空，请输入！");
            txtName.Focus();
        }
    }

    private void cmbProvince_SelectedIndexChanged(object sender, EventArgs e)
    {
        switch (cmbProvince.SelectedIndex)
        {
            case 0:
                cmbCity.Items.Clear();
                cmbCity.Items.Add("武汉");
                cmbCity.Items.Add("宜昌");
                cmbCity.Items.Add("黄石");
                break;
            case 1:
                cmbCity.Items.Clear();
                cmbCity.Items.Add("长沙");
                cmbCity.Items.Add("岳阳");
                cmbCity.Items.Add("浏阳");
                break;
            default:
                cmbCity.Items.Clear();
                break;
        }
    }
}
```

# 实验七

## ADO.NET技术

{% note info modern %}
下载源码后在视图中打开{% kbd 服务器资源管理器 %}，右键{% kbd 数据连接 %} {% kbd 添加新连接 %}在弹窗中点{% kbd 预览 %}双击源码文件后缀名为`.mdf`的文件
{% endnote %}

```SQL
alter database simsdb collate Chinese_PRC_CI_AS
use [SIMSDB]
create table  [dbo].[TUserInfo]
(
	[Id] [INT] PRIMARY KEY IDENTITY(1,1),
	[UserName] [nvarchar](11) NOT NULL,
	[UserPwd] [nvarchar](11) NOT NULL,
	[UserType] [nvarchar](8) NOT NULL,
	[UserSex] [nvarchar](4) NOT NULL,
	[UserBirthday] [nvarchar](11) NOT NULL,
	[UserPhone] [nvarchar](12) NOT NULL,
	[UserAddress] [nvarchar](50) NOT NULL,
)
go
```

```C#
//SQLHelper数据库帮助类：
public class SQLHelper
{
    //数据库连接字段
    static string connStr = "Data Source=(localdb)\\MSSQLLocalDB;Initial Catalog=SIMSDB;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False";
    public int GetAddDeleteModefy(string SQL, params SqlParameter[] ps)
    {
        int n = 0;
        SqlConnection conn = new SqlConnection(connStr); //创建数据库连接对象
        SqlCommand comm = new SqlCommand(SQL, conn);//创建命令对象
        if (ps != null && ps.Length > 0)
        {
            comm.Parameters.AddRange(ps);
        }
        try
        {
            conn.Open();
            n = comm.ExecuteNonQuery();
        }
        catch { }
        finally { conn.Close(); }
        return n;
    }
    public DataTable GetAllDataTable(string sql, params SqlParameter[] ps)
    {
        //定义根据传入的 SQL 语句返回数据表的方法
        DataTable dt = new DataTable();
        //创建数据库连接对象
        SqlConnection conn = new SqlConnection(connStr);
        SqlCommand comm = new SqlCommand(sql, conn);
        if (ps != null && ps.Length > 0)
        {
            comm.Parameters.AddRange(ps);
        }
        try
        {
            conn.Open();
            SqlDataAdapter da = new SqlDataAdapter(comm);
            da.Fill(dt);
        }
        catch { }
        finally { conn.Close(); }
        return dt;
    }
}
```
```C#
//登录界面
private void btnLogin_Click(object sender, EventArgs e)
{
    string type = string.Empty;
    switch (cmbUserType.SelectedIndex)
    {
        case 0: type = "管理员"; break;
        case 1: type = "教师"; break;
        case 2: type = "学生"; break;
    }
    string sql = "select *from TUserInfo where UserName =@name and UserPwd = @pwd and UserType = @type";
    SqlParameter[] ps = new SqlParameter[] { new SqlParameter("@Name", txtName.Text), new SqlParameter("@Pwd", txtPwd.Text), new SqlParameter("@Type", cmbUserType.SelectedItem.ToString()) };
    SQLHelper tUser = new SQLHelper();
    DataTable dt = tUser.GetAllDataTable(sql, ps);
    if (dt.Rows.Count != 0)
    {
        MessageBox.Show("用户登录成功");
        frmAdmin fa = new frmAdmin(txtName.Text);
        fa.Show();
        this.Hide();
    }
    else
    {
        MessageBox.Show("用户登录失败");
    }
    
}

private void button2_Click(object sender, EventArgs e)
{
    Form2 f = new Form2();
    f.Show();
    this.Hide();
}

//用户注册界面：
private void button1_Click(object sender, EventArgs e)
{
    string name = txtName.Text;
    string pwd = txtPwd.Text;
    string type = string.Empty;
    string phone = txtPhone.Text;
    string sex = string.Empty;
    string birthday = string.Empty;
    string address = string.Empty;
    switch (cmbType.SelectedIndex)
    {
        case 0: type = "管理员"; break;
        case 1: type = "教师"; break;
        case 2: type = "学生"; break;
    }
    if (rdbMan.Checked) { sex = rdbMan.Text; }
    else { sex = rdbWoman.Text; }
    birthday = cmbYear.Text;
    address = cmbProvince.Text + cboCity.Text;
    SQLHelper tUser = new SQLHelper();
    string sql = "insert into TUserInfo(UserName ,UserPwd ,UserType,UserSex ,UserBirthday,UserPhone ,UserAddress ) values(@Name, @Pwd, @Type, @Sex, @Birthday, @Phone, @Address)";
    SqlParameter[] ps = new SqlParameter[] { new SqlParameter("@Name", name), new SqlParameter("@Pwd", pwd), new SqlParameter("@Type", type), new SqlParameter("@Sex", sex), new SqlParameter("@Birthday", birthday), new SqlParameter("@Phone", phone), new SqlParameter("@Address", address) };
    if (tUser.GetAddDeleteModefy(sql, ps) != 0)
    {
        MessageBox.Show("用户注册成功！");
    }
    else
    {
        MessageBox.Show("用户注册失败！");
    }
}

private void Form2_Load(object sender, EventArgs e)
{
    cmbProvince.Items.Add("湖北");
    cmbProvince.Items.Add("湖南");
}

private void cmbProvince_SelectedIndexChanged(object sender, EventArgs e)
{
    switch (cmbProvince.SelectedIndex)
    {
        case 0:
            cboCity.Items.Clear();
            cboCity.Items.Add("武汉");
            cboCity.Items.Add("宜昌");
            cboCity.Items.Add("黄石");
            break;
        case 1:
            cboCity.Items.Clear();
            cboCity.Items.Add("长沙");
            cboCity.Items.Add("岳阳");
            cboCity.Items.Add("浏阳");
            break;
        default:
            cboCity.Items.Clear();
            break;
    }
}

private void button2_Click(object sender, EventArgs e)
{
    Form1 f = new Form1();
    f.Show();
    this.Hide();
}

//学生信息管理系统
public frmAdmin(string Name)
{
    InitializeComponent();
    this.lblShow.Text = "欢迎：" + Name + "用户访问本系统";
}
```

# 上机实验

## 试题一

```C#
//设计计算类Caculate：
public class Caculate
{
//定义字段成员
private int num1;private int num2;private int sum;
//属性封装字段
public int Num1		{get { return num1; }set { num1 = value; }}
public int Num2		{get { return num2; }set { num2 = value; }}
public int Sum		{get { return sum; }set { sum = value; }}
//构造函数初始化字段
public Caculate(int num1,int num2)	{this.num1 = num1;this.num2 = num2;}
//计算方法：        
//加
public int Add(int num1, int num2)	{sum = num1 + num2;return sum;}
//减
public int sub(int num1, int num2)	{sum = num1 - num2;return sum;}
//乘
public int mul(int num1, int num2)	{sum = num1 * num2;return sum;}
//除
public int div(int num1, int num2)		{sum = num1 / num2;return sum;}
}
//在窗体界面的[计算结果]按钮的单击事件的代码设计如下：
private void button1_Click(object sender, EventArgs e)
{
int nember1 = Convert.ToInt32(txtNum1.Text);
int nember2 = Convert.ToInt32(txtNum2.Text);
Caculate zhi = new Caculate(nember1, nember2);
if (cmbOp.Text == "+") { lilShow.Text += nember1 + cmbOp.Text + nember2 + "=" + zhi.Add(nember1, nember2) + "\n"; }
else if (cmbOp.Text == "-") { lilShow.Text += nember1 + cmbOp.Text + nember2 + "=" + zhi.sub(nember1, nember2) + "\n"; }
else if (cmbOp.Text == "*") { lilShow.Text += nember1 + cmbOp.Text + nember2 + "=" + zhi.mul(nember1, nember2) + "\n"; }
else if (nember2 == 0) { lilShow.Text += "分母不能为0！\n"; }
else if (cmbOp.Text == "/") { lilShow.Text += nember1 + cmbOp.Text + nember2 + "=" + zhi.div(nember1, nember2) + "\n"; }
}
```

## 试题二
```C#
//泛型基类Person类：
public class Person
{
//定义字段属性：姓名，性别，年龄
private string name;private string sex;private int age;
//属性封装字段
public string Name	{get { return name; }set { name = value; }}
public string Sex		{get { return sex; }set { sex = value; }}
public int Age	{get { return age; }set { age = value; }}
//构造函数初始化字段
public Person(string name, string sex, int age)
{this.name = name;this.sex = sex;this.age = age;}
//定义一个虚方法让Student类来重写
public virtual string GetStudent()
{return string.Format("\n{0}姓名：{1}性别：{2}年龄：{3}", Name, Sex, Age);}
}

//派生类Student继承泛型基类人类：
public class Student:Person
{
//定义字段属性：学号，专业
private string sno;private string major;
//属性封装字段
public string Son		{get { return sno; }set { sno = value; }}
public string Major	{get { return major; }set { major = value; }}
//构造函数初始化字段
public Student(string sno,string name,string sex,int age,string major):base (name,sex,age)
{this.sno = sno;this.major = major;}
//重写GetStudent类
public override  String GetStudent()
{return string.Format("\n学号：{0}姓名：{1}性别：{2}年龄：{3}专业：{4}",Son, Name, Sex, Age,Major);}
}
//在窗体界面的[显示学生信息]按钮的单击事件的代码设计如下：
private void button1_Click(object sender, EventArgs e)
{
List<Person> stus = new List<Person>();stus.Add(new Student(textBox1.Text, textBox2.Text, textBox3.Text, Convert.ToInt32(textBox4.Text), textBox5.Text));
lilShow.Text += string.Format("学号：{0}\n姓名：{1}\n性别：{2}\n年龄：{3}\n专业：{4}", textBox1.Text, textBox2.Text, textBox3.Text, Convert.ToInt32(textBox4.Text), textBox5.Text);
}
```

## 试题三
```SQL
alter database simsdb collate Chinese_PRC_CI_AS
use [数据库名称]
create table  [dbo].[表名称]
(
	[Id] [INT] PRIMARY KEY IDENTITY(1,1),
	[UserName] [nvarchar](12) NOT NULL,
	[UserPwd] [nvarchar](10) NOT NULL,
	[UserSex] [nvarchar](2) NOT NULL,
	[UserAddress] [nvarchar](100) NOT NULL,
	[UserType] [nvarchar](6) NOT NULL,
)go
```

```C#
创建SQLHelper类
public class SQLHelper
{
static string connStr = "填数据库属性连接字段";
public int GetAddDeleteModefy(string SQL, params SqlParameter[] ps)
{
int n = 0;
SqlConnection conn = new SqlConnection(connStr); //创建数据库连接对象
SqlCommand comm = new SqlCommand(SQL, conn);//创建命令对象
if (ps != null && ps.Length > 0)
{comm.Parameters.AddRange(ps);}
try
{conn.Open();n = comm.ExecuteNonQuery();}
catch { }
finally { conn.Close(); }
return n;}
public DataTable GetAllDataTable(string sql, params SqlParameter[] ps)
{
DataTable dt = new DataTable();
SqlConnection conn = new SqlConnection(connStr);
SqlCommand comm = new SqlCommand(sql, conn);
if (ps != null && ps.Length > 0)
{
comm.Parameters.AddRange(ps);
}
try
{conn.Open();SqlDataAdapter da = new SqlDataAdapter(comm);da.Fill(dt);}
catch { }
finally { conn.Close(); }
return dt;
}
}

在用户注册窗体界面的[提交]按钮的单击事件的代码设计如下：
private void Form1_Load(object sender, EventArgs e)
{
cmbProvince.Items.Add("湖北");
cmbProvince.Items.Add("湖南");
}

private void txtName_TextChanged(object sender, EventArgs e)
{
if (txtName.Text == string.Empty)
{
MessageBox.Show("用户名不得为空，请输入！");
txtName.Focus();
}
}

private void cmbProvince_SelectedIndexChanged(object sender, EventArgs e)
{
switch (cmbProvince.SelectedIndex)
{
case 0:
cmbCity.Items.Clear();
cmbCity.Items.Add("武汉");
cmbCity.Items.Add("宜昌");
cmbCity.Items.Add("黄石");
break;
case 1:
cmbCity.Items.Clear();
cmbCity.Items.Add("长沙");
cmbCity.Items.Add("岳阳");
cmbCity.Items.Add("浏阳");
break;default:cmbCity.Items.Clear();break;}}
private void btnSubmit_Click(object sender, EventArgs e)
{
string name = txtName.Text;string pwd = txtPwd.Text;
string type = string.Empty;string sex = string.Empty;string birthday = string.Empty;
string address = string.Empty;switch (cmbType.SelectedIndex)
{case 0: type = "管理员"; break;case 1: type = "教师"; break;case 2: type = "学生"; break;}if (rdoMale.Checked) { sex = rdoMale.Text; }else { sex = rdoFemale.Text; }
address = cmbProvince.SelectedItem.ToString() + "省" + cmbCity.SelectedItem.ToString() + "市";
CheckBox[] body = new CheckBox[] { chkMusic, chkSport, chkFilm, chkInternet };
string mes = string.Empty;
for (int i = 0; i < body.Length; i++)
{if (body[i].Checked)		{mes += body[i].Text + " ";}}
if (txtPwd.Text != txtRePwd.Text){MessageBox.Show("前后两次输入的密码不一致，请重新输入！");}
else{SQLHelper tUser = new SQLHelper();string sql = "insert into tbUserInfo(UserName ,UserPwd,UserSex  ,UserAddress ,UserType ) values(@Name, @Pwd, @Sex,@Address, @Type)";SqlParameter[] ps = new SqlParameter[] { new SqlParameter("@Name", name), new SqlParameter("@Pwd", pwd), new SqlParameter("@Sex", sex),new SqlParameter("@Address", address),new SqlParameter("@Type", type)};
if (tUser.GetAddDeleteModefy(sql, ps) != 0)
{MessageBox.Show("用户注册成功！");Form2 f = new Form2();
f.Show();this.Hide();}
else{MessageBox.Show("用户注册失败！");}}}

private void btnExit_Click(object sender, EventArgs e){
Form2 f = new Form2();f.Show();this.Hide();}}

在用户登录窗体界面的[登录]按钮的单击事件的代码设计如下：
private void btnLogin_Click(object sender, EventArgs e)
{string type = string.Empty;switch (cmbUserType.SelectedIndex){
case 0: type = "管理员"; break;case 1: type = "教师"; break;case 2: type = "学生"; break;}
string sql = "select *from tbUserInfo where UserName =@name and UserPwd = @pwd and UserType = @type";SqlParameter[] ps = new SqlParameter[] { new SqlParameter("@Name", txtName.Text), new SqlParameter("@Pwd", txtPwd.Text), new SqlParameter("@Type", cmbUserType.Text) };SQLHelper tUser = new SQLHelper();DataTable dt = tUser.GetAllDataTable(sql, ps);if (dt.Rows.Count != 0 && textBox1.Text == "9986") 
{MessageBox.Show("用户登录成功！并跳转到系统主界面！");Form2 f = new Form2();
f.Show();this.Hide();}else{MessageBox.Show("用户登录失败");}}
private void button2_Click(object sender, EventArgs e)
{Form1 f = new Form1();f.Show();this.Hide();}}

```