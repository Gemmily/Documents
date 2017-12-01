### Android 坐标系
---
**坐标系**
![Alt text](./xy.png)
#### View获取自身坐标
- getLeft()
- getTop()
- getRight()
- getBottom()
#### View获取自身宽高
- getHeight()
- getWidth()
####MontionEvent坐标
- getX() 触摸点相对当前View左边距离
- getY() 触摸点相对当前View顶部距离
- getRawX() 触摸点相对屏幕左边距离
- getRawY() 触摸点相对于屏幕顶部距离
#### View 滑动
1. **layout()**
在View进行绘制时，会调用`onLayout()`方法来设置显示的位置。
通过修改View的`left`、`top`、`right`、`bottom`四个属性来滑动。

 ```java
 case MotionEvent.ACTION_MOVE:  
    int offsetX = x - mLastX;  
    int offsetY = y - mLastY;  
 layout(getLeft() + offsetX, getTop() + offsetY, getRight() + offsetX, getBottom() + offsetY);
 break;
   ```
   
2. **offsetLeftAndRight()**和**offsetTopAndBottom()**
对layout()方法的封装。
 ```java
 case MotionEvent.ACTION_MOVE:  
    int offsetX = x - mLastX;  
    int offsetY = y - mLastY;  
offsetLeftAndRight(offsetX);
offsetTopAndBottom(offsetY);
 break;
   ```
3. **LayoutParams**
改变margin达到改变位置的目的。
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
4. **scrollTo()**和**scrollBy()**
>移动的是**View的内容**, 在ViewGroup中使用则移动的是ViewGroup下的**所有子View**。— — — —移动的是child

```java
case MotionEvent.ACTION_MOVE:
    int offsetX = x - lastX;
    int offsetY = y - lastY;
    ((View)getParent()).scrollBy(-offsetX,-offsetY);
    break;
```
#### Scroller
1. 创建Scroller 实例
2. 调用`startScroll()`方法来初始化滚动数据并刷新界面。
3. 重写`computeScroll()`方法，实现平滑滚动的逻辑。 
