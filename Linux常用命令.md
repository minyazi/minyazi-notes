# <a name="top">Linux常用命令</a>
* [一、Linux如何重启网络？](#anchor1)
* [二、rcp](#anchor2)
* [三、scp](#anchor3)
* [四、其他](#anchor4)

## <a name="anchor1">一、Linux如何重启网络？</a>[【TOP】](#top)
```
RedHat：
（方式一）service network restart
（方式二）/etc/rc.d/init.d/network restart
SUSE：
（方式一）service network restart
（方式二）rcnetwork restart
（方式三）/etc/rc.d/network restart
```

## <a name="anchor2">二、rcp</a>[【TOP】](#top)
```
remote file copy，远程文件拷贝

```

## <a name="anchor3">三、scp</a>[【TOP】](#top)
```
secure copy，安全拷贝

```

## <a name="anchor4">四、其他</a>[【TOP】](#top)
```
ls -l > test.txt                     ->   不保留test.txt文件的内容，将命令执行结果输出到test.txt文件中，终端不显示执行结果
ls -l >> test.txt                    ->   保留test.txt文件的内容，将命令执行结果输出到test.txt文件中，终端不显示执行结果
ls -l | tee test.txt                 ->   不保留test.txt文件的内容，将命令执行结果输出到test.txt文件中，终端显示执行结果
ls -l | tee -a test.txt              ->   保留test.txt文件的内容，将命令执行结果输出到test.txt文件中，终端显示执行结果
find . -name test.txt                ->   在当前目录及其子目录下查找test.txt文件
grep test *                          ->   在当前目录下的所有文件中查找test字符串
grep -r test *                       ->   在当前目录及其子目录下的所有文件中查找test字符串
ls -lt                               ->   按时间排序，降序
ls -ltr                              ->   按时间排序，升序
ls -lS 或 ls -l --sort=size          ->   按大小排序，降序
ls -lSr 或 ls -lr --sort=size        ->   按大小排序，升序
ls -lX 或 ls -l --sort=extension     ->   按扩展名排序，降序
ls -lXr 或 ls -lr --sort=extension   ->   按扩展名排序，升序
```
