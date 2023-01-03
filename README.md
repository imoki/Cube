# 光立方
光立方取模程序，适用于8*8*8的光立方动画设计

## 使用说明  
1. 鼠标移动到led上方会显示坐标信息，点击则点亮led。  
按钮旁边的字母代表快捷键，如拍摄(S),则"拍摄"的快捷键为Ctrl+S  
![6bd122616a600af901b1e958b72d1fb](https://user-images.githubusercontent.com/78804251/210315698-a002c113-c7b4-43d9-9ba0-1c87a31d7d27.png)  
2. 选择完后，点击“拍摄”按钮，即可记录此时坐标信息。  
3. 点击“清屏”可熄灭所有led。重复1和2步骤，直至制作完所有动画。  
4. 点击“导出”，动画坐标会被保存再“cube”目录下的“output.txt”文件中。

## 坐标格式来源参考
8阶光立方，采用扩散型LED（不是透明型LED）  
立方体由下至上，分为8片（行），每片64个（列）  
行共阴极，列共阳极  
8行用1个74hc595（8个并行输出端口），64列用8个74hc595  
  
给74hc595顺序编号（从0开始编号）：  
由下至上，分别是第0-7片（端口用Q0-Q7）用一个74hc595（8号74hc595）。  
以第0片的俯视图为例,这一片有64个LED  
采用笛卡尔坐标表示法。000为坐标原点（x,y,z）,用三个数字表示某个LED（例如：000，表示第0行,第0个LED,第0片）  
最上面为第0行，8个LED（为第000-070LED），用一个74hc595（0号）  
第1行（100-170LED），用一个74hc595（1号）  
以此类推。  
最后一行（第7行，700-770LED），用一个74hc595（7号）  
  
需要9个字节，依次为8-0号74hc595(8-0号字节)采用，先送高位再送低位。因为这样符合书写习惯  
8号字节控制片，7-0号字节分别代表7-0行，其某一字节的某个为第某个LED  
每一字节分别位Q7-Q0  
例如让坐标000亮，则给z为低电平0，x和y为高电平1。其余相反  
11111110 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000001  
用16进制表示：FE 00 00 00 00 00 00 00 01  
例如让235亮，第2行，第3个，第5片  
11011111 00000000 00000000 00000000 00000000 00000000 00001000 00000000 00000000  
  
最后将这一串二进制转为十六进制即可。  
取模软件中用逗号将每组十六进制进行分隔，以便其他程序接入使用。  
