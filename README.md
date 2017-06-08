
Androidstudio中通过依赖使用zxing扫一扫简单使用
====
1、在module app中的build.gradle中加入依赖
```
 compile 'com.journeyapps:zxing-android-embedded:3.5.0'
```
2、设置属性
在点击事件中初始化
```
IntentIntegrator integrator = new IntentIntegrator(MainActivity.this);
integrator.initiateScan();
```
如果想要竖屏显示需要新建一个空的activity继承CaptureActivity
```
public class ScanActivity extends CaptureActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
}
```
在AndroidManifest.xml中设置ScanActivity属性
```
 <activity
            android:name=".ScanActivity"
            android:screenOrientation="portrait" />
```
然后在点击事件中设置属性
```
IntentIntegrator integrator = new IntentIntegrator(MainActivity.this);
                // 设置要扫描的条码类型，ONE_D_CODE_TYPES：一维码，QR_CODE_TYPES-二维码
                integrator.setDesiredBarcodeFormats(IntentIntegrator.QR_CODE_TYPES);
                integrator.setCaptureActivity(ScanActivity.class);
                integrator.setPrompt("请扫描二维码"); //底部的提示文字，设为""可以置空
                integrator.setCameraId(0); //前置或者后置摄像头
                integrator.setBeepEnabled(false); //扫描成功的「哔哔」声，默认开启
                integrator.setBarcodeImageEnabled(true);//是否保留扫码成功时候的截图 
                integrator.initiateScan();
```
3、添加权限
```
<uses-permission android:name="android.permission.CAMERA" />
```
4、对结果的处理
```
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        IntentResult scanResult = IntentIntegrator.parseActivityResult(requestCode, resultCode, data);
        if (scanResult != null) {
            String result = scanResult.getContents();
            Log.e("HYN", result);
            Toast.makeText(MainActivity.this, result, Toast.LENGTH_LONG).show();
        }
    }
```
