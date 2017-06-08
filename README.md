
Androidstudio中通过依赖使用zxing扫一扫简单使用
====
1、在module app中的build.gradle中加入依赖<br>  
 compile 'com.journeyapps:zxing-android-embedded:3.5.0'<br>
2、设置属性
```
IntentIntegrator integrator = new IntentIntegrator(MainActivity.this);
integrator.initiateScan();
