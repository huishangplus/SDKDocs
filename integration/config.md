##### 1.配置`AndroidManifest.xml`

首先，需要声明权限

```java
<uses-permission android:name="com.umpay.payplugin.permission.OPERATION_HARDWARE" />
```

然后在application标签添加通过魔方平台申请的支付的APPID，[申请APPID方法](http://partner.huishangplus.com/webmerser_jcs/common/APIfile.jsp "申请方法")。

```java
<application
         android:icon="@drawable/icon"
         android:label="@string/app_name" >
         <meta-data
            android:name="UMP_APPID"
            android:value="请输入您的用户APPID"/>
            ……
</application>

```
##### 2.初始化支付SDK

在自己的定义的`Application`类的`onCreate()`方法中调用
`UMPay.getInstance().init(this);`此方法就是为了获取`Application`的引用，并不会做耗时操作。


##### 3.绑定和解绑

在自己应用的第一个启动并不关闭`Activity`中的`onCreate()`方法中绑定，在`onDestroy()`方法中解绑，绑定成功之后才可以做后续操作


```java
//绑定的方法
UMPay.getInstance().bind(this, new UMBindCallBack() {
    @Override
    public void bindException(Exception e) {
        UMPayLog.e("绑定失败！" + e.getMessage());
    }

    @Override
    public void bindSuccess() {
        UMPayLog.e("绑定成功！");
    }

    @Override
    public void bindDisconnected() {
        UMPayLog.e("断开绑定！");
    }
});

```
```java
//解绑
UMPay.getInstance().unBind();
```


