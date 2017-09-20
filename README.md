# MPremission
android 6.0动态权限申请简化库

[![](https://jitpack.io/v/guanguoxiang/MPremission.svg)](https://jitpack.io/#guanguoxiang/MPremission)

使用方法
```
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
  
  	dependencies {
          compile 'com.github.guanguoxiang.MPremission:api:1.0'
	        compile 'com.github.guanguoxiang.MPremission:annotations:1.0'
          annotationProcessor 'com.github.guanguoxiang.MPremission:compiler:1.0'
	}

```
在Activity或Fragment中
```
public class MainActivity extends AppCompatActivity {

    MPermission permission;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        permission=MPermission.with(this);
        //请求相机和读写的权限
        permission.apply(100, Manifest.permission.WRITE_EXTERNAL_STORAGE,Manifest.permission.CAMERA);

    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        permission.onRequestPermissionsResult(this,requestCode,permissions,grantResults);
    }

    @AuthorityOK(100)
    public void requestOK(){

    }

    @AuthorityFail(100)
    public void requestFail(){

    }

    @AuthorityOK(101)
    public void requestOtherOK(){

    }

    @AuthorityFail(101)
    public void requestOtherFail(){

    }


    @Override
    protected void onDestroy() {
        permission.recycle();
        super.onDestroy();
    }
}
```
