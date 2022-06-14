# Windows 10 修改键盘键位映射

## 1.打开注册表编辑器:按下Win+R打开运行，输入regedit，点击确定。
## 2.创建映射文件:左侧目录树下定位到这个地方：

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout

注意，不要点进它的两个子文件夹里。右键点Keyboard Layout这个文件夹，选择新建二进制值。并且给建好的文件取名为Scancode Map
## 3.添加映射
打开Scancode Map文件，如下图：
![键盘映射图片Alt](../Img/KeyboardMapping01map.png "键盘映射操作文件设置")

先解释一下每一排的含义

0000	00 00 00 00 00 00 00 00	. . . . . . . .
相对地址	数据	每对数据所对应的ASCII字符
现在解释一下图中我所设置的含义：

前8组00是版本号和头部字节，不用动。

接下来4组表示映射数，如图所示，我填写为04 00 00 00。其中“04”表示有三组映射。
若要映射多组，只需增加相应的值即可，如映射2组为"03"，映射5组为"06"，其最小为值为“02”，表示只映射一组。

再后边每4组数据代表一个映射，每一个映射格式如下：A B
B映射为A，也就是说，我们按下B键，则相当于按下了原来的A键。

映射应该这么来：

    [Left Ctrl]  左大写[Caps Kock]
左侧大写锁定设置成Ctrl键
接下来，只要把对应键位码输进去就好了！注意：在注册表中输入时，需要将扫描码的高低字节交换一下。
通过查阅键位表，我得知：
    Left Ctrl 00 1D
    Caps Lock 00 3A
因此我把数值对填充进去，最后，以00 00 00 00结尾，就可以了，你可以去对照一下我的截图。

## 4.如何让某个键失效？
如果想要某个键失效，将它的扫描码映射为“00 00”即可。

## 5.如何撤销更改？
若要恢复键盘键位原来的布局，只需定位于注册表

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
删除"Scancode Map"键值就可以了

## 附录 键位表
```
Backspace 00 0E 
Caps Lock 00 3A 
Delete E0 53 
End E0 4F 
Enter 00 1C 
Escape 00 01 W
HOME E0 47 
Insert E0 52 
Left Alt 00 38 
Left Ctrl 00 1D 
Left Shift 00 2A 
Left Windows E0 5B 
Num Lock 00 45 
Page Down E0 51 
Page Up E0 49 
Power E0 5E 
PrtSc E0 37 
Right Alt E0 38 
Right Ctrl E0 1D 
Right Shift 00 36 
Right Windows E0 5C 
Scroll Lock 00 46 
Sleep E0 5F 
Space 00 39 
Tab 00 0F 
Wake E0 63 
0 00 52 
1 00 4F 
2 00 50 
3 00 51 
4 00 4B 
5 00 4C 
6 00 4D 
7 00 47 
8 00 48 
9 00 49 
- 00 4A 
/* 00 37 
. 00 53 
/ 00 35 
/+ 00 4E 
Enter E0 1C 
F1 00 3B 
F2 00 3C 
F3 00 3D 
F4 00 3E 
F5 00 3F 
F6 00 40 
F7 00 41 
F8 00 42 
F9 00 43 
F10 00 44 
F11 00 57 
F12 00 58 
F13 00 64 
F14 00 65 
F15 00 66 
Down E0 50 
Left E0 4B 
Right E0 4D 
Up E0 48 
Calculator E0 21 
E-Mail E0 6C 
Media Select E0 6D 
Messenger E0 11 
My Computer E0 6B 
’ ” 00 28 
- _ 00 0C 
, < 00 33 
. > 00 34 
/ ? 00 35 
; : 00 27 
[ { 00 1A 
\ | 00 2B 
] } 00 1B 
` ~ 00 29 
= + 00 0D 
0 ) 00 0B 
1 ! 00 02 
2 @ 00 03 
3 # 00 04 
4 $ 00 05 
5 % 00 06 
6 ^ 00 07 
7 & 00 08 
8 * 00 09 
9 ( 00 0A 
A 00 1E 
B 00 30 
C 00 2E 
D 00 20 
E 00 12 
F 00 21 
G 00 22 
H 00 23 
I 00 17 
J 00 24 
K 00 25 
L 00 26 
M 00 32 
N 00 31 
O 00 18 
P 00 19 
Q 00 10 
R 00 13 
S 00 1F 
T 00 14 
U 00 16 
V 00 2F 
W 00 11 
X 00 2D 
Y 00 15 
Z 00 2C 
Close E0 40 
Fwd E0 42 
Help E0 3B 
New E0 3E 
Office Home E0 3C 
Open E0 3F 
Print E0 58 
Redo E0 07 
Reply E0 41 
Save E0 57 
Send E0 43 
Spell E0 23 
Task Pane E0 3D 
Undo E0 08 
Mute E0 20 
Next Track E0 19 
Play/Pause E0 22 
Prev Track E0 10 
Stop E0 24 
Volume Down E0 2E 
Volume Up E0 30 
? - 00 7D 
E0 45 
Next to Enter E0 2B 
Next to L-Shift E0 56 
Next to R-Shift E0 73 
DBE_KATAKANA E0 70 
DBE_SBCSCHAR E0 77 
CONVERT E0 79 
NONCONVERT E0 7B 
Internet E0 01 
iTouch E0 13 
Shopping E0 04 
Webcam E0 12 
Back E0 6A 
Favorites E0 66 
Forward E0 69 
HOME E0 32 
Refresh E0 67 
Search E0 65 
Stop E0 68 
My Pictures E0 64 
My Music E0 3C 
Mute E0 20 
Play/Pause E0 22 
Stop E0 24 
+ (Volume up) E0 30 
- (Volume down) E0 2E 
Media E0 6D 
Mail E0 6C 
Web/Home E0 32 
Messenger E0 05 
Calculator E0 21 
Log Off E0 16 
Sleep E0 5F 
Help(on F1 key) E0 3B 
Undo(on F2 key) E0 08 
Redo(on F3 key) E0 07 
Fwd (on F8 key) E0 42 
Send(on F9 key) E0 43
```


# 参考

    https://blog.csdn.net/lhdalhd1996/article/details/90741092