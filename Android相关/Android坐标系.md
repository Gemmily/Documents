### Android ����ϵ
---
**����ϵ**
![Alt text](./xy.png)
#### View��ȡ��������
- getLeft()
- getTop()
- getRight()
- getBottom()
#### View��ȡ������
- getHeight()
- getWidth()
####MontionEvent����
- getX() ��������Ե�ǰView��߾���
- getY() ��������Ե�ǰView��������
- getRawX() �����������Ļ��߾���
- getRawY() �������������Ļ��������
#### View ����
1. **layout()**
��View���л���ʱ�������`onLayout()`������������ʾ��λ�á�
ͨ���޸�View��`left`��`top`��`right`��`bottom`�ĸ�������������

 ```java
 case MotionEvent.ACTION_MOVE:  
    int offsetX = x - mLastX;  
    int offsetY = y - mLastY;  
 layout(getLeft() + offsetX, getTop() + offsetY, getRight() + offsetX, getBottom() + offsetY);
 break;
   ```
   
2. **offsetLeftAndRight()**��**offsetTopAndBottom()**
��layout()�����ķ�װ��
 ```java
 case MotionEvent.ACTION_MOVE:  
    int offsetX = x - mLastX;  
    int offsetY = y - mLastY;  
offsetLeftAndRight(offsetX);
offsetTopAndBottom(offsetY);
 break;
   ```
3. **LayoutParams**
�ı�margin�ﵽ�ı�λ�õ�Ŀ�ġ�
 ```java
 case MotionEvent.ACTION_MOVE:  
    int offsetX = x - mLastX;  
    int offsetY = y - mLastY;  
//     LinearLayout.LayoutParams lp = (LinearLayout.LayoutParams) getLayoutParams();  
    ViewGroup.MarginLayoutParams lp = (ViewGroup.MarginLayoutParams) getLayoutParams();  
    lp.leftMargin = getLeft() + offsetX;  
    lp.topMargin = getTop() + offsetY;  
    setLayoutParams(lp);  
    break;
   ```
4. **scrollTo()**��**scrollBy()**
>�ƶ�����**View������**, ��ViewGroup��ʹ�����ƶ�����ViewGroup�µ�**������View**���� �� �� ���ƶ�����child

```java
case MotionEvent.ACTION_MOVE:
    int offsetX = x - lastX;
    int offsetY = y - lastY;
    ((View)getParent()).scrollBy(-offsetX,-offsetY);
    break;
```
#### Scroller
1. ����Scroller ʵ��
2. ����`startScroll()`��������ʼ���������ݲ�ˢ�½��档
3. ��д`computeScroll()`������ʵ��ƽ���������߼��� 
