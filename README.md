# MultiPictureView


[![](https://jitpack.io/v/goyourfly/MultiPictureView.svg)](https://jitpack.io/#goyourfly/MultiPictureView)

##### MultiPictureView 是一个将多张图片组合显示并支持添加和删除的控件

### Demo

<table>
<tr>
<td>
<img src='./screenshot/ss1.png' width=‘200’/>
</td>
<td>
<img src='./screenshot/ss2.png' width=‘200’/>
</td>
</tr>
</table>

### Usage
> 详细的使用请看示例代码

##### 1. 在布局中声明
````xml
<com.goyourfly.multi_picture.MultiPictureView
	android:id="@+id/multi_image_view"
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	app:editable="false"
	app:deleteDrawable="@drawable/..."
	app:addDrawable="@drawable/..."
	app:imageLayoutMode="DYNAMIC"
	app:maxImage="9"
	app:space="6dp"
	app:span="3" />
````

|  参数  |  类型  |  说明  |  默认值  |
|----|----|----|----|
| editable| boolean | 是否可编辑（添加和删除）| false |
|  span | integer | 每行最多显示多少 | 3 |
| space | dimension | 图片间隔大小  | 8dp |
| maxImage | integer | 最多显示多少张图片 | 9 |
| imageLayoutMode | integer | 图片布局类型：动态(DYNAMIC=1)和静态(STATIC=2) | STATIC=2 |
| deleteDrawable | drawable | 删除图标 | 红色删除Drawable |
| addDrawable | drawable | 添加图片 | 灰色添加图片Drawable |

##### 2. 在代码中使用
###### 2.1 初始化ImageLoader
````kotlin
MultiPictureView.setImageLoader(object : ImageLoader {
    override fun loadImage(image: ImageView, uri: Uri) {
        Vincent.with(image.context)
                .load(uri)
                .placeholder(R.drawable.ic_placeholder_loading)
                .error(R.drawable.ic_placeholder_loading)
                .into(image)
    }
})
````

###### 2.2 绑定图片资源，设置事件监听
```` java
multiPictureView = (MultiPictureView) findViewById(R.id.multi_image_view);
// 设置图片资源
multiPictureView.setList(list:List<Uri>)
multiPictureView.setAddClickCallback(new MultiPictureView.AddClickCallback() {
    @Override
    public void onAddClick(int index) {
		...
    }
});
multiPictureView.setDeleteClickCallback(new MultiPictureView.DeleteClickCallback() {
    @Override
    public void onDeleted(int index) {
		...
    }
});
multiPictureView.setItemClickCallback(new MultiPictureView.ItemClickCallback() {
    @Override
    public void onItemClicked(int index, @NotNull ArrayList<Uri> uris) {
		...
    }
});
````

### Compile

[![](https://jitpack.io/v/goyourfly/MultiPictureView.svg)](https://jitpack.io/#goyourfly/MultiPictureView)

Step 1. Add it in your root build.gradle at the end of repositories:

````
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
````

Step 2. Add the dependency

````
dependencies {
    compile 'com.github.goyourfly:MultiPictureView:latestVersion'
}
````

