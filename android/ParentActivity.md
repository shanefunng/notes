##向上导航
只支持api 16以上，16以下如下：

	<application>
		<activity name=".MainActivity">
		...
		<activity>
		<activity
			name=".ChildActivity"
			parentActivityName=".MainActivity">
			<!--Parent activity meta-data to support 4.0 and lower-->
			<meta-data
				android:name="android.support.PARENT_ACTIVITY"
				android:value=".MainActivity"/>
		<activity>
	</application>

修改MainActivity.class:

	Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
	setSupportActionBar(toolbar);

	ActionBar actionBar = getSupportActionBar();
	actionBar.setDisplayHomeAsUpEnabled(true);
