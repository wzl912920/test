Android 6.0会对targetSdkVersion < 23的应用默认授予所有申请的权限，意味着我们可以不做处理，但是然并卵，用户仍然可以在设置中取消所授予的权。这就需要我们在有用到权限的地方修改代码逻辑。
```Java
//1、申请权限
if (ContextCompat.checkSelfPermission(this, Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.PERMISSION_GRANTED) {
    ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
            WRITE_EXTERNAL_STORAGE_REQUEST_CODE);
}
//2、用户同意或拒绝后会回调下面方法
@Override
public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    if (requestCode == WRITE_EXTERNAL_STORAGE_REQUEST_CODE) {
           if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
           } else {
           }
       }
}
```
###### Fragment中使用注意事项
  * 1、fragment中直接调用自身的requestPermission，并重写onRequestPermissionResult方法，否则会调用到activity的onRequestPermissionResult方法中。
  * 2、在子fragment中调用时，需要使用getParentFragment.requestPermission的方法，然后在父fragment中回调子fragment的onRequestPermission方法就可以了。

需要进行验证的权限
<br>BODY_SENSORS
<br>CALENDAR
<br>CAMERA
<br>CONTACTS
<br>LOCATION
<br>AUDIO
<br>PHONE
<br>MESSAGE
<br>STORAGE
