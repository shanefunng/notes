##自定义View
1. 继承View, or ViewGroup, or SDK内置的组件;
2. 分别实现构造方法, onMeasure(), onLayout(), onDraw()等方法；
3. 在attrs.xml中声明自定义属性;
4. 在布局文件中使用。

---
##代码片段：

  public class Person{
    private String name;
    private String sex;
    private int age;
    private int zipCode;
    
    public void setName(String name){
      this.name = name;
    }
    
    public void setAge(int age){
      this.age = age
    }
  }
  
  ##结论：
  
  
