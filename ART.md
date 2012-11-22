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

#烧录:

* vi rt-thread/bsp/stm32f40x/rtconfig.py
	* CROSS_TOOL = 'gcc'
	* EXEC_PATH = '/usr/local/arm/arm-2011.09/bin/'
* scons -j4
* dfu-util -l
* dfu-util -d 0483:df11 -a 0 -R -s 0x08000000 -D rtthread.bin

#例程代码


