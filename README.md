# 动态绑定
### 第一个实例：

如下用父类引用变量指向子类对象，来声明父类变量，创建子类对象

    public class Fu {
        int age = 50;
        public void hobby {
            System.out.println("听戏曲");
        }
    }
    
    public class Zi extends Fu {
        int age = 20;
        public void hobby () {
            System.out.println("打游戏");
        }
    }
    
    public class Demo {
        public static void main (String[] args) {
            Fu f = new Zi();
            f.hobby();
            System.out.println(f.age);
        }
    }
    
    输出：
    打游戏
    50

理解Fu f=new Zi（）；
f.方法名（）；
要记住一句话，*编译看左边，执行看右边*，即编译的时候，系统会认为你的f是Fu类型的，编译时用f去调用变量和方法都是去调用父类的，如果父类中没有你调用的方法或者变量，那么编译就会出错。
但实际上，我们知道f类的实际类型是Zi类的，所以在执行的时候，打印hobby方法打印的是子类的，这个过程，叫*动态绑定*，即f调用哪一个hobby方法是由他的实际类型决定，*但这对变量没用*，由图可见f.age还是调用的父类的age。
————————————————
版权声明：本文为CSDN博主「niceeicn」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/wokkkok/article/details/110876431
