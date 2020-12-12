# 阅后价值

```java
public static AccessibilityServiceMonitor getInstance() {
        //什么时候需要双重检测
        if (mAccessibilityServiceMonitor == null) {
            //抛出异常的方式
            throw new NullPointerException("AblService辅助服务未开启");
        }
        return mAccessibilityServiceMonitor;
    }
	
```

```java
 //为什么还要赋值一遍？
    @Override
    public void onCreate() {
        mAccessibilityServiceMonitor = this;
    }
     @Override
    public void onServiceConnected() {
        super.onServiceConnected();
        //setServiceInfo();这个方法同样可以实现xml中的配置信息
        //可以做一些开启后的操作比如点两下返回
        //再次赋值有必要吗？
        mAccessibilityServiceMonitor = this;
    }	
```

```Java
    @Override
    public boolean onUnbind(Intent intent) {
        Log.d(TAG, "onUnbind: ");
        //关闭服务时,调用
        //如果有资源记得释放
        return super.onUnbind(intent);
    }
```

**但是都很少看到对node对回收操作**



bean类实在太麻烦，尽快转向getter、setter

