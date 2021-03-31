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
