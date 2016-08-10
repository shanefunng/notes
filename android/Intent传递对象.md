## 使用Intent传递对象
---
### Serializable方式

**使用方式：**让需要传递的对象的类实现Serializable接口。

1. 实现Servializable接口：

		public class Person implements Serializable{
			private String name;
			private int age;
		
			public String getName(){
				return name;
			}
		
			public void setName(String name){
				this.name = name;
			}

			public int getAge(){
				return age;
			}

			public void setAge(int age){
				this.age = age;
			}
		}

2. 构造Intent：

		Person person = new Person();
		person.setName("Tom");
		person.setAge(20);
		Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
		intent.putExtra("person_data", person);
		startActivity(intent);

3. 获取Intent中的对象：

		Person person = (Person) getIntent().getSerializableExtra("person_data");

### Parcelable方式

**代码示例：**

1. 被传递的对象的类需要实现Parcelable接口：

		public class Person implements Parcelabale{
			private String name;
			private int age;
			
			......//省略getter/setter

			@Ovrride
			public int describeContents(){
				return 0;
			}
		
			@Override
			public void writeToParcel(Parcel dest, int flags){
				dest.writeString(name);//写出name
				dest.writeInt(age);//写出age
			}
			
			public static final Parcelable.Creator<Person> CREATOR = new Parcelable.Creator<Person>(){
				
				@Override
				public Person createFromParcel(Parcel source){
					Person person = new Person();
					person.name = source.readString();//读取name
					person.age = source.readInt();//读取age
					return person;
				}

				@Override
				public Person[] newArray(int size){
					return new Person[size];
				}
			};
		}


2. 构造Intent（同Serializable）
3. 获取Person对象：

		Person person = (Person) getIntent().getParcelableExtra("person_data");

### 两种方式的对比：

方式 | 原理 | 优缺点
--- | --- | ---
Serializable | 将整个对象序列化 | 实现方式比较简单
Parcelable | 将整个对象分解为内建的基本类型 | 效率高

**推荐使用Parcelable方式**


		