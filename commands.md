运行代码命令：

输出报错信息：

nohup python -u ./test.py > output.log 2>&1 &

不输出错误信息：

nohup python -u ./test.py > output.log &

查看当前进程：

ps -ef | grep NGCF

查看所有进程：

ps -ef

查看log：

cat output.log

杀死进程：

kill -9 进程号

nohup python -u ./runRL.py > output.log 2>&1 &