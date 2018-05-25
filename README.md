# AndroidTabLayout
Android 标签布局。

### 本应用的示例

![image](https://github.com/iWay7/AndroidTabLayout/blob/master/sample.gif)   

### 本示例基于 AndroidHelpers 库，访问 https://github.com/iWay7/AndroidHelpers 添加依赖。

#### 开始使用：
##### 准备一个可以随 selected 状态变化的 selector 颜色文件
```
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:color="@color/red" android:state_selected="true" />
    <item android:color="@color/blue" />
</selector>
```

##### 在布局文件中声明一个 TabLayout 视图，并依照 LinearLayout 添加子视图代表 Tab 标签：
```
<site.iway.androidhelpers.TabLayout
    android:id="@+id/tabLayout"
    android:layout_width="match_parent"
    android:layout_height="48dp"
    android:background="#eeeeee"
    app:containSplitter="false"
    app:invokeSelectOnTouchDown="true"
    app:invokeSelectOnTouchMove="true"
    app:invokeSelectOnTouchUp="true"
    app:invokeSelectOnTouchUpRange="5dp">
    <TextView
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:gravity="center"
        android:text="Page 1"
        android:textColor="@color/tab_text_color" />
    <TextView
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:gravity="center"
        android:text="Page 2"
        android:textColor="@color/tab_text_color" />
    <TextView
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:gravity="center"
        android:text="Page 3"
        android:textColor="@color/tab_text_color" />
</site.iway.androidhelpers.TabLayout>
```

##### 其中的属性解释如下：
```
app:containSplitter 指示子视图是否含有分割线视图
app:invokeSelectOnTouchDown 在触摸按下的时候响应
app:invokeSelectOnTouchMove 在触摸滑动的时候响应
app:invokeSelectOnTouchUp 在触摸抬起的时候响应
app:invokeSelectOnTouchUpRange 在触摸抬起的时候响应相对于按下位置的距离
```

##### 可以用下方式绑定到 ViewPager 中：
```
viewPager.setOnPageChangeListener(new OnPageChangeListener() {
    @Override
    public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {
    }
    @Override
    public void onPageSelected(int position) {
        tabLayout.setSelectedItem(position);
    }
    @Override
    public void onPageScrollStateChanged(int state) {
    }
});

tabLayout.setOnItemSelectedListener(new OnItemSelectedListener() {
    @Override
    public boolean onItemSelected(TabLayout tabLayout, int item) {
        viewPager.setCurrentItem(item);
        return true;
    }
});
```

##### OnItemSelectedListener 中 onItemSelected 的返回值代表是否执行选中操作。

##### 用代码的方式改变选中项，默认没有任何选中项，通过此方法在视图构建完成后选中默认项：
```
tabLayout.setSelectedItem(0, false); // 第一个参数代表项位置，第二个参数表示是否触发回调方法
```