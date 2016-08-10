## 全局获取Context的技巧
---
### 继承系统Application类：

	/**
 	* Created by shane on 7/10/16.
 	*/
	public class MyApplications extends Application
	{
    		private static Context mContext;

    		@Override
    		public void onCreate()
    		{
        		super.onCreate();
        		mContext = getApplicationContext();
    		}

    		public static Context getContext()
    		{
        		return mContext;
    		}
	}

### 修改manifest：
	<application 
		name = ".MyApplication"
		......
		......
	</application>
