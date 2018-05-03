# WireMock
WireMock API模拟工具

[WireMock - WireMock](http://wiremock.org/)


    模拟API以进行快速，可靠和全面的测试
    WireMock是一个基于HTTP的API的模拟器。一个服务虚拟化工具或模拟服务器。

##### 启动jar包命令
    
    cd/D/wireMock nohup java -Xms1024M -Xmx1024M -jar /D/wiremock/wiremock-standalone-2.17.0.jar  --port 9999 &

##### 目录说明

    程序启动后在同目录下生成两个空的文件夹：__files和mappings。
    __files是放上传/下载/录制文件用的。
    mappings放你想要的Service返回数据和Url mapping。

##### 例子
    在mappings文件夹下随便创建一个test.json文件
    (添加修改mapping文件需要重启程序或POST调用其接口/__admin/mappings/reset)
	
	{
    	"request": {
    	    "method": "GET",
    	    "urlPattern": "/mock_pass.*"
   		 },
    		"response": {
    	    "status": 200,
    	    "body": "{\"code\":1,\"msg\":\"ok\"}"
    		}
		}
	
	
	 打开浏览器，输入：http://127.0.0.1:9999/mock_pass
	 返回以下内容
	
	 {"code":1,"msg":"ok"}

##### 例子1
    {
    "request": {
	      "method" : "ANY",		
        "urlPath": "/utils_provider/dubbo",
        "queryParameters": {
            "funid": {
                "equalTo": "18"
            }
        }
    },    
    "response": {
        "status": 200,
        "bodyFileName":"funid-18.json"
    }
       }

##### 例子2
    {
    "request": {
	      "method" : "ANY",		
        "urlPath": "/utils_provider/dubbo",
        "queryParameters": {
            "funid": {
                "equalTo": "18"
            }
        }
    },    
    "response": {
        "status": 200,
        "jsonBody":{"status":"Error","message":"Endpoint not found"}
    }
       }

##### bodyFileName和jsonBody区别

    bodyFileName为存放响应数据的文件名，其为在__files里面建立的响应文件，一般功能测试时使用
    jsonBody就是响应的json数据，其数据会存放到内存里。为防止full gc，设置适当的年老代空间，一般压测时才使用。

##### 参考

    http://wiremock.org/docs/stubbing/
    http://wiremock.org/docs/request-matching/

##### Download

[jar下载](https://github.com/13570524658/WireMock/raw/master/wiremock-standalone-2.17.0.jar)
