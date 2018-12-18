# N76E003
NUVOTON's N76E003
一、准备工作：

| 硬件      | 软件 |
| --------- | -----:|
| 电脑  | WIN10/LINUX|
| NU-LINK下载器     |  Keil_C51 |
| N76E003开发板      |    N76E003_BSP_Keil_C51 |
| 杜邦线     |      |

----

二、开发环境搭建

| 安装      | 
| --------- | 
| 1、安装keil_c51 | 
| 2、安装N76E003_keil支持包N76E003_BSP_Keil_C51     |
| 3、上一步中选择安装Nu-link驱动，N76E003使用Nu-link下载固件。     |  
    
三、创建N76E003工程
1、准备工作，创建相关文件夹，新建文件夹 N76E003_Template ：放置工程所有文件，在N76E003_Template中新建文件夹 FwLib、Project 、User 和 文本文件README.txt
FwLib：放BSP中提供的文件
Project ：该文件夹用于创建工程
User ：放我们自己创建的文件
README.txt ：用于记录工程信息，例如版本、修改记录等，也可以不用
在User 中新建文件夹 inc、src：
inc ：头文件
src : 	.c文件
2、复制BSP中的Common、Include、Startup文件夹到FwLib文件夹中
3、打开keil，创建新工程
4、选择将工程创建在Project 文件夹中
5、选择device，选择N76E003，
点“OK”会弹出一下的框，我们选择“否”
6、在\N76E003_Template\User\src中创建main.c文件
7、将文件加入我们的工程中去，右键点击Target1，选择Manage Components
8、Project Targets一栏，我们将Target名字修改为N76E003_Template,然后在Groups一栏删掉一个，建立三个Groups：Startup,User,Common.
9、往Group里面添加我们需要的文件，选择需要添加文件的Group，这里第一步我们选择Startup，然后点击右边的Add Files,定位到我们刚才建立的目录\N76E003_Template\FwLib\Startup下面，选择需要的文件，然后点击Add，然后Close.可以看到Files列表下面包含我们添加的文件。
其他Groups添加方法一样，添加完成后最后点击OK，回到工程主界面。添加文件。
10、点击魔术棒
出来一个菜单，然后点击 C51选项.然后点击Include Paths右边的按钮。弹出一个添加path的对话框，然后我们将图上面的2个目录添加进去。记住，keil只会在一级目录查找，所以如果你的目录下面还有子目录，记得path一定要定位到最后一级子目录。然后点击OK.
11、设置时钟宏定义，我们使用内部16MHz，所以需要填写
12、配置Output选项。如下图。
13、配置Debug选项。定位到Debug界面，，勾选Use、选择nuvoton 8051 keil c51 driver。
14、配置Utilities选项。点击“OK”完成所有配置，回到主界面
15、main.c中编写简单main函数，实现led闪烁

    
    #include "N76E003.h"
	#include "SFR_Macro.h"
	#include "Function_define.h"
	#include "Common.h"
	#include "Delay.h"
 
	void main (void) 
	{
		Set_All_GPIO_Quasi_Mode;					// Define in Function_define.h
	
 	 while(1)
  	{
			clr_GPIO1;											// Tiny board GPIO1 LED 	define
		Timer0_Delay1ms(300);
		set_GPIO1;	
		Timer0_Delay1ms(300);
	  }
	}  
    

16、进行编译，编译完成，无错误。
17、下载固件
18、开发板led正常闪烁
