#ART使用

* USB数据线接ART板子的USB Slave
* 按住DFU按钮，按下RESET按钮，松开RESET按钮 ==> ART进入DFU模式
* 烧录完成，按RESET复位

#ART代码

* RT-Threaad: http://code.google.com/p/rt-thread/
* ART: https://github.com/RT-Thread/ART

#安装工具

* svn: sudo apt-get install subversion
* git: sudo apt-get install git
* python: sudo apt-get install python
* scons: sudo apt-get install scons
* arm-linux-gnu tools: https://sourcery.mentor.com
* dfu-util: http://dfu-util.gnumonks.org/ (0.6以上)

#编译烧录:

* git clone git://github.com/RT-Thread/ART.git
* cd ART/software/platform/
* vi rtconfig.py
	* CROSS_TOOL = 'gcc'
	* EXEC_PATH = '/usr/local/arm/arm-2011.09/bin/'
* scons -j4
* dfu-util -l
* sudo dfu-util -d 0483:df11 -a 0 -R -s 0x08000000 -D rtthread.bin
* alias sudo='sudo env PATH=$PATH'(IDE)
* sudo apt-get install socat 
* cd ART/ide/build/
* ant;ant run
* 程序位置:
	* rtthread.bin ART/software/platform/
	* root.bin ART/ide/build/linux/work/hardware/ART/ 
* IDE编译下载
	* sudo ./linux/work/arduino
* 命令编译下载
	* cd ART/ide/build/linux/work/hardware/ART/examples
	* scons --app=blink (root目录下生产blink.mo应用程序文件)
	* python mkromfs.py --binary --addr 0x08080000 root
	* sudo dfu-util -d 0483:df11 -a 0 -R -s 0x08080000 -D root.bin
* RT-thread启动后，自动执行/init.rc 脚本，这个脚本finsh shell执行.
* finsh />exec(“blink.mo”)
* finsh />list()
	*可以使用finsh中的函数直接操作硬件：pinMode(13, 1) --> digitalWrite(13, 1) --> digitalWrite(13, 0)

*问题:

	* 先按住DFU键，然后再插USB线，按RESET键。dfu-util -l 查看ART是否进入DFU模式，是否有DFU设备 (OK)
	* 使用非root用户，IDE可以编译程序，但不能下载,dfu-util需要root权限，使用root运行IDE，有工具栏路径无法找到的问题 (OK)
	* 虚拟串口无法链接(/dev/ttyACM0) (OK) 
	* 自己编译的rtthread.bin下载(ART/software/platform/ --OK)，sys灯没反应；编译下载的root.bin没反应

#例程代码
	* adk
	* blink
	* c++
	* hello
	* serial

###RT-Thread 代码：

	* 环境: ubuntu 12.04 arm-none-eabi-gnu(2011.09)
	* scons 组织管理代码
	* rt-thread/tools/building.py

	* rt-thread/
	├── AUTHORS
	├── bsp
	├── components
	├── COPYING
	├── documentation
	├── examples
	├── include
	├── libcpu
	├── README
	├── src
	└── tools

	* rt-thread/components/
	├── CMSIS
	├── dfs
	├── drivers
	├── external
	├── finsh
	├── init
	├── libc
	├── libdl
	├── net
	├── pthreads
	├── rtgui
	├── SConscript
	└── utilities

	* rt-thread/components/external/
	├── cairo
	├── freetype
	├── ftk
	├── jpeg
	├── libpng
	├── libz
	├── lua
	├── lzo
	├── pixman
	├── SConscript
	└── tjpgd1a

	* rt-thread Conf:
	./rt-thread/src/SConscript
	./rt-thread/libcpu/SConscript
	./rt-thread/components/*/SConscript

	* rt-thread/bsp/stm32f40x/
	├── applications
	├── build
	├── dfu.sh
	├── drivers
	├── Libraries
	├── readme.txt
	├── rtconfig.h
	├── rtconfig.py
	├── rtthread-stm32.map
	├── SConscript
	├── SConstruct
	├── stm32_rom.ld

	* stm32f40x Conf:
	./stm32f40x/SConstruct
	./stm32f40x/Libraries/SConscript
	./stm32f40x/applications/SConscript
	./stm32f40x/drivers/SConscript
	./stm32f40x/SConscript

	* rt-thread.bin 编译及链接:
	
	* rt-thread/bsp/stm32f40x/rtconfig.h: 配置头文件:

	* rt-thread 启动过程:

	* rt-thread GNU GCC 移植:

	* rt-thread 特性:
		* 线程调度
		* 线程同步与通信
		* 内存管理
		* 异常与中断
		* 定时器
		* I/O设备管理
		* FinSH Shell
		* 文件系统
		* Lwip协议
		* RTGUI










