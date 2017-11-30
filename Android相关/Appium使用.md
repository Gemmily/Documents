#### Appium
---
#### 1. Appium ����
Appium ��һ���Զ������Կ�Դ���ߣ�֧�� iOS ƽ̨�� Android ƽ̨�ϵ�ԭ��Ӧ�ã�web Ӧ�úͻ��Ӧ�á�
֧��ƽ̨��iOS��Android��Windows��FirefoxOS
�������[�ٷ��ĵ�][9]

#### 2. Appium ������
Ϊ�������ƶ��Զ�������Appium ��ѭ��һ����ѧ����Ҫ������4����
1. ������Ϊ���Զ����������±�������޸����Ӧ�á�
2. �㲻�ؾ�����ĳ�����Ի��߿����д�����в��Խű���
3. һ���ƶ��Զ����Ŀ�ܲ�Ӧ���ڽӿ����ظ������ӡ����ƶ��Զ����Ľӿ�Ӧ��ͳһ��
4. �����Ǿ����ϣ����������ϣ������뿪Դ��

#### 3. Appium��Ͱ�װ��Android��
1. [��װJDK�����û�������](#1)
2. [��װAndroid SDK�����û�������](#2)
3. [��װNodejs](#3)
4. [��װappium](#4)
5. [��֤��װ](#5)

<h5 id="1">��װJDK�����û�������(��windowsΪ��)</h5>

1. ��Java����������Ӧ��JDK����װ
2. ���û�������

     i.  ���JAVA_HOME��Ӧ��·�� 
     `C:\Program Files\Java\jdk1.7.0_79`
    ii.  ��PATH����ĩβ׷�� 
    `;%JAVA_HOME%/bin;`
   iii. ���CLASSPATH������ֵΪ
   `%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar`
3. ��command line ����`java -version`
��ʾ��������˵��������ȷ

```
java version "1.7.0_79"<br>
Java(TM) SE Runtime Environment (build 1.7.0_79-b15)<br>
Java HotSpot(TM) 64-Bit Server VM (build 24.79-b02, mixed mode)
```

<h5 id="2">��װAndroid SDK�����û�������</h5>

>ע�⣺��װAndroid SDK��Ҫ��ǽ���������SDK repository

1. ��[Android ����][1]���ز���װSDK
2. ���û�������

     i.  ���ANDROID_HOME����ֵΪ��
     `C:\(��İ�װ·��)\Android\sdk`
    ii. ��path��������ֵĩβ׷�ӣ�
    `;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools;`
3. ������Ϻ�������������`adb devices`
������£�˵�����óɹ���

```
* daemon not running. starting it now on port 5037 *
* daemon started successfully *
```


<h5 id="3">��װNodejs</h5>

1. ��[Nodejs����][2]�������°汾��NodeJs��ֱ�Ӱ�װ��
2. ��װ��Ϻ󣬴������У�����`node -v`
���������������Ϣ˵����װ�ɹ�

```
 v4.0.0
```

<h5 id="4">��װappium</h5>

��װappium�����ַ�ʽ��
>npm ��װ�� windows ��ԱȽϸ��ӣ�����ʹ�ùٷ���װ����

1. ʹ�� **npm**��װ**Appium**
  ```
npm install -g appium 
```
2. ʹ��**Appium**�ٷ���װ����װ
��[Appium����][3]���غ�����ʹ��ϵͳһ�µİ汾���а�װ

<h5 id="5">��֤��װ</h5>

��ȷ��Appium��װ��Ϻ����ǿ���ͨ��`appium-doctor`����������鵱ǰappium��װ�Ƿ����ƣ���ǰ��JDK��SDK�Ȼ����Ƿ�������ȷ��
���`appium-doctor`���ص��������д�ģ�����ݷ��صľ������ʾ������Ļ�������ơ�
������صĽ���������£�˵����װ�ɹ�

```  
Android Checks were successful.
All Checks were successful
```
>��Ҫע����ǣ��������ͨ����װ����װ�ģ�ʹ��appium-doctor ����ʱ�����л��� C:\Program Files (x86)\Appium\node_modules\.bin Ŀ¼

#### 4.���� Appium Server
1. ������������

    ```
$ appium
info: Welcome to Appium v1.4.16 (REV ae6877eff263066b26328d457bd285c0cc62430d)
info: Appium REST http interface listener started on 0.0.0.0:4723
info: Console LogLevel: debug

```

2. ͨ��ͼ�λ����氲װ�� appium
![Alt text](./img/appium_launch_windows.png)

#### 5.appium������
1. Android Setting 
������������ҪΪ�˲����ڽű��������capabilities���Ժ�inspector���ʹ�á� 
![Alt text](./img/config.png)

2. General Setting
����������Ǳ������˿���4723������appium�Ķ˿ڣ�����ģ�����Ķ˿ڡ� 
![Alt text](./img/General.png)

3. inspector 
�Ŵ󾵹��ߣ���ȡapp����ؼ����ԵĹ��ߡ�
![Alt text](./img/inspector.png)

4. ��־���
�м��ɫ����������ʾ��־��
     i. info��Appium�ĵ�����Ϣ 
     ii. error��������Ϣ
     
#### 6.��д���Խű���[�ٷ�demo][8]��
1. AndroidStudio���½�android���̡�
2. ����java module����appium����java�������������Զ���case��
3. ����[ Appium java client ][4]��[Selenium Java standalone server][5]�������Ӧ��jar��
4. ���jar��
5. �����ļ�������apps����Ӵ����Ե�APK ([�ٷ�����APK][6])
6. �������ʼ������(����ʹ��[�ٷ�����Դ��][7])
![Alt text](./img/init.png)

    >ע�⣺�����ϵͳ����·��Ҫ�ĳ��Լ���
   ![Alt text](./img/modify.png)
#### 7. ����
     i.����appium
    ii.�ڵ�ǰ�ű��༭���Ҽ�ѡ��`Run AndroidContactsTest`�� 

[1]:https://developer.android.com/studio/index.html#Other
[2]:https://nodejs.org/en/
[3]:https://bitbucket.org/appium/appium.app/downloads/
[4]:https://search.maven.org/#search%7Cga%7C1%7Cg%3Aio.appium%20a%3Ajava-client
[5]:http://www.seleniumhq.org/download/
[6]:https://github.com/appium/sample-code/blob/master/sample-code/apps/ContactManager/ContactManager.apk 
[7]:https://github.com/appium/sample-code/blob/master/sample-code/examples/java/junit/src/test/java/com/saucelabs/appium/AndroidContactsTest.java 
[8]:https://github.com/appium/sample-code/tree/master/sample-code/examples
[9]:http://appium.io/documentation.html?lang=zh






