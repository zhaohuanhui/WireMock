# WireMock
WireMock API模拟工具  最高支持JDK 1.8版本

[WireMock](http://wiremock.org/)


    模拟API以进行快速，可靠和全面的测试
    WireMock是一个基于HTTP的API的模拟器。一个服务虚拟化工具或模拟服务器。

##### CD进入jar路径 （win）

    这里我以打开E:\homework\1.jpg来给大家做示范。在命令行中输入  E:  
    输入后按下enter键。就进入E盘中
    E:
    如果你想要查看E盘中的文件目录，只用继续输入dir 并且按enter键即显示E盘的文件夹和文件目录！
    dir
    我们现在要打开的是homework文件夹 故我们继续输入 cd homework 就可以了！但是要注意cd 之后有一个空格哟！
    同理我们如果需要查看homework中的目录继续输入dir即可
    现在我们要打开1.jpg这张图片我们只用继续输入文件名1.JPG输入后按回车键就可以打开

##### 启动jar包命令

    java -jar wiremock-standalone-2.17.0.jar  –port 9999 --verbose
      
##### 目录说明

    程序启动后在同目录下生成两个空的文件夹：__files和mappings。
    __files是放上传/下载/录制文件用的。mappings放你想要的Service返回数据和Url mapping。
    
##### 重启程序
     
      在mappings文件夹下随便创建一个test.json文件
     (添加修改mapping文件需要重启程序或POST调用其接口/__admin/mappings/reset)
      
      打开浏览器，输入：http://localhost:8080/__admin/mappings/reset

##### 测试例子

	{
		"request": {
			"method": "GET",
			"urlPattern": "/mock_pass.*"
		},
		"response": {
			"status": 200,
		        "fixedDelayMilliseconds": 2000
			 "headers": {
          		              "Content-Type": "application/json",
         		              "Cache-Control": "max-age=86400"
      				     }
			"body": "{\"code\":1,\"msg\":\"ok\"}"
		}
	}

	
	 打开浏览器，输入：http://localhost:8080/mock_pass
	 返回以下内容
	
	 {"code":1,"msg":"ok"}

##### 例子1
	{
		"request": {
			"method": "ANY",
			"urlPath": "/utils_provider/dubbo",
			"queryParameters": {
				"funid": {
					"equalTo": "18"
				}
			}
		},
		"response": {
			"status": 200,
			"bodyFileName": "funid-18.json"
		}
	}
	
	 打开浏览器，输入：http://localhost:8080/utils_provider/dubbo?funid=18
	 返回以下内容
	
		{
	          "status": "Error",
	          "message": "Endpoint not found"
	        }

##### 例子2
	{
		"request": {
			"method": "ANY",
			"urlPath": "/utils_provider/dubbo",
			"queryParameters": {
				"funid": {
					"equalTo": "18"
				}
			}
		},
		"response": {
			"status": 200,
			"jsonBody": {
				"status": "Error",
				"message": "Endpoint not found"
			}
		}
	}
	
		 打开浏览器，输入：http://localhost:8080/utils_provider/dubbo?funid=18
	         返回以下内容
	
		{
	          "status": "Error",
	          "message": "Endpoint not found"
	        }

##### bodyFileName和jsonBody区别

    bodyFileName为存放响应数据的文件名，其为在__files里面建立的响应文件，一般功能测试时使用
    jsonBody就是响应的json数据，其数据会存放到内存里。为防止full gc，设置适当的年老代空间，一般压测时才使用。

##### 参考

    http://wiremock.org/docs/stubbing/
    http://wiremock.org/docs/request-matching/

##### Download

[wiremock-standalone-2.17.0.jar下载](https://github.com/13570524658/WireMock/raw/master/wiremock-standalone-2.17.0.jar)

http://wiremock.org/docs/running-standalone/
