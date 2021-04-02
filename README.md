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
要记住一句话，**编译看左边，执行看右边**，即编译的时候，系统会认为你的f是Fu类型的，编译时用f去调用变量和方法都是去调用父类的，如果父类中没有你调用的方法或者变量，那么编译就会出错。
但实际上，我们知道f类的实际类型是Zi类的，所以在执行的时候，打印hobby方法打印的是子类的，这个过程，叫**动态绑定**，即f调用哪一个hobby方法是由他的实际类型决定，**但这对变量没用**，由图可见f.age还是调用的父类的age。

### 第二个实例

如下在子类中新定义了一个Minorhobby, 我们知道它是属于子类的

    public class Zi extends Fu {
        int age = 20;
        public void Minorhobby() {
            System.out.println("唱歌");
        }
        public void hobby(){
            System.out.println("打游戏");
        }
    }
    
但是测试类中出现问题了

    public class Demo {
        public static void main(String[] args) {
            Fu f = new Zi();
            f.hobby();
            System.out.println(f.age);
            Zi z = new Zi();
            z.Minorhobby();
            f.Minorhobby();
        }
    }
    
    
绿色框中我们创建一个Zi类对象，调用Zi类方法，没问题

我们知道Fu f=new Zi（）；创建的f的实际指向对象也是子类对象，但是他却不能调用Zi类的方法Minorhobby，这也是由于无法通过编译造成的，编译时，系统会认为f就是Fu类的对象，而去寻找Fu类中有无Minorhobby方法，没找到，就报错了.

我们有没有办法就非要让f去访问Minorhobby方法呢？如下，用类型强转可以

    public class Demo {
        public static void main(String[] args) {
            Fu f = new Zi();
            f.hobby();
            System.out.println(f.age);
            
            // Zi f2 = f;  编译出错
            Zi f2 = (Zi)f; // 将f2 强转为子类
            f2.Minorhobby();
        }
    }
    
    输出：
    打游戏
    50
    唱歌

不过要注意，只能把父类的强转为子类的，而且该变量的实际类型也必须是子类
那问题来了，为什么要声明父类变量，创建子类对象呢，直接用第二张图绿色框中的形式不就行吗？
其实，用**父类引用变量指向子类对象，可以使得变量接受任意子类型的值，提高程序设计的通用性**

### 第三个实例
那如果我们再在父类中定义一个新方法呢，我们知道，子类是会继承这个方法的，所以无论f编译是父类还是子类，都能通过编译，无论运行是f是子类还是父类，也都能运行

    public class Fu {
        int age = 50;
        public void hobby() {
            System.out.println("看戏曲");
        }
        public void otherhobby(){
            System.out.println("抽烟");
        }
    }
    
    public class Demo {
        public static void main(String[] args) {
            Fu f = new Zi();
            f.hobby();
            f.otherhobby();
            System.out.println(f.age);
            Zi f2 = (Zi)f;
            f2.Minorhobby();
            f2.otherhobby();
        }
    }
    
    输出：
    打游戏
    抽烟
    50
    唱歌
    抽烟
