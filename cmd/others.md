# date & time

## demo:
**test.bat**
>@echo off  
echo %date% %time%  
:: yyyy          MM          dd           HH          mm          ss  
echo %date:~4,2% %date:~7,2% %date:~10,4% %time:~0,2% %time:~3,2% %time:~6,2%  
>
>if %TIME:~0,2% leq 9 (set b=0%TIME:~1,1%)else set b=%TIME:~0,2%  
set appendfix=%date:~10,4%%date:~4,2%%date:~7,2%%b%%time:~3,2%%time:~6,2%  
echo %appendfix%  

**output**
>Wed 08/16/2017 16:31:25.12  
08 16 2017 16 31 25  
20170816163125  

## Reference:
http://blog.csdn.net/zzm628/article/details/51668906
