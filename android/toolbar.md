## Toolbar
---
### 1. 修改*styles.xml*, 使*AppTheme* 继承自*Theme.AppCompat.....NoActionBar*

		<resources>
			<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
				<item name="colorPrimary">@color/ColorPrimary</item>
				<item name="colorPrimaryDark">@color/ColorPrimaryDark</item>
				<item name="colorAccent">@color/ColorAccent</item>
			</style>
		</resources>

### 2. 在*main_activity.xml* 中添加*`<Toobar>`*

		<LinearLayout>
		<android.support.v7.widget.Toolbar
			android:layout_width="match_parent"
			android:layout_height="?attr/actionBarSize"
			android:background="?attr/colorPrimary"
			android:elevation="4dp"
			android:theme="@style/ThemeOverlay.AppCompat.ActionBar"
			app:popupTheme="@style/ThemeOverlay.AppCompat.Light"
		/>
		......
		</LinearLayout>

***注意：***上述xml属性中，*layout_height*,*background*,*elevation*必须添加;theme, popupTheme用法未知, 自定义toolbar高度如下：
	
	layout_height="Your customized height"
	minHeight="?attr/actionBarSize"

### 3. 创建*action_menu*, 添加其他*action*

	<menu xmlns:android=""
			xmlns:app="">
		<item
			android:id=""
			android:title=""
			android:icon=""
			app:showAsAction=""/>
	</menu>

### 4. 修改*MainActivity.class*
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main_activity);

		Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
		setSupportActionBar(toolbar);
	}
	
	@Override
	public boolean onCreateOptionsMenu(Menu menu)
	{
		getMenuInflater().inflate(R.menu.action_menu, menu);
		return super.onCreateOptionsMenu(menu);
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item)
	{
		switch(item.getItemId()){
			case R.id.search:
				//Do something
				return true;
			case R.id.settings:
				//Do your thing
				return true;
			default:
				return super.onOptionsItemSelected(item);
		}
		
	}