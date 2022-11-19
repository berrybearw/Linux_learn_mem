# Linux_learn_mem
內存

參考 : 

* [https://www.itread01.com/content/1547590715.html](https://www.itread01.com/content/1547590715.html)

簡介 : 

* [https://binaryterms.com/swapping-in-operating-system.html](https://binaryterms.com/swapping-in-operating-system.html)

* http://blog.is36.com/tag/linux/

linux在終端環境下可以使用 free 命令看到系統實際使用內存的情況，

一般用free -m方式查看內存佔用情況（兆為單位）。

而系統實際可用內存是不是free部分呢，不是的，

系統實際內存佔用以及可用內存有如下幾個加減法：

- **used=total-free** 即 **total=used+free**
- 實際內存佔用：**used-buffers-cached** 即 **total-free-buffers-cached**
- 實際可用內存：**buffers+cached+free**

Linux 查看正在吃 swap 的程式
---

參考 : 

* [https://blog.longwin.com.tw/2017/02/linux-find-use-swap-process-2017/](https://blog.longwin.com.tw/2017/02/linux-find-use-swap-process-2017/)
* [https://www.cyberciti.biz/faq/linux-which-process-is-using-swap/](https://www.cyberciti.biz/faq/linux-which-process-is-using-swap/)

`ps -eo vsz,rss,pid,args | 排序 -n`

第一列是虛擬內存使用情況，也稱為交換，具體取決於您選擇的定義...

```bash
#一行查看方式
for file in /proc/*/status ; do awk '/VmSwap|Name/{printf $2 " " $3}END{ print ""}' $file; done | sort -k 2 -n -r | less
#pmap
pmap -x pid | tail -n 1 |awk '{print $5}'
```
