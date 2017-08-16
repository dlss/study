# for 语法：

在cmd 窗口中：for %I in (command1) do command2   
在批处理文件中：for %%I in (command1) do command2 

1. for、in 和do 是  for 语句的关键字，它们三个缺一不可； 
2. %%I 是for 语句中对形式变量的引用，就算它在do 后的语句中没有参与语句的执行，也是必须出现的； 
3. in 之后，do 之前的括号不能省略； 
4. command1 表示字符串或变量，command2 表示字符串、变量或命令语句； 
5. for 后 可以 加 /f /r /l /d 这四个参数

## /d 参数
### 格式：
FOR /D %%variable IN (set) DO command [command-parameters]   
### 说明：
用于搜索**目录或文件夹**，但不会搜索文件，搜索的仅仅是指定目录第一层目录，而不是整个目录树；

### demo：
:: 把C盘下所有子文件夹打出来  
>for /d %%i in (c:\\*) do echo %%i

:: 把当前路径下所有子文件夹打出来  
>for /d %%i in (*) do echo %%i

:: 把当前路径下文件夹的名字只有1-6个字母的打出来  
>for /d %%i in (??????) do echo %%i

:: 把C盘下以win开头的文件夹打出来  
>for /d %%i in (c:\win*) do echo %%i

## /r 参数
### 格式：
FOR /R [[drive:]path] %%variable IN (set) DO command [command-parameters]    
### 说明：
他可以把当前或者你指定路径下的**文件名字**全部读取出来,注意是文件名字，不是文件目录名字。      
检查以 [drive:]path 为根的**目录树**，如果在 /R 后没有指定目录，则使用当前目录。     
如果集仅为一个单点(.)字符，则枚举该目录树，而不是文件。   

### demo：
:: 把C:\Windows\System32下所有文件打印出来
>for /r C:\Windows\System32 %%i in (*) do echo %%i

:: 把C:\Windows\System32下所有exe文件打印出来
>for /r C:\Windows\System32 %%i in (*.exe) do echo %%i

:: 把C:\Windows\System32路径下文件的字只有1-3个字母的exe文件打印出来
>for /r C:\Windows\System32 %%i in (???.exe) do echo %%i

:: 把C:\Windows\System32路径下sfc.exe文件打印出来
>for /r C:\Windows\System32 %%i in (sfc.exe) do echo %%i

:: 把C:\Windows\System32整个目录树结构打印出来
>for /r C:\Windows\System32 %%i in (.) do echo %%i

## /l 参数
### 格式：
for /L %variable IN (start,step,end) DO command [command-parameters]  
for /L %variable IN (start,step,end) DO command [command-parameters]     
for /L %variable IN (start,step,end) DO command [command-parameters]     
for /L %variable IN (start,step,end) DO command [command-parameters]    

### 说明：
该集表示以增量形式从开始到结束的一个数字序列。可以使用负的 Step 

#### demo： 
　　for /l %%i in (1,1,5) do @echo %%i --输出1 2 3 4 5    
　　for /l %%i in (1,2,10) do @echo %%i --输出1,3，5,7，9    
　　for /l %%i in (100,-20,1) do @echo %%i --输出100,80,60,40,20    
　　for /l %%i in (1,1,5) do start cmd --打开5个CMD窗口    
　　for /l %%i in (1,1,5) do md %%i --建立从1~5共5个文件夹    
　　for /l %%i in (1,1,5) do rd /q %%i --删除从1~5共5个文件夹   

## /f 参数
### 格式：
FOR /F ["options"] %%variable IN (file-set) DO command [command-parameters]   
FOR /F ["options"] %%variable IN ("string") DO command [command-parameters]   
FOR /F ["options"] %%variable IN ('command') DO command [command-parameters]   
### 说明：
为解析文本而生,提取文本信息,语句是以行为单位处理文本文件的

带引号的字符串"options"包括一个或多个指定不同解析选项的关键字。这些关键字为:

        eol=c           - 指一个行注释字符的结尾(就一个)
        skip=n          - 指在文件开始时忽略的行数。
        delims=xxx      - 指分隔符集。这个替换了空格和跳格键的默认分隔符集。
        tokens=x,y,m-n  - 指每行的哪一个符号被传递到每个迭代的 for 本身。这会导致额外变量名称的分配。m-n格式为一个范围。通过 nth 符号指定 mth。    如果符号字符串中的最后一个字符星号，那么额外的变量将在最后一个符号解析之后分配并接受行的保留文本。经测试，该参数最多只能区分31个字段。

        usebackq        - 使用后引号（键盘上数字1左面的那个键`）。
                        未使用参数usebackq时：file-set表示文件，但不能含有空格
                            双引号表示字符串，即"string"
                            单引号表示执行命令，即'command'
                          使用参数usebackq时：file-set和"file-set"都表示文件
                          当文件路径或名称中有空格时，就可以用双引号括起来
                            单引号表示字符串，即'string'
                            后引号表示命令执行，即`command`

### demo：
**test.bat**
>@echo off  
>
>for /f "eol=# delims=, tokens=1-3" %%i in (%~dp0test.txt) do (  
>	if NOT "%%j"=="azure-docs-pr.cs-cz" (  
>		echo rebase.bat "%%i\%%j" "%%k"  
>	)  
>)  

**test.txt**
>\# PPE   
>OPS-E2E-PPE,azure-docs-pr,https://github.com/OPS-E2E-PPE/azure-docs-pr.git  
>OPS-E2E-PPE,azure-docs-pr.cs-cz,https://github.com/OPS-E2E-PPE/azure-docs-pr.cs-cz.git  
>OPS-E2E-PPE,azure-docs-cli-python,https://github.com/OPS-E2E-PPE/azure-docs-cli-python.git  
>
>\# PROD  
>\# OPS-E2E-PROD,azure-docs-pr,https://github.com/OPS-E2E-PROD/azure-docs-pr.git  
>\# OPS-E2E-PROD,azure-docs-pr.cs-cz,https://github.com/OPS-E2E-PROD/azure-docs-pr.cs-cz.git  
>OPS-E2E-PROD,azure-docs-cli-python,https://github.com/OPS-E2E-PROD/azure-docs-cli-python.git

**output**
>rebase.bat "OPS-E2E-PPE\azure-docs-pr" "https://github.com/OPS-E2E-PPE/azure-docs-pr.git"  
>rebase.bat "OPS-E2E-PPE\azure-docs-cli-python" "https://github.com/OPS-E2E-PPE/azure-docs-cli-python.git"  
>rebase.bat "OPS-E2E-PRO\Dazure-docs-cli-python" "https://github.com/OPS-E2E-PROD/azure-docs-cli-python.git"  

**reference:  
http://club.topsage.com/thread-597580-1-1.html   
http://blog.csdn.net/wh_19910525/article/details/7912440**
