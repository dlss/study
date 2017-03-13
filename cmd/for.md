## 格式1：FOR /L %variable IN (start,step,end) DO command [command-parameters]   

## 格式2：FOR /L %variable IN (start,step,end) DO command [command-parameters]    

## 格式3：FOR /L %variable IN (start,step,end) DO command [command-parameters]    

## 格式4：FOR /L %variable IN (start,step,end) DO command [command-parameters]    
该集表示以增量形式从开始到结束的一个数字序列。可以使用负的 Step 
### 示例： 
　　for /l %%i in (1,1,5) do @echo %%i --输出1 2 3 4 5    
　　for /l %%i in (1,2,10) do @echo %%i --输出1,3，5,7，9    
　　for /l %%i in (100,-20,1) do @echo %%i --输出100,80,60,40,20    
　　for /l %%i in (1,1,5) do start cmd --打开5个CMD窗口    
　　for /l %%i in (1,1,5) do md %%i --建立从1~5共5个文件夹    
　　for /l %%i in (1,1,5) do rd /q %%i --删除从1~5共5个文件夹   
  
  
  reference: http://blog.csdn.net/wh_19910525/article/details/7912440
