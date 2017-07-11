###Android �����淶�ĵ�
###�ṹ�淶

###����淶
#### Java�����淶
#####1.������
������д+��Ŀ����+ģ�����ƣ�ȫ��������Сд��ĸ��
``` java
me.keeganlee.kandroid.model
```
#####2.��ͽӿ�����
ʹ�ô��շ���������ʻ����ʴ���������ÿ�����ʵ�����ĸ��д��
- activity�࣬������ActivityΪ��׺���磺LoginActivity
- fragment�࣬������FragmentΪ��׺����:ShareDialogFragment
- service�࣬������ServiceΪ��׺���磺DownloadService
- adapter�࣬������AdapterΪ��׺���磺CouponListAdapter
- �����࣬������UtilΪ��׺���磺EncryptUtil
- ģ���࣬������BOΪ��׺���磺CouponBO
- �ӿ�ʵ���࣬������ImplΪ��׺���磺ApiImpl
#####3.��������
ʹ��С�շ�����ö�����������һ�����ʵ�����ĸСд���������ʵ�����ĸ��д��
- ��ʼ��������������init��ͷ������initView
- ���÷�����������set��ͷ������setData
- ���з���ֵ�Ļ�ȡ������������get��ͷ������getData
- ����������أ�ʹ��saveΪǰ׺��ʶ���磺saveData();
- ���������õģ�ʹ��resetǰ׺��ʶ���磺resetData();
- ���������أ�ʹ��clearǰ׺��ʶ���磺clearData();
- �������ݻ�Ч����صģ�ʹ��drawǰ׺��ʶ���磺drawCircle();
- �����͵��жϷ�����������is��has��������߼�����ĵ�����equals������isEmpty()
#####4.��������������
- �ǹ����ҷǾ�̬�ֶε������� m ��ͷ��
- ��̬�ֶε������� s ��ͷ��
- �����ֶ���Сд��ĸ��ͷ��
- ������̬` final `�ֶΣ�������Ϊȫ����д�����»������� (ALL_CAPS_WITH_UNDERSCORES)��
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
#####5.�ؼ�id����
�ؼ���д _ ��Χ _ ���壬��Χ��ѡ��ֻ������ȷ����ķ�Χ�ڲ���Ҫ���ϡ�

�ؼ���д

| �ؼ�       |��д      |�ؼ�        |��д      |
| :-------- | --------:| :-------- |
|TextView	|tv	       |EditText   |et       |
|Button	    |btn	   |ImageButton|imgbtn
|ImageView	|img	   |ListView   |lv
|RadioGroup	|rg        |RadioButton|rbtn
|ProgressBar|pb        |SeekBar    |sb
|CheckBox	|cb	       |Spinner	   |sp
|LinearLayout|ll       |RelativeLayout|rl
|ScrollView	|sv  	   |FrameLayout	|fl	

``` java
<!-- ���Ǳ������ı��� -->
<TextView
    android:id="@+id/txt_header_title"
    ... />

<!-- ���ǵ�¼��ť -->
<Button
    android:id="@+id/btn_login"
    ... />
```
#####6.��Դ�ļ�������
1. layout����
�������_ ��Χ_���ܣ���Χ��ѡ��ֻ������ȷ����ķ�Χ�ڲ���Ҫ���ϡ�
- activity_��Χ_���ܣ�ΪActivity��������ʽ
- fragment_��Χ_���ܣ�ΪFragment��������ʽ
- dialog_��Χ_���ܣ�ΪDialog��������ʽ
- item_list_��Χ_���ܣ�ΪListView��item������ʽ
2.  strings������
����_ ��Χ_���ܣ���Χ��ѡ��
- ҳ����⣬������ʽΪ��title_ҳ��
- ��ť���֣�������ʽΪ��btn_��ť�¼�
- ��ǩ���֣�������ʽΪ��label_��ǩ����
- ѡ����֣�������ʽΪ��tab_ѡ�����
- ��Ϣ�����֣�������ʽΪ��toast_��Ϣ
- �༭�����ʾ���֣�������ʽΪ��hint_��ʾ��Ϣ
- ͼƬ���������֣�������ʽΪ��desc_ͼƬ����
- �Ի�������֣�������ʽΪ��dialog_����
- menu��item���֣�������ʽΪ��action_����
3.  colors������
ǰ׺_ �ؼ� _ ��Χ _ ��׺���ؼ�����Χ����׺��ѡ�����ؼ��ͷ�Χ����Ҫ��һ����
- ������ɫ�����bgǰ׺
- �ı���ɫ�����textǰ׺
- �ָ�����ɫ�����divǰ׺
- Ĭ��״̬����ɫ�����normal��׺
- ����ʱ����ɫ�����pressed��׺
- ѡ��ʱ����ɫ�����selected��׺
- ������ʱ����ɫ�����disable��׺
4. drawable������
ǰ׺_ �ؼ�_ ��Χ_��׺���ؼ�����Χ����׺��ѡ�����ؼ��ͷ�Χ����Ҫ��һ����
- ͼ���࣬���icǰ׺
- �����࣬���bgǰ׺
- �ָ��࣬���divǰ׺
- Ĭ���࣬���defǰ׺
- Ĭ��״̬�����normal��׺
- ����ʱ��״̬�����pressed��׺
- ѡ��ʱ��״̬�����selected��׺
- ������ʱ��״̬�����disable��׺
- ����״̬�����selector��׺��һ��ΪListView��selector��ť��selector��
#### Javaע��
#####1. �ļ�ͷע��
�ļ�����ͳһ��Ӱ�Ȩ����������� package �� import ��䣨������֮���ÿ��зָ�������������ӿ��������� Javadoc ��ע��˵�����ӿڵ����á�
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
#####2. ��ͽӿ�ע��
��д��ÿ�������Ҫ�Ĺ���������������� Javadoc ��ע��������һ�仰˵����򷽷�����;����ʽӦ�Ե����˳������Զ��ʿ�ͷ��
``` java
/** Returns the correctly rounded positive square root of a double value. */
static double sqrt(double a) {
    ...
}

��
/**
 * Constructs a new String by converting the specified array of
 * bytes using the platform's default character encoding.
 */
public String(byte[] bytes) {
    ...
}
```
#####4. ����ע��
���漸�ַ��������������javadocע�ͣ�˵���÷�������;�Ͳ���˵�����Լ�����ֵ��˵����
- �ӿ��ж�������з���
- ���������Զ���ĳ��󷽷�
- ��������Զ��幫�÷���
- ������Ĺ��÷���
 
#####3.ʹ�� TODO ��ע
Ϊ����ʹ�� TODO ��ע�Ƕ��ڵ���ʱ�������������˵�㹻�õ�����������
``` java
 // TODO: Remove this code after the UrlTable2 has been checked in.
```
#### Java ��ʽ����

#####1. һ��������಻Ҫ����40�д��롣
#####2.ʹ��4���ո��������飬����Ҫʹ���Ʊ����
#####3. ��һ�����ʽ�޷�������һ����ʱ���ɻ�����ʾ�������������8���ո�������

``` java
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
``` 
#####4. �п�����Ϊ100�����ø�ʽ��ʱ�Զ����е��п�λ�á�
#####5. �����Ų�Ҫ����һ�У�����ǰ��Ĵ���ͬһ�С����ң���������ǰ��Ĵ���֮����һ���ո������
``` java
public void method() { // ��ȷд��

} 

public void method()
{ // ����д��
}  

public void method(){ // ����д��

} 
``` 
#####6. ���е�ʹ��

���߼���صĴ�����ÿ��и���������߿ɶ��ԡ�����Ҳֻ��һ�У���Ҫ�ն��С��������������һ�����У�
- ��������֮��
- �����ڵ������߼���֮��
- �����ڵľֲ������ͷ����ĵ�һ���߼����֮��
- �����ͱ���֮��
��������С�ֲ���������������������������ߴ���Ŀɶ��ԺͿ�ά���ԣ������ͳ���Ŀ����ԡ�ÿ������Ӧ���ڰ�����������ʹ�ó��ϵ����ڲ�Ŀ��н���������
#####7. һ������һ����������Ҫһ�������������������������дע�͡�
``` java
private String param1; // ����1
private String param2; // ����2
```
#####8. ��ɫֵͳһ��colors.xml�ж��壬Ȼ���ڴ���Ͳ����ļ������á����⣬��Ҫ�ڴ���Ͳ����ļ�������ϵͳ����ɫ������͸����

#####9. ���ִ�С�ĵ�λͳһ��sp��Ԫ�ش�С�ĵ�λͳһ��dp��

#####10. Ӧ���е��ַ���ͳһ��strings.xml�ж��壬Ȼ���ڴ���Ͳ����ļ������á�

