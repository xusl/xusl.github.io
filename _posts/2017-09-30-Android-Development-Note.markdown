---
layout: post
title: Android Development Note
date: 2017-09-30 15:32:24.000000000 +09:00
tag: Android
---

bindService 异常
--------------------------------------

在AndroidManifest.xml声明服务
```html
<service  
    android:name=".BindService"  
    android:enabled="true"  
    android:exported="true" >  
        <intent-filter>  
            <action android:name="com.zen.action.BOOKMANAGER_SERVICE"/>  
        </intent-filter>  
</service>  
```

#### Problem

绑定服务时抛出异常 *'IllegalArgumentException: Service Intent must be explicit'*
```java
final Intent intent = new Intent();  
intent.setAction("com.zen.action.BOOKMANAGER_SERVICE");  
bindService(intent,conn,Service.BIND_AUTO_CREATE);  
```


#### Solution
创建Intent时，调用setPackage方法，Intent对象就是显性的
```java
final Intent intent = new Intent();  
intent.setAction("com.zen.action.BOOKMANAGER_SERVICE");  
intent.setPackage(this.getPackageName());  
bindService(intent,conn,Service.BIND_AUTO_CREATE);  
```

---
Android Webview gives net::ERR_CACHE_MISS message
---
Missing permission, 
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

net::ERR_PROXY_CONNECTION_FAILED
解决方法：取消WiFi的代理。
打开手机的设置—>在连接的WiFi将代理设置成无。

maybe the Router set Proxy, you should change another Router that does not use proxy.

---
#### FragmentActivity 

默认情况下，按返回键会销毁Activity

```java
onBackPressed() -> onDestroy()
```



android.support.test doest exist
---

add dependencies in build.gradle

```groovy
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    testCompile 'junit:junit:4.12'
```

---
WifiManager Leak 
---

Android Studio Inspections:

On versions prior to Android N (24), initializing the WifiManager via Context#getSystemService can cause a memory leak if the context is not the application context. Change context.getSystemService(...) to context.getApplicationContext().getSystemService(...).

In many cases, it's not obvious from the code where the Context is coming from (e.g. it might be a parameter to a method, or a field initialized from various method calls.) It's possible that the context being passed in is the application context, but to be on the safe side, you should consider changing context.getSystemService(...) to context.getApplicationContext().getSystemService(...).

```html
 Activity com.afmobi.palmplay.StartActivity has leaked IntentReceiver android.net.wifi.WifiManager$1@9552346 that was originally registered here. Are you missing a call to unregisterReceiver()?
 android.app.IntentReceiverLeaked: Activity com.afmobi.palmplay.StartActivity has leaked IntentReceiver android.net.wifi.WifiManager$1@9552346 that was originally registered here. Are you missing a call to unregisterReceiver()?
 at android.app.LoadedApk$ReceiverDispatcher.<init>(LoadedApk.java:959)
 at android.app.LoadedApk.getReceiverDispatcher(LoadedApk.java:728)
 at android.app.ContextImpl.registerReceiverInternal(ContextImpl.java:1177)
 at android.app.ContextImpl.registerReceiver(ContextImpl.java:1157)
 at android.app.ContextImpl.registerReceiver(ContextImpl.java:1151)
 at android.content.ContextWrapper.registerReceiver(ContextWrapper.java:554)
 at android.net.wifi.WifiManager.init(WifiManager.java:2242)
 at android.net.wifi.WifiManager.<init>(WifiManager.java:750)
 at android.app.SystemServiceRegistry$45.createService(SystemServiceRegistry.java:551)
 at android.app.SystemServiceRegistry$45.createService(SystemServiceRegistry.java:548)
 at android.app.SystemServiceRegistry$CachedServiceFetcher.getService(SystemServiceRegistry.java:872)
 at android.app.SystemServiceRegistry.getSystemService(SystemServiceRegistry.java:825)
 at android.app.ContextImpl.getSystemService(ContextImpl.java:1370)
 at android.view.ContextThemeWrapper.getSystemService(ContextThemeWrapper.java:123)
 at android.app.Activity.getSystemService(Activity.java:5401)
 ...
 at android.os.Handler.dispatchMessage(Handler.java:111)
 at android.os.Looper.loop(Looper.java:207)
 at android.app.ActivityThread.main(ActivityThread.java:5763)
 at java.lang.reflect.Method.invoke(Native Method)
 at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:789)
 at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:679)
```
