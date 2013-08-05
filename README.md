# Waterfall
=========

瀑布流，Endless view，Pinterest like

Easy to use Waterfall, Welcome to use it and tell me

Email: kjsoloho@gmail.com

---

## Usage

在你的xml中添加下面的布局: 

```xml
<org.solo.waterfall.WaterfallSmartView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:waterfall="http://schemas.android.com/apk/res/org.solo.waterfall"
    android:id="@+id/waterfall"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="5dp"
    waterfall:column="3"
    waterfall:itemMargin="5dp" >

    <!-- 你可以自定义自己的LinearLayout，建议是用LinearLayout布局
         列表将会加入到下面的布局里，使用方法于ScrollView类似  -->

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal" >
    </LinearLayout>

</org.solo.waterfall.WaterfallSmartView>
```

给WaterfallSmartView添加Adapter，就像使用ListView一样

``` java
private WaterfallSmartView mWaterfall;

@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
		
	mAdapter = new PhotoAdapter(this);
	mWaterfall = (WaterfallSmartView) findViewById(R.id.waterfall);
	mWaterfall.setAdapter(mAdapter);
	mWaterfall.setOnItemClickListener(this);		
}
```

定义Adapter的时候要注意，项目只能一次一次的加入，同时要同步到WaterFallSmartView

``` Java
class PhotoAdapter extends ArrayAdapter<String> {

	public void add(String object, int weight, int height) {
		super.add(object);
		// AddItem to waterfall in same time
		mWaterfall.addItem(object, weight, height);
	}		
    
}
```

我借用了[Universal-Image-Loader](https://github.com/nostra13/Android-Universal-Image-Loader)来加载图片

``` Java
ImageLoadingListener mImageLoadingListener = new ImageLoadingListener() {
	@Override
	public void onLoadingComplete(final String imageUri, View view, Bitmap loadedImage) {
		mAdapter.add(imageUri, loadedImage.getWidth(), loadedImage.getHeight());
	}
};
```

## License

    Copyright 2013 Chris Banes

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
