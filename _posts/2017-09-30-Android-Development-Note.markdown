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

绑定服务时抛出异常 'IllegalArgumentException: Service Intent must be explicit'
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