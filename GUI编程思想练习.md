# GUI编程思想练习

## 组件

- 窗口
- 弹窗
- 面板
- 文件框
- 列表框
- 按钮
- 图片
- 监听事件
- 鼠标事件
- 键盘事件
- 外挂
- 破解工具

## GUI简介

Gui的核心技术：Swing AWT

不流行主要原因：

1. 因为界面不美观。
2. 需要 jre 环境！

为什么我们要学习？

1. 可以写出自己心中想要的一些小工具。
2. 工作时候，也可能需要维护到swing界面，概率极小！
3. 了解MVC架构，了解监听！

## AWT

### AWT介绍

1. 包含了很多类和接口！ GUI：图形用户界面编程
2. 元素：窗口，按钮，文本框
3. 包都在java（awt）包

### 组件和容器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210116203349262.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3J6ejY1NDUyMDY0,size_16,color_FFFFFF,t_70#pic_center)

#### Frame框架

```java
 //Gui 的第一个界面
    public static void main(String[] args){
        //Frame,JDK,看源码！（JDK帮助文档）
        Frame frame = new Frame("我的第一个Java图像界面窗口");
        //需要设置可见性
        frame.setVisible(true);
        //设置窗口大小
        frame.setSize(400,400);
        //设置背景颜色，可以直接查源代码设置已有的颜色frame.setBackground(Color.black);
        //也可以直接输入new color(r.g.b)三基色
        frame.setBackground(new Color(37, 80, 167));
        //弹出的初始位置
        frame.setLocation(200,200);
        //已经大概有雏形，但是没有设置关闭窗口功能，最小化、最大化、窗口尺寸已经默认存在。
        //设置大小固定
        frame.setResizable(false);
    }
```

这样写的问题是窗口无法关闭，只能结束java程序运行才行。

封装思想重写上述功能：

```java
import java.awt.*;
public class TestFrame2 {
    public static void main(String[] args) {
        //可能需要多个窗口
        MyFrame myFrame1 = new MyFrame(100, 100, 200, 200, Color.blue);
        MyFrame myFrame2 = new MyFrame(150, 150, 200, 200, Color.yellow);
        MyFrame myFrame3 = new MyFrame(200, 200, 200, 200, Color.red);
        MyFrame myFrame4 = new MyFrame(250, 250, 200, 200, Color.green);
    }
}
class MyFrame extends Frame {
    static int id = 0;      //可能存在多个窗口，需要一个计数器
    public MyFrame(int x,int y,int w,int h,Color color){
        super("Myframe+"+(++id));//继承
        setBounds(x, y, w, h);//坐标
        setBackground(color);//颜色
        setVisible(true);//可见性
    }
}
```

#### 面板Panel

```java
import java.awt.*;
//panel 可以看成是一个空间，但是不能单独存在
public class TestPanel {
    public static void main(String[] args){
        Frame frame = new Frame();  //new 窗口
        //布局的概念
        Panel panel = new Panel();  //new 面板
        Panel panel1 = new Panel();
        //设置布局,不设置面板会置顶
        frame.setLayout(null);
        //窗口坐标和颜色
        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(140, 208, 212));
        //panel 设置坐标，相对于frame
        panel.setBounds(50,50,400,100);
        panel.setBackground(new Color(181, 186, 54));
        panel1.setBounds(50,200,400,250);
        panel1.setBackground(new Color(165, 34, 101));
        //将panel添加进frame
        frame.add(panel1);
        frame.add(panel);
        frame.setVisible(true);

    }
}
```

### 布局

- 流式布局
- 东西南北中
- 表格布局

#### 流式布局

frame.setLayout(new FlowLayout(0));

```java
import java.awt.*;
public class TestFlowLayout  {
    public static void main(String[] args) {
        Frame frame = new Frame();
        //组件-按钮
        Button button1 = new Button("button1");
        Button button2 = new Button("button2");
        Button button3 = new Button("button3");
        //设置流式布局的位置
        //frame.setLayout(new FlowLayout(0));	0为左，1为中...
        frame.setLayout(new FlowLayout(FlowLayout.LEFT));//两种方式
        frame.setSize(200,200);
        //把按钮添加上去
        frame.add(button1);
        frame.add(button2);
        frame.add(button3);
        frame.setVisible(true);
    }
}
```

#### 东西南北中

frame.add(按键名字,BorderLayout.EAST方位);

```java
import java.awt.*;
public class TestBorderLayout {
    public static void main(String[] args) {
        Frame frame = new Frame("TestBorderLayout");
        Button east = new Button("East");
        Button west = new Button("West");
        Button south = new Button("South");
        Button north = new Button("North");
        Button center = new Button("Center");
        frame.setSize(400,400);
        //不同布局的方位
        frame.add(east,BorderLayout.EAST);
        frame.add(west,BorderLayout.WEST);
        frame.add(south,BorderLayout.SOUTH);
        frame.add(north,BorderLayout.NORTH);
        frame.add(center,BorderLayout.CENTER);
        frame.setVisible(true);
    }
}
```

#### 表格布局

TestGridLayout

```java
import java.awt.*;
public class TestGridLayout {
    public static void main(String[] args) {
        Frame frame = new Frame("TestGridLayout");
        Button btn1 = new Button("btn1");
        Button btn2 = new Button("btn2");
        Button btn3 = new Button("btn3");
        Button btn4 = new Button("btn4");
        Button btn5 = new Button("btn5");
        Button btn6 = new Button("btn6");
        frame.setLayout(new GridLayout(3,2));
        frame.add(btn1);
        frame.add(btn2);
        frame.add(btn3);
        frame.add(btn4);
        frame.add(btn5);
        frame.add(btn6);
        frame.pack();//Java函数，用于优化大小；
        // frame.setSize(400,400);
        frame.setVisible(true);
    }
}
```

总结：

1. Frame 是一个顶级窗口
2. Panel 无法单独显示，必须添加到某个容器中
3. 布局管理器
   1. 流式
   2. 东西南北中
   3. 表格
4. 大小、定位、背景颜色、可见性、监听

### 事件监听

事件监听：当某个事件发生的时候，干什么?

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
public class TesActionEvent {
    public static void main(String[] args) {
        //按下按钮，触发一些事件
        Frame frame = new Frame();
        Button button = new Button();
        /*按钮可以new一个接口，需要命名内部类，把他的实现类写下来。但一般不这么做
        button.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {  }  });*/
        
        //因为,addActionListener()需要一个ActionListener，所以我们需要构造一个ActionListener
        //接口就写实现类，父类就继承
        MyActionListener myActionListener = new MyActionListener();
        button.addActionListener(myActionListener);
        frame.add(button,BorderLayout.CENTER);
        windowClose(frame);
        frame.pack();
        frame.setVisible(true);
    }
    //关闭窗体的事件
    private static void windowClose(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}
class MyActionListener implements ActionListener{
    //事件监听
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("666");
    }
}
```

任何事件的监听都可以用ActionListener类，按钮、文本、鼠标、网络编程、内部类…

#### **多按钮共享一个事件**

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
public class TestActionTwo {
    public static void main(String[] args) {
        //两个按钮，实现同一个监听
        //开始--停止
        Frame frame = new Frame("开始-停止");
        Button button1 = new Button("start");
        Button button2 = new Button("stop");
      // button2.setActionCommand("button2-stop");
        MyMonitor myMonitor = new MyMonitor();
        button1.addActionListener(myMonitor);
        button2.addActionListener(myMonitor);
        frame.add(button1,BorderLayout.NORTH);
        frame.add(button2,BorderLayout.SOUTH);
        frame.pack();
        frame.setVisible(true);
    }
}
class MyMonitor implements ActionListener{
    @Override
    public void actionPerformed(ActionEvent e) {
        /*e.getActionCommand() 获取按钮的信息
        System.out.println("按钮被点击了：msg=>"+e.getActionCommand());
        输出结果butoo2为"按钮被点击了：msg=>stop";可以显示的定义触发会返回的命令
        butoo1为"start"。无显示定义，则会走默认的值。
        */
        //可以多个按钮只写一个监听类
        if (e.getActionCommand().equals("start")){//equals 等号
            System.out.println(e.getActionCommand()+"按钮被点击");
        } if (e.getActionCommand().equals("stop")){
            System.out.println(e.getActionCommand()+"按钮被点击");
        }
    }
}
```

### 输入框TextField 监听

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TestText01 {
    public static void main(String[] args) {
        new MyFrame();
    }
}
class MyFrame extends Frame{
    public MyFrame(){
        TextField textField = new TextField();//文本 TextArea文本域，可以写多行
        add(textField);
        //监听这个文本框输入的文字
        MyActionListener2 myActionListener2 = new MyActionListener2();
        //按下enter 就会触发这个输入框的事件
        textField.addActionListener(myActionListener2);
        //设置替换编码
        textField.setEchoChar('*');
        setVisible(true);
        pack();
    }
}
class MyActionListener2 implements ActionListener{//监听器
    @Override
    public void actionPerformed(ActionEvent e) {
        TextField field = (TextField)e.getSource();//获得一些资源,返回的一个对象
        System.out.println(field.getText());//获得输入框的文本
        field.setText("");//设置enter 后的状态
    }
}
```

### 画笔

基本图形

```java
import java.awt.*;
public class TestPaint {
    public static void main(String[] args) {
        new MyPaint().loadFrame();
    }
}
class MyPaint extends Frame {
    public void loadFrame(){
        setBounds(200,200,600,500);
        setVisible(true);
    }
    //画笔，颜色，可以画画
   @Override
    public void paint(Graphics g) {
       // super.paint(g);有些类里面有初始化操作，就无法删除
       g.setColor(Color.red);
       //g.drawOval(100,100,100,100);   //draw空心
       g.fillOval(100,100,100,100);   //fill实心、填充的
       g.setColor(Color.GREEN);
       g.fillRect(200,200,200,200);
       //养成习惯，画笔用完，将它还原到最初的颜色，不然你再化一个图会带上之前的颜色。
    }
}
```

### 鼠标监听

```java
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.ArrayList;
import java.util.Iterator;

//鼠标监听事件
public class TestMouseListener {	//（1）
    public static void main(String[] args) {
    new MyFrame("画图");
    }
}
//自己的类
class MyFrame extends Frame{		//（2）
    //画画需要画笔，需要监听鼠标当前的位置，需要集合来存储这个点
    ArrayList points;


    public MyFrame(String title) {//--------框架
        super(title);       //名字                                           
        setBounds(200, 200, 400, 300);
        //存标点击的点
        points = new ArrayList<>();
        //鼠标监听器，针对这个窗口
        this.addMouseListener(new MyMouseListener());        //-监听鼠标

        setVisible(true);
    }
    @Override				//（3）
    public void paint(Graphics g) { //画画                  //--------------画笔存储实施
        //画画，需要监听鼠标的事件
        Iterator iterator = points.iterator();              //-迭代器
        while (iterator.hasNext()){                         //检查序列中是否还有元素
            Point point = (Point) iterator.next();
            g.setColor(Color.BLUE);
            g.fillOval(point.x,point.y,10,10);
        }
    }
    //添加一个点到界面上，点集合			//（4）
    public void addPaint(Point point){
        points.add(point);                  //将（点）传到迭代器里


    }


    //适配器模式，就是别人已经写好的端口，不用全部重写内部类，直接继承更加方便。
    private class MyMouseListener extends MouseAdapter{  //（5）    //----------监听器
            //鼠标，按下，弹起，按下不放。
            @Override
            public void mousePressed(MouseEvent e) {        //-鼠标按下
               MyFrame frame = (MyFrame) e.getSource();     //-鼠标按下的来源
                //这里我点击的时候，就会在界面上产生一个点
                //这个点就是鼠标的点
                frame.addPaint(new Point(e.getX(),e.getY()));//--将监控的（点的坐标）传到点集合
                //每次点击鼠标都需要重写画一遍
                frame.repaint();                             //再次刷漆
            }
        }
}            
```

画图构造流程图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210116203245402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3J6ejY1NDUyMDY0,size_16,color_FFFFFF,t_70#pic_center)

编程步骤：

1. 生成main方法（1）

2. 创建自己的类（2），框架类，画笔类（3），监听器类（5）

3. （2）生成框架类内基本信息，super,Bounds,Visidle

4. （2）生成集合ArrayLiset

5. （3）画笔类：生成：迭代器iterator；

6.  条件：假如迭代器内有元素，则赋值point；

7.  并且画圆，坐标（point.x,y），大小，颜色；

8. （4）创建一集合点，将未来监控的点传到画笔迭代器里

9. （5）监听器继承MouseAdapter,生成mousePressed；获取按键来源；将点的来源传至集合点（4）；再次刷漆

10. （2）框架监控鼠标；（1）new 框架；运行

### 窗口监听

```java
package com.ssxxz.lesson03;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestWindow {
    public static void main(String[] args) {
        new WindowFrame("窗口监听");
    }
}
class WindowFrame extends Frame{
    public WindowFrame(String kk) {
        super(kk);
        setBackground(Color.cyan);
        setBounds(100,100,200,200);
        setVisible(true);
        //匿名内部类
        this.addWindowListener(
                new WindowAdapter() {
                    @Override
                    public void windowOpened(WindowEvent e) {
                        System.out.println("窗口打开");
                    }
                    @Override
                    public void windowClosed(WindowEvent e) {
                        System.out.println("窗口关闭中");
                    }
                    @Override
                    public void windowActivated(WindowEvent e) {
                        System.out.println("窗口激活");
                        WindowFrame source = (WindowFrame) e.getSource();       //获取框架信息
                        source.setTitle("被激活了");
                    }
                    @Override
                    public void windowStateChanged(WindowEvent e) {
                        WindowFrame source = (WindowFrame) e.getSource();
                        source.setTitle("状态改变了");
                        System.out.println("窗口状态改变");
                    }
                    @Override
                    public void windowClosing(WindowEvent e) {
                        System.out.println("窗口关闭");
                        System.exit(0);
                    }
                }
        );
    }
   /* 通过匿名内部类可以不用另外创建类
   class MyWindowListener extends WindowAdapter{
        @Override
        public void windowClosing(WindowEvent e) {
            setVisible(false);      //隐藏窗口，通过按钮点击事件
            System.exit(0);         //0正常退出，1非正常退出
        }
    }*/
}
```

### 键盘监听

```java
import java.awt.*;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
//键盘
public class TestKeyListener {
    public static void main(String[] args) {
        new KeyFrame();
    }
}
class KeyFrame extends Frame{
    public KeyFrame() {
        setBounds(10,10,300,400);
        setVisible(true);
        this.addKeyListener(new KeyAdapter() {
            //键盘按下
            @Override
            public void keyPressed(KeyEvent e) {
                //获得当前键盘的码
                int keyCode = e.getKeyCode();       //不需要去记录这个数值，直接使用静态属性VK_XXX
                System.out.println(keyCode);
                if (keyCode == KeyEvent.VK_UP){     //KeyEvent.VK 按键类
                    System.out.println("你按下了上键！");
                }
                //根据按下不同操作，产生不同结果。
            }
        });
    }
}
```

## Swing

### 窗口、面板

```java
import javax.swing.*;
import java.awt.*;
public class JFrameDemo {
    //init();初始化
    public void init(){
        //顶级窗口
        JFrame jf = new JFrame("这是一个JFrame窗口");
        jf.setVisible(true);
        //jf.setBackground(Color.cyan);     因为在容器中，直接颜色没效果，需要容器实例化
        jf.setBounds(100,100,200,200);
        JLabel jLabel = new JLabel("欢迎来到狂神说Java系列节目");  //标签
        jf.add(jLabel);
        //让文本标签居中，设置水平对齐
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);
        //需要容器实例化,颜色才能现象
        Container contentPane = jf.getContentPane();
        contentPane.setBackground(Color.cyan);
        //关闭事件
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
    public static void main(String[] args) {
        //建立一个窗口
        new JFrameDemo().init();
    }
}
```

### 弹窗

JDialog，用来被弹出，默认就有关闭事件！

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
//主窗口
public class DialogDemo extends JFrame {
    public DialogDemo() {
        this.setVisible(true);      //可见
        this.setSize(700,500);          //尺寸
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);       //关闭事件
        //JFrame 放东西，容器
        Container container = this.getContentPane();
        //绝对布局，会相对容器自动定位
        container.setLayout(null);
        //按钮
        JButton button = new JButton("点击弹出一个对话框");      //创建
        button.setBounds(30,30,200,50);
        //点击这个按钮的时候，弹出一个弹窗
        button.addActionListener(new ActionListener() {           //监听器
            @Override
            public void actionPerformed(ActionEvent e) {
                //监听弹窗
                new MyDialogDemo();
            }
        });
        container.add(button);      //将按钮放进容器中
    }
    public static void main(String[] args) {
        new DialogDemo();
    }
}
        //弹窗的窗口
class MyDialogDemo extends JDialog{
            public MyDialogDemo() {
                this.setVisible(true);
                this.setBounds(100,100,500,500);
           // this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);    弹窗可以被关掉，不需要额外添加事件
                Container container = this.getContentPane();
                container.setLayout(null);

                container.add(new Label("学Java"));
            }
        }
```

### 标签

lebel

```java
new JLabel("xxx");
```

图标ICON

```java
import javax.swing.*;
import java.awt.*;

//图片，需要实现类，Frame 继承
public class IconDemo extends JFrame implements Icon {

    private int width;
    private int height;

    public IconDemo(){}

    public IconDemo(int width,int height){
        this.width = width;
        this.height = height;
    }


    public void init(){     //图标
        IconDemo iconDemo = new IconDemo(15,15);
        //图标放在标签上，也可以放在按钮上!
        //标签，图标，位置
        JLabel label = new JLabel("icontest", iconDemo, SwingConstants.CENTER);

        Container container = getContentPane();
        container.add(label);

        this.setVisible(true);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
    
    public static void main(String[] args) {
        new IconDemo().init();
    }
    @Override       //图标尺寸
    public void paintIcon(Component c, Graphics g, int x, int y) {
        g.fillOval(x,y,width,height);
    }

    @Override
    public int getIconWidth() {
        return this.width;
    }

    @Override
    public int getIconHeight() {
        return this.height;
    }
}
```

图片

```java
import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class ImageIconDemo extends JFrame {
    public ImageIconDemo()  {
        //获取图片的地址
        JLabel label = new JLabel("ImageIcon");
        URL url = ImageIconDemo.class.getResource("xxx.jpg");//获取当前类以下的东西

        ImageIcon imageIcon = new ImageIcon(url);//命名不要冲突
        label.setIcon(imageIcon);
        label.setHorizontalAlignment(SwingConstants.CENTER);

        Container contentPane = getContentPane();
        contentPane.add(label);

        setVisible(true);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        setBounds(100,100,300,500);
    }
    public static void main(String[] args) {
        new ImageIconDemo();
    }
}
```

### 面板

JPanel

```java
import javax.swing.*;
import java.awt.*;


public class JPanelDemo extends JFrame {
    public JPanelDemo() {
        Container container = this.getContentPane();
        //后面参数的意思，面板与面板的间距
        container.setLayout(new GridLayout(2,1,10,10));

        JPanel panel1 = new JPanel(new GridLayout(1, 3));   //GridLayout网格布局
        JPanel panel2 = new JPanel(new GridLayout(2, 1));
        JPanel panel3 = new JPanel(new GridLayout(2, 3));

        panel1.add(new JButton("1"));
        panel1.add(new JButton("1"));
        panel1.add(new JButton("1"));
        panel2.add(new JButton("2"));
        panel2.add(new JButton("2"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));

        container.add(panel1);
        container.add(panel2);
        container.add(panel3);

        this.setVisible(true);
        this.setSize(500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }
    public static void main(String[] args) {
        new JPanelDemo();
    }
}
```

边框，文本域

JScrollPanel

```java
import javax.swing.*;
import java.awt.*;

public class JScrollDemo extends JFrame {
    public JScrollDemo() {
        Container container = this.getContentPane();
        //文本域
        JTextArea textArea = new JTextArea(20, 50);
        textArea.setText("欢迎学习狂神说Java");
        //Scroll 面板
        JScrollPane scrollPane = new JScrollPane(textArea);
        container.add(scrollPane);

        this.setBounds(100,100,300,350);
        this.setVisible(true);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new JScrollDemo();
    }
}
```

### 按钮

```java
import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class JButtonDemo01 extends JFrame {
    public JButtonDemo01() {
        Container container = this.getContentPane();
        //将一个图片变为图标
        URL resource = JButtonDemo01.class.getResource("123.jpg");  //图片路径
        ImageIcon icon = new ImageIcon(resource);       //转换为图标

        //把这个图标放到按钮上
        JButton button = new JButton();
        button.setIcon(icon);
        button.setToolTipText("图片按钮");      //图片按钮提示
        //add
        container.add(button);

        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }

    public static void main(String[] args) {
        new JButtonDemo01();
    }
}
```

- 单选按钮

```java
import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class JButtonDemo02 extends JFrame{
    public JButtonDemo02() {
        Container container = this.getContentPane();
        //将一个图片变为图标
        URL resource = JButtonDemo01.class.getResource("123.jpg");  //图片路径
        ImageIcon icon = new ImageIcon(resource);       //转换为图标

        //单选框
        JRadioButton radioButton1 = new JRadioButton("JRadioButton01");
        JRadioButton radioButton2 = new JRadioButton("JRadioButton02");
        JRadioButton radioButton3 = new JRadioButton("JRadioButton03");
        //由于单选框只能选择一个，可以将他们分组，一个组只能选一个。
        ButtonGroup group = new ButtonGroup();      //组
        group.add(radioButton1);                    
        group.add(radioButton2);
        group.add(radioButton3);

        container.add(radioButton1,BorderLayout.CENTER);
        container.add(radioButton2,BorderLayout.NORTH);
        container.add(radioButton3,BorderLayout.SOUTH);


        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }

    public static void main(String[] args) {
        new JButtonDemo02();
    }
}
```

- 复选按钮

```java
import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class JButtonDemo03 extends JFrame {
    public JButtonDemo03() {
        Container container = this.getContentPane();
        //将一个图片变为图标
        URL resource = JButtonDemo01.class.getResource("123.jpg");  //图片路径
        ImageIcon icon = new ImageIcon(resource);       //转换为图标

        //多选框
        JCheckBox checkBox01 = new JCheckBox("checkBox01");
        JCheckBox checkBox02 = new JCheckBox("checkBox02");
        
        container.add(checkBox01,BorderLayout.NORTH);
        container.add(checkBox02,BorderLayout.SOUTH);

        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }
    public static void main(String[] args) {
        new JButtonDemo03();
    }
}
```

### 列表

- 下拉框

```java
import javax.swing.*;
import java.awt.*;

public class TsetComboboxDemo01 extends JFrame {
    public TsetComboboxDemo01() {
        Container container = this.getContentPane();
        JComboBox status = new JComboBox();
        status.addItem(null);
        status.addItem("正在上映");
        status.addItem("已下架");
        status.addItem("即将上映");

        // status.addActionListener(); 监听获取值

        container.add(status);

        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TsetComboboxDemo01();
    }
}
```

- 列表框

```java
import javax.swing.*;
import java.awt.*;
import java.util.Vector;

public class TsetComboboxDemo02 extends JFrame {
    public TsetComboboxDemo02() {
        Container container = this.getContentPane();
        //生产列表的内容
        //String[] contents = {"1","2","3"};    静态数组

        Vector contents = new Vector();

        //列表中需要放入内容
        JList jList = new JList(contents);      //列表

        //动态数组
        contents.add("zhangsan");
        contents.add("lisi");
        contents.add("wangwu");
        
        container.add(jList);

        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
    public static void main(String[] args) {
        new TsetComboboxDemo02();
    }
}
```

- 应用场景
  - 下拉框：选择地址或者一些单个选项（一到两个最好使用按钮，两个以上使用下拉框，节省内存布局）
  - 列表框：展示信息，一般是动态扩容。

### 文本框

- 文本框 **TextField**

```java
import javax.swing.*;
import java.awt.*;

public class TestTextDemo01 extends JFrame  {
    public TestTextDemo01() throws HeadlessException {
        Container container = this.getContentPane();


        JTextField textField1 = new JTextField("hello",50);    //文本框+尺寸
        JTextField textField2 = new JTextField("world");

        container.add(textField1,BorderLayout.NORTH);
        container.add(textField2,BorderLayout.SOUTH);


        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TestTextDemo01();
    }
}
```

- 密码框 **PasswordField**

```java
import javax.swing.*;
import java.awt.*;

public class TestTextDemo02 extends JFrame {
    public TestTextDemo02() throws HeadlessException {
        Container container = this.getContentPane();

        JPasswordField passwordField = new JPasswordField();    //密码框***
        passwordField.setEchoChar('?');                         //密码框显示符号

        container.add(passwordField);


        this.setVisible(true);
        this.setSize(500,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TestTextDemo02();
    }
}
```

- 文本域 **TextArea**

```java
import javax.swing.*;
import java.awt.*;

public class JScrollDemo extends JFrame {
    public JScrollDemo() {
        Container container = this.getContentPane();
        //文本域
        JTextArea textArea = new JTextArea(20, 50);
        textArea.setText("欢迎学习狂神说Java");
        //Scroll 面板
        JScrollPane scrollPane = new JScrollPane(textArea);
        container.add(scrollPane);


        this.setBounds(100,100,300,350);
        this.setVisible(true);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new JScrollDemo();
    }
}

```

------



