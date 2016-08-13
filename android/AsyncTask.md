### 一、Java中多线程的几种实现方式：
---
#### 1. 继承*Thread*类，重写*run()*方法：

	class MyThread extends Thread() {
		@Override
			ublic void run() {
			/处理逻辑
		}
	}

		
**启动方式：**

	new MyThread().start();

**缺点：**使用继承，耦合性太高。

#### 2.实现*Runnable*接口：

	class MyThread implements Runnable {
		@Override
		public void run() {
			//处理逻辑
		}
	}
	
	
**启动方式：**

	MyThread myThread = new MyThread();
	new Thread(myThread).start();

#### 3.匿名内部类的方式实现*Runnable*接口,比较常用:

	new Thread(new Runnable() {
		@Override
		public void run() {
			//处理逻辑
		}
	}).start();

### 二、异步消息处理机制：

1.**Message:**
	线程之间传递消息，内部可携带少量的信息，常用的字段有*what*,*arg1*,*arg2*,*obj*;其中what,arg1,arg2一般携带整型数据，obj字段携带一个Object对象。

2.**Handler:**
	主要用于发送和处理消息，常用方法有*sendMessage()*,*handleMessage()*.

3.**MessageQueue:**
	消息队列，不要用于存放所有通过handler发送的消息，这部分消息会一直存在于消息队列中，等待被处理。每个线程中只会有一个MessageQueue对象。

4.**Looper:**
	线程中的MessageQueue的管家，调用Looper的loop()方法后，就会进入无线循环当中，当发现MessageQueue中存在一条消息时，就会将它取出传递道Handler的handlerMessage()方法中。每个线程中也只会有一个Looper对象。

**重点：**
	因为Handler是在主线程中创建的，所以*handleMessage()*方法中的代码逻辑在主线程中执行，一般用来修改UI。

### 三、AsyncTask：

#### 1.**代码示例：**

	public class MyAsyncTask extends AsyncTask<Void, Integer, Boolean>
		{
	    		@Override
	    		protected void onPreExecute()
	    		{
				super.onPreExecute();
	    		}
	    		@Override
	    		protected void onPostExecute(Boolean aBoolean)
	    		{
				super.onPostExecute(aBoolean);
	    		}
	    		@Override
	    		protected void onProgressUpdate(Integer... values)
	    		{
				super.onProgressUpdate(values);
	    		}
	    		@Override
	   		    protected Boolean doInBackground(Void... params)
	    		{
				return null;
	    		}
		}

执行任务:

	new MyAsyncTask().execute();

#### 2.泛型参数说明：

1. Params：执行AsyncTask是传入的参数，可用于在后台任务中使用。
2. Progress：后台任务执行时，如果需要在界面上显示当前的进度，则使用这里指定的泛型作为进度单位。
3. Result：任务执行完毕，如果需要对结果进行返回，则使用这里的泛型作为返回值。

#### 3.AsyncTask的几个回调方法说明：
1. *__onPreExecute()__*
在*doInBackground(Params)*之前调用，用于进行一些界面上的初始化，例如显示一个进度条对话框等。
2. *__doInBackground(Params...)__*
这个方法中的所有代码都在子线程中运行，一般在这里进行耗时任务;任务一旦完成使用*return*语句将任务结果返回;如果要反馈任务进度，可以调用*publishProgress(Progress...)*方法来完成。
3. *__onProgress(Progress...)__*
当后台任务调用了*publishProgress(Progress...)*后，这个方法就会被调用，可以利用这个方法中的参数对主线程中UI进行操作。
4. *__onPostExecute(Result)__*
后台任务执行完毕并通过*return*语句返回时，这个方法就会被调用。根据返回的参数执行一些UI操作，比如关掉进度对话框，弹出*Toast*消息提醒任务执行完毕等。
