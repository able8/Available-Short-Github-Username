# Available-Short-Github-Username

分享几千个3位长度的 Github 用户名，大家可以挑选中意的名字注册！

### 起因:

- 为了找到简短可用的 Github 用户名

### 原理：

- 一般情况下
- 如果用户名存在，则访问 `https://github.com/Userame` 返回 200
- 如果返回是 `404 Not Found` ，则这个用户名 **很可能** 没被注册

### 实现

- `curl -sI "https://github.com/$Name" | grep  -q "404 Not Found" && echo $Name >> ok.txt`
- `-I`,  表示仅获取网页头部，大大减少数据量。Fetch the headers only!

### 注意
- txt文件里是1.1w个用户名，但大概测试发现只有一半左右是可以使用的！

### 脚本摘要

```bash
for i in 1 2 3 4 5 6 7 8 9 0 a b c d e f g h i j k l m n o p q r s t u v w x y z
do
    for j in 1 2 3 4 5 6 7 8 9 0 a b c d e f g h i j k l m n o p q r s t u v w x y z
    do
        for m in 1 2 3 4 5 6 7 8 9 0 a b c d e f g h i j k l m n o p q r s t u v w x y z
        do
            echo $i$j$m >> aaa.txt
        done
    done
done



# 并发设置
Command="curl -s" # 待检测的进程的 关键字
MaxBingFaNum=100
SleepTime=3  # 检测进程数量的时间间隔
DownloadCount="1"
for Name in $(cat aaa.txt)
do
    DownloadCount=$((++DownloadCount))
    {
        curl -sI "https://github.com/$Name" | grep  -q "404 Not Found" && echo $Name >> ok.txt
    } &

    CurrentBingFaNum=$(ps -ef|grep "${Command}"|grep -v grep|wc -l|tr -d ' ')
    #echo 进行中的任务数: "${CurrentBingFaNum}"
    echo ${DownloadCount}
    while [ "${CurrentBingFaNum}" -gt "${MaxBingFaNum}" ]
    do
        echo -n .
        sleep ${SleepTime}
        CurrentBingFaNum=$(ps -ef|grep "${Command}"|grep -v grep|wc -l|tr -d ' ')
    done
done
```