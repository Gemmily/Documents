## Android 开发规范
### 1.目录结构
一个完整的项目，应保持下列结构：
- app/manifests AndroidManifest.xml配置文件目录
- app/java 源码目录
- app/res 资源文件目录
- libs/第三方架包管理目录。
- bin/输出文件夹，如apk文件 。
- Gradle Scripts gradle编译相关的脚本

### 2.代码规范  

####  2.1 Java 命名规范  

2.1.1 包命名  

域名反写+项目名称+模块名称，全部单词用小写字母。
- 一级包名为com
- 二级包名为xx（可以是公司或则个人的随便）
- 三级包名应用的英文名app_name
- 四级包名为模块名或层级名

常见的命名划分

| 命名格式          |作用                   |
| :------------    | :------------------- | 
|com.xx.app_name.activities(或com.xx.app_name.activity)	|存放app所有的Activity|
|com.xx.app_name.service	|存放app所有的Service|
|com.xx.app_name.receiver	|存放app所有的|BroadcastReceiver
|com.xx.app_name.provider	|存放app所有的ContentProvider|
|com.xx.app_name.fragment	|存放app所有的Fragment|
|com.xx.app_name.dialog	    |存放app所有的Dialog|
|com.xx.app_name.base	    |存放app一些共有的基础模块，诸如BaseActivity、BaseContentProvider、BaseService，BaseFragment等|
|com.xx.app_name.utils	    |存放app的工具类,诸如格式化日期的DateFormatUtils，处理字符串的StringUtils等|
|com.xx.app_name.bean(或com.xx.app_name.unity)	              |存放app自定义的实体类|
|com.xx.app_name.db	 |存放app数据库操作相关的类|
|com.xx.app_name.view |存放app自定义的控件|
|com.xx.app_name.adapter|	存放app所有的适配器类|

2.1.2 类和接口命名  

使用大驼峰规则，用名词或名词词组命名，每个单词的首字母大写。

|类     | 命名格式      |示例              |
|:------|:-------------|:----------------| 
|activity类| 以Activity为后缀|LoginActivity|
|fragment类|以Fragment为后缀|ShareDialogFragment|
|service类 |以Service为后缀|DownloadService|
|adapter类 |以Adapter为后缀|CouponListAdapter|
|基础功能类 |Base+XX父类名  |BaseActivity，BaseFragment
|工具类     |以Util为后缀|EncryptUtil|
|模型类     |以bean为后缀|UserBean|
|接口实现类 |以Impl为后缀|ApiImpl|

2.1.3 方法命名  

使用小驼峰规则，用动词命名，第一个单词的首字母小写，其他单词的首字母大写。
- 初始化方法，命名以init开头，例：initView
- 设置方法，命名以set开头，例：setData
- 具有返回值的获取方法，命名以get开头，例：getData
- 保存数据相关，使用save为前缀标识，如：saveData();
- 对数据重置的，使用reset前缀标识，如：resetData();
- 清除数据相关，使用clear前缀标识，如：clearData();
- 绘制数据或效果相关的，使用draw前缀标识，如：drawCircle();
- 布尔型的判断方法，命名以is或has，或具有逻辑意义的单词如equals，例：isEmpty()

2.1.4 变量及常量命名  

- 非公开且非静态字段的名称以 m 开头。
- 静态字段的名称以 s 开头。
- 其他字段以小写字母开头。
- 公开静态` final `字段（常量）为全部大写并用下划线连接 (ALL_CAPS_WITH_UNDERSCORES)。

>注意，所有常量都必须是static final成员，但并不是所有的static final成员都是常量。

``` java
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

2.1.5 控件id命名  

布局文件中的控件命名尽量使用控件缩写做前缀。控件缩写 _ 范围 _ 意义，范围可选，

| 控件       |缩写      |控件        |缩写      |
| :-------- | :--------| :-------- |:--------|
|TextView	|tv	       |EditText   |et       |
|Button	    |btn	   |ImageButton|imgbtn   |
|ImageView	|img	   |ListView   |lv       |
|RadioGroup	|rg        |RadioButton|rbtn     |
|ProgressBar|pb        |SeekBar    |sb       |
|CheckBox	|cb	       |Spinner	   |sp       |
|LinearLayout|ll       |RelativeLayout|rl    |
|ScrollView	|sv  	   |FrameLayout	|fl	     |

``` java
<!-- 这是标题栏的标题 -->
<TextView
    android:id="@+id/txt_header_title"
    ... />

<!-- 这是登录按钮 -->
<Button
    android:id="@+id/btn_login"
    ... />
```

2.1.6 资源文件命名字  

1.layout命名  
组件类型_ 范围_功能，范围可选，只在有明确定义的范围内才需要加上。

- activity_范围_功能，为Activity的命名格式
- fragment_范围_功能，为Fragment的命名格式
- dialog_范围_功能，为Dialog的命名格式
- item_list_范围_功能，为ListView的item命名格式

2.strings的命名  
类型_ 范围_功能，范围可选。

- 页面标题，命名格式为：title_页面
- 按钮文字，命名格式为：btn_按钮事件
- 标签文字，命名格式为：label_标签文字
- 选项卡文字，命名格式为：tab_选项卡文字
- 消息框文字，命名格式为：toast_消息
- 编辑框的提示文字，命名格式为：hint_提示信息
- 图片的描述文字，命名格式为：desc_图片文字
- 对话框的文字，命名格式为：dialog_文字
- menu的item文字，命名格式为：action_文字

3.colors的命名  
前缀_ 控件 _ 范围 _ 后缀，控件、范围、后缀可选，但控件和范围至少要有一个。

- 背景颜色，添加bg前缀
- 文本颜色，添加text前缀
- 分割线颜色，添加div前缀
- 默认状态的颜色，添加normal后缀
- 按下时的颜色，添加pressed后缀
- 选中时的颜色，添加selected后缀
- 不可用时的颜色，添加disable后缀

4.drawable的命名  
前缀_ 控件_ 范围_后缀，控件、范围、后缀可选，但控件和范围至少要有一个。

- 图标类，添加ic前缀
- 背景类，添加bg前缀
- 分隔类，添加div前缀
- 默认类，添加def前缀
- 默认状态，添加normal后缀
- 按下时的状态，添加pressed后缀
- 选中时的状态，添加selected后缀
- 不可用时的状态，添加disable后缀
- 多种状态，添加selector后缀（一般为ListView的selector或按钮的selector）

####  2.2 Java 注释

2.2.1 文件头注释  

文件顶部统一添加版权声明，其后是 package 和 import 语句（各个块之间用空行分隔），最后是类或接口声明。在 Javadoc 备注中说明类或接口的作用。

``` java
/*
 * Copyright (C) 2015 The Android Open Source Project
 */

package com.android.internal.foo;

import android.os.Blah;
import android.view.Yada;

import java.sql.ResultSet;
import java.sql.SQLException;

/**
 * Does X and Y and provides an abstraction for Z.
 */

public class Foo {
    ...
}
```

2.2.2 类和接口注释  

编写的每个类和重要的公开方法都必须包含 Javadoc 备注，至少用一句话说明类或方法的用途。句式应以第三人称描述性动词开头。

``` java
/** Returns the correctly rounded positive square root of a double value. */
static double sqrt(double a) {
    ...
}

// or

/**
 * Constructs a new String by converting the specified array of
 * bytes using the platform's default character encoding.
 */
public String(byte[] bytes) {
    ...
}
```

2.2.3 方法注释  

下面几种方法，都必须添加javadoc注释，说明该方法的用途和参数说明，以及返回值的说明。
- 接口中定义的所有方法
- 抽象类中自定义的抽象方法
- 抽象父类的自定义公用方法
- 工具类的公用方法
 
2.2.4 使用 TODO 备注  

为代码使用 TODO 备注是短期的临时解决方案，或者说足够好但并不完美。

``` java
 // TODO: Remove this code after the UrlTable2 has been checked in.
```

#### 2.3 Java 语言规范

2.3.1 不要忽略异常  

要避免出现捕获异常，但不处理的情况

``` java
public void setUserId(String id) {
    try {
        mUserId = Integer.parseInt(id);
    } catch (NumberFormatException e) { }
}
```

有必要还需给用户提示。

``` java
public void setCount(String count) {
    try {
        count = Integer.parseInt(id);
    } catch (NumberFormatException e) {
        count = 0;
        Log.e(TAG, "There was an error parsing the count " + e);
        DialogFactory.showErrorMessage(R.string.error_message_parsing_count);
    }
}
```

一些适当的处理：
- 通知用户，显示错误提示。
- 设置错误后变量默认值。
- 抛出对应的异常。
- 将错误打印到控制台。

2.3.2 不要轻易使用 Exception 捕获异常  

使用 ` Exception ` 捕获异常， 会使包括如`RuntimeExceptions`  中的 ` ClassCastException ` 异常，会被夹在应用程序级别的错误进行处理，从而掩盖了我们处理异常代码的效率。

因此当捕获我们可预知的异常时，应该采取相应的措施：

``` java
public void openCustomTab(Context context, Uri uri) {
    Intent intent = buildIntent(context, uri);
    try {
        context.startActivity(intent);
    } catch (ActivityNotFoundException e) {
        Log.e(TAG, "There was an error opening the custom tab " + e);
    }
}
```

2.3.3 多组异常  

一段代码中，可能会出现多种异常。为了可读性和避免重复代码进行分组。例如，

``` java
public void openCustomTab(Context context, @Nullable Uri uri) {
    Intent intent = buildIntent(context, uri);
    try {
        context.startActivity(intent);
    } catch (ActivityNotFoundException e) {
        Log.e(TAG, "There was an error opening the custom tab " + e);
    } catch (NullPointerException e) {
        Log.e(TAG, "There was an error opening the custom tab " + e);
    } catch (SomeOtherException e) {
        // Show some dialog
    }
}

// or
public void openCustomTab(Context context, @Nullable Uri uri) {
    Intent intent = buildIntent(context, uri);
    try {
        context.startActivity(intent);
    } catch (ActivityNotFoundException e | NullPointerException e) {
        Log.e(TAG, "There was an error opening the custom tab " + e);
    } catch (SomeOtherException e) {
        // Show some dialog
    }
}
```

2.3.4 全包声明

当我们声明引用时，应用使用全包声明。

``` java
错误的用法:
import android.support.v7.widget.*;

正确的用法:
import android.support.v7.widget.RecyclerView;
```

2.3.5 不要保留未使用的引用

#### 2.4 Java style规范  

2.4.1 一个方法最多不要超过40行代码。  

2.4.2 使用4个空格来缩进块，而不要使用制表符。  

2.4.3 当一个表达式无法容纳在一行内时，可换行显示，另起的新行用8个空格缩进。

``` java
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
``` 

##### 2.4.4 行宽设置为100，设置格式化时自动断行到行宽位置。
##### 2.4.5 花括号不要单独一行，和它前面的代码同一行。而且，花括号与前面的代码之间用一个空格隔开。

``` java
public void method() { // 正确写法

} 

public void method()
{ // 错误写法
}  

public void method(){ // 错误写法

} 
``` 

2.4.6 空行的使用  

将逻辑相关的代码段用空行隔开，以提高可读性。空行也只空一行，不要空多行。在以下情况需用一个空行：
- 两个方法之间
- 方法内的两个逻辑段之间
- 方法内的局部变量和方法的第一条逻辑语句之间
- 常量和变量之间
尽可能缩小局部变量的作用域。这样做有助于提高代码的可读性和可维护性，并降低出错的可能性。每个变量应该在包含变量所有使用场合的最内层的块中进行声明。

2.4.7 一行声明一个变量，不要一行声明多个变量，这样有利于写注释。  

``` java
private String param1; // 参数1
private String param2; // 参数2
```

2.4.8 颜色值统一在colors.xml中定义，然后在代码和布局文件中引用。另外，不要在代码和布局文件中引用系统的颜色，除了透明。  

2.4.9 文字大小的单位统一用sp，元素大小的单位统一用dp。  

2.4.10 应用中的字符串统一在strings.xml中定义，然后在代码和布局文件中引用。  

2.4.11 switch语句中，必须包含default语句。  

2.4.12 变量字段排序

1. 枚举
2. 常量
3. Dagger 注入
4. Butterknife 绑定
5. 私有全局变量
6. 公共全局变量

2.4.13 import语句顺序

1.   Android imports
2.   第三方库（com、junit、net、org）
3.   java和javax

符合 IDE 设置，导入顺序应为：
- 每个分组内按字母顺序排序，其中大写字母开头的语句位于小写字母开头的语句前面（例如 Z 在 a 前面）。
- 每个主要分组（android、com、junit、net、org、java、javax）之间用空行隔开。

针对 Android 简单归结为“选择一种兼容一致的排序方式”。因此我们选择了一种样式，更新了样式指南，并让 IDE 遵循该指南。系统对所有软件包的导入都符合此模式，无需再进行额外的工程处理。

这种样式是按以下原则选取的：

- 用户希望先看到的导入往往位于顶部 (android)。
- 用户最不希望看到的导入往往位于底部 (java)。
- 用户可以轻松遵循的样式。
- IDE 可以遵循的样式。  
  
    
      
     ------------------------------------------------------
     
### 参考资料：

1. [Google代码样式指南](https://source.android.com/source/code-style) 
2. [Android技术积累:开发规范](http://keeganlee.me/post/android/20150709)
3. [Android 项目规范](http://www.jianshu.com/p/7f7122cd28d1)
4. [Android程序架构目录结构介绍](http://blog.csdn.net/renzhe333/article/details/13004689)
