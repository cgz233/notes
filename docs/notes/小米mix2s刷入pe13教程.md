# 小米mix2s刷入pe13教程

## 准备工作

1. 首先需要拥有一部小米mix2s，一台装有Windows的电脑
2. 下载pe13卡刷包和rec：https://download.pixelexperience.org/polaris/
3. 解bl锁：http://www.miui.com/unlock/index.html
4. 在电脑上安装adb和fastboot驱动，也可以使用wzsx150大佬的adb和fastboot工具：https://wwxg.lanzoub.com/iiAVj0mopgng

## 开始刷机

1. 长按电源键和音量减进入fastboot模式，并连接电脑

2. 打开adb和fastboot工具，输入`fastboot flash recovery pe的rec路径`

   <img src="https://pb.nichi.co/youth-grow-vacuum" style="zoom: 33%;" /> 

3. 长按电源键和音量加进入recovery模式

4. 等待出现界面

   <img src="https://pb.nichi.co/weapon-marriage-again" style="zoom: 15%;" /> 

5. 依次点击Factory reset -> Format data/factory reset -> Format data 格式化data分区

6. 成功后返回主界面

7. 然后依次点击Apply update -> Apply from ADB ，然后连接电脑打开adb和fastboot工具，输入指令`adb sideload 卡刷包路径`

   <img src="https://pb.nichi.co/math-valve-ready" style="zoom:33%;" /> 

8. 等待成功后开机即可

