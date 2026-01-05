## 动态代理&Lambda

#### 使用反射原理实现动态代理达到动态编程的目的

```java
package ReflectionTest;

/**
 * @author sunchaowei
 * @create 2026/1/5-14:47
 */

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

interface Human {

    String getBelief();

    void eat(String food);

}

//被代理类
class SuperMan implements Human {


    @Override
    public String getBelief() {
        return "I believe I can fly!";
    }

    @Override
    public void eat(String food) {
        System.out.println("我喜欢吃" + food);
    }
}

class HumanUtil {

    public void method1() {
        System.out.println("====================通用方法一====================");

    }

    public void method2() {
        System.out.println("====================通用方法二====================");
    }

}

/*
要想实现动态代理，需要解决的问题？
问题一：如何根据加载到内存中的被代理类，动态的创建一个代理类及其对象。
问题二：当通过代理类的对象调用方法a时，如何动态的去调用被代理类中的同名方法a。


 */

class ProxyFactory {
    //调用此方法，返回一个代理类的对象。解决问题一
    public static Object getProxyInstance(Object obj) {//obj:被代理类的对象
        MyInvocationHandler handler = new MyInvocationHandler();

        handler.bind(obj);

        return Proxy.newProxyInstance(obj.getClass().getClassLoader(), obj.getClass().getInterfaces(), handler);
    }

}

class MyInvocationHandler implements InvocationHandler {

    private Object obj;//需要使用被代理类的对象进行赋值

    public void bind(Object obj) {
        this.obj = obj;
    }

    //当我们通过代理类的对象，调用方法a时，就会自动的调用如下的方法：invoke()
    //将被代理类要执行的方法a的功能就声明在invoke()中
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        HumanUtil util = new HumanUtil();
        util.method1();

        //method:即为代理类对象调用的方法，此方法也就作为了被代理类对象要调用的方法
        //obj:被代理类的对象
        Object returnValue = method.invoke(obj, args);

        util.method2();

        //上述方法的返回值就作为当前类中的invoke()的返回值。
        return returnValue;

    }
}

public class ProxyTest {

    public static void main(String[] args) {
        SuperMan superMan = new SuperMan();
        //proxyInstance:代理类的对象
        Human proxyInstance = (Human) ProxyFactory.getProxyInstance(superMan);
        //当通过代理类对象调用方法时，会自动的调用被代理类中同名的方法
        String belief = proxyInstance.getBelief();
        System.out.println(belief);
        proxyInstance.eat("四川麻辣烫");

        System.out.println("*****************************");

        NikeClothFactory nikeClothFactory = new NikeClothFactory();

        ClothFactory proxyClothFactory = (ClothFactory) ProxyFactory.getProxyInstance(nikeClothFactory);

        proxyClothFactory.produceCloth();

    }
}
```

#### Lambda表达式举例

```java
package LambdaTest;

import java.io.PrintStream;

/**
 * @author sunchaowei
 * @create 2026/1/4-08:50
 */
public class LambdaTest {

    public static void main(String[] args) {

        test(new Function01() {
            @Override
            public String doSomething(String aa, Integer bb) {
                return "传统的";
            }
        });

        test((String x1, Integer x2) -> {return "lambdafull";});

        test(( x1,  x2)->"lambdaeasy");

        test(Doer::hiHi2);

        Doer doer = new Doer();

        test(doer::hiHi);

        test(doer::doSomething);

        PrintStream os = System.out;

        test02(os::println);

        test02(System.out::println);

        /*
        总结:
        1. 只要参数相同就可以进行方法引用
        2. lambda表达式->符号左边表示接口抽象方法参数 右边表示具体方法体
        3. 如果方法参数只有一个可以去掉括号例如 (String x1) = String x1 参数类型可以从接口抽象方法推断因此类型也可以省略 String x1 = x1
        4. 方法体如果只有一句代码可以去掉大括号和可能存在的return语句但是";"需要保留 例如 { return new String("返回字符串"); } = new String("返回字符串");
        5. 因此简写后 x1 -> new String("返回字符串");
        6. 方法引用: "::"符号左边表示实现引用的对象,对于静态方法它表示类型名称,对于实例方法它表示类型的实例对象,引用的方法与接口的抽象方法参数和返回值类型必须相同
         */

    }

    public static void test(Function01 fcc) {
        System.out.println(fcc.doSomething("你好", 30));
    }
    public static void test02(printIf pp){
    }

}

class Doer implements Function01 {
    /**
     * @param aa
     * @param bb
     * @return
     */
    @Override
    public String doSomething(String aa, Integer bb) {
        return "接口实现方法";
    }

    public String hiHi(String cc, Integer dd) {
        return "实例同参方法";
    }

    public static String hiHi2(String cc, Integer dd) {
        return "静态同参方法";
    }
}
```