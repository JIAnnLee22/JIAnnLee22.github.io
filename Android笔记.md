# Android 开发笔记

## 键盘回车完成监听

布局xml代码

```xml
android:imeOptions="actionDone"
android:singleLine="true"
```

java代码监听

```java
editText.setOnEditorActionListner((view, actionId, keyEvent)-> {
    if (actionId == EditorInfo.IME_ACTION_DONE) {
        //todo something
    }
    return false;
});
```

## 软键盘自动顶起布局

```xml
<!-- 放在顶级布局里,如果是fragment放在依赖的activity根布局-->
android:fitSystemWindows="true"
```

```xml
<!-- 放在androidManifest.xml里对应的activity-->
<activity name="xxx" android:windowSoftInputMode="stateHidden|adjustResize">
```

## 输入框光标到最后
```java
editText.setSelection(editText.getText().length())
```


## Handler通信(线程切换的原理)
子线程发送消息到消息队列，主线程对应的`Loop`会死循环的抽取队列里面的消息，通过`Message msg = me.mQueue.next()`拿到任务。通过`Handler`的`msg.taget.dispatchMessage(msg)`分发消息。

## Service组件
启动方式：1.`startService()` 2.`bindService()` 
取消服务：1.`stopService(Intent intent)`传入`startService(Intent intent)`中的`intent`参数 2.在`Service`中调用`stopSelf()`销毁自己


## 自定义view

抗锯齿
```java
canvas.setDrawFilter(new PaintFlagsDrawFilter(0, Paint.ANTI_ALIAS_FLAG | Paint.FILTER_BITMAP_FLAG));
```

文字与旁边的画的圆或圆角矩形中线水平对齐
```java
//获取文字的基线
private float getBaseLine(Paint paint, float centerY) {
return centerY - (paint.getFontMetricsInt().bottom + paint.getFontMetricsInt().top) / 2;
}

//绘制文字的时候             在rectFNew这个矩形右边绘制  中线水平对齐
canvas.drawText("绘制内容", rectFNew.right, getBaseLine(paint, rectFNew.centerY()), paint);
```
