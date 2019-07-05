## HTML5 Plus



* B/S  

  一个普通的Web项目，通过浏览器访问资源，不可脱线运行，不能调用HTMLPlus的增加的API。

* C/S 

  它的程序要安装和运行在手机上，不通过浏览器在线下载。在App项目下编写的HTML、js等文件，是会被打包到原生的安装包（Android是apk包、iOS是ipa包）里的。

调用手机端 需要安装手机基座 xcode

#### Api

打开链接：plus.webview.create('url', 'style').show()

打开相机：puls.camera.getCamera('1','2')  1代表主摄像头，2代表副摄像头

获取文件：IO 模块里面的 plus.io.resolveLocalFileSystemURL()

推送：push

地图：maps

支付：payment

