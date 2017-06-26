## Service
---

### 一、服务分类：
1. **标准服务：**
	1. 继承系统 `Service`，重写`onStartCommand()`方法;
	2. 在组件中（广播，或者activity）调用`startService()`方法启动服务；
	3. 在组件中（广播，或者activity）调用`stopService()`方法停止服务;
	4. **缺点：** 启动服务之后，组件与服务没有任何联系，此时只能调用 *stopService()*, *stopSelf()* 停止服务。
2. **绑定服务：**
	1. 继承系统`Service`，自定义内部类继承*Binder*类，声明内部类为成员变量;
	2. 重写`onBind()`方法，返回上一步声明的内部类;
	3. 在调用组件中声明自定义Binder类和ServiceConnection类，并在ServiceConnection的`onServiceConnected(ComponentName name, IBinder service)`方法中，将service向下转型获取引用并调用service中公开的方法;
	4. 在调用组件中调用`bindService()`和`unbindService()`方法绑定或者解绑服务。

3. **注意**
	任何一个服务在整个应用程序范围内都是通用的，即MyService不仅可以和MainActivity绑定，还可以和任何一个其他的活动进行绑定，而且在绑定完成后他们都可以获取到相同的mBinder实例。

---

### 二、服务的生命周期
* bind型的服务比非bind型服务多了`onBind()`,`onRebind()`,`onUnbind()`回调方法;
* 如果即调用了`startService()`,又调用了`bindService()`方法，那么必须同时调用`stopService()`和`unbindService()`方法才能停止服务。

---

### 三、服务的高级技巧

#### 前台服务
**场景：** 服务一般运行在后台，优先级比较低，当系统内存不足是，可能回收掉正在后台运行的服务。如果希望服务一直在后台运行，不会因为系统内存不足而被回收，可以使用前台服务。

**前台服务：** 它会一直有个正在运行的图标在系统的状态栏显示，下拉状态栏后可以看到更加详细的信息，非常类似于通知的效果。比如常见的音乐播放器、墨迹天气等。

**使用方式：** 在activity中调用`startForeground()`方法。

#### IntentService

**场景：** 服务中的代码运行在主线程中，如果直接在服务里处理一些耗时的任务，很容易出现ANR。这时候就应该在服务中的每个具体方法里开启一个子线程来处理耗时逻辑，例如在`onStartCommand()`中使用如下方式：

	public int onStartCommand(Intent intent , int flags, int startId){
		new Thread(new Runnable(){
			@Override
			public void run() {
				//处理逻辑
				stopSelf();//自己停止服务
			}
		}).start();
		return super.onStartCommand(intent, flags, startId);
	}

**缺点：**
这种服务一旦启动就会一直处于运行状态，必须调用`stopService()`或者`stopSelf()`方法才能让服务停止下来。
一般程序员容易忘记开启线程或者忘记调用*stopSelf()*方法，Android专门提供了一个默认开启线程并能自动停止的服务IntentService.



	
