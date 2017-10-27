---
layout: post
title: Java WeakReference 使用错误一例
date: 2017-10-27 15:32:24.000000000 +09:00
tag: Android
---

Java WeakReference 使用错误一例
--------------------------------------

FileShareService.java
```java
public class FileShareService extends Service {
    ...
    private void initWifi() {
        wifiServer = new WifiApServer(this, new WifiApResultHandler() {
        @Override
        public void onResult(boolean state, Object data) {
                if (state) {
                    startHttpServer();
                }
            }
        });
    }
    ...
}
```

WifiApServer.java

```java
public class WifiApServer {
  private WeakReference<WifiApResultHandler> mResultRef;
  ... 
  public WifiApServer(Context context, WifiApResultHandler shareHandler) {
      mResultRef = new WeakReference<>(shareHandler);
  }
  
  private void startWifiAp(String ssid, String password) {
    WifiApResultHandler resultHandler = mResultRef.get();
    ... 
  }
}
```



#### Problem

在WifiApServer.startWifiAp中，resultHandler 的值是null。


#### Solution
FileShareService 中把WifiApResultHandler对象放在类的属性中：
```java
public class FileShareService extends Service {
    ...
    private WifiApResultHandler mWifiSpotResultHandler = new WifiApResultHandler() {
        @Override
        public void onResult(boolean state, Object data) {
            if (state) {
                startHttpServer();
            }
        }
    };
  
    private void initWifi() {
        wifiServer = new WifiApServer(this, mWifiSpotResultHandler);
    }
    ...
} 
```