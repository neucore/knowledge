安装
拷贝neulink.jar 放到 app/libs目录下

集成
在AndroidManifest.xml中添加下列内容
<!-- Mqtt Service -->
<service android:name="org.eclipse.paho.android.service.MqttService" />
<!-- Log Service -->
<service android:name="com.neucore.neulink.impl.LogService" />
代码集成
实现一个XXXApplication extends android.app.Application
在XXXApplication的onCreate()方法内添加如下代码
参考 MyApplication.java


/**
* 用户人脸数据库服务;必须实现IUserService接口
  */
  IUserService service = UserService.getInstance(this);
  /**
* 集成Neulink
  */
  SampleConnector register = new SampleConnector(this,callback,service);
  配置文件【neuconfig.properties】
  SD卡启用时位置
  Context.getExternalFilesDir()/neucore/config/neuconfig.properties

SD卡没有启用时位置
Context.getFilesDir()/neucore/config/neuconfig.properties

配置文件内容介绍
#MQTT-Server配置项变更之后应用需要重新启动
#测试环境tcp://10.18.9.99:1883
#生产环境tcp://10.18.105.254

MQTT-Server=tcp://10.18.9.99:1883

#下列配置项不需要启动即能生效【目前只实现了OSS】
Storage.Type=OSS
#################################################
#OSS配置项
OSS.EndPoint=https://oss-cn-shanghai.aliyuncs.com
OSS.BucketName=neudevice
OSS.AccessKeyID=LTAI4G6ZyiqBdrY9HA1Np6To
OSS.AccessKeySecret=fJPkLrpdMRIEB6BxdwbpD1xJsivC9h
#################################################
AWS.BucketName=
AWS.KeyName=
AWS.FilePath=
#################################################
FTP.Server=ftp://10.18.105.254:21
FTP.BucketName=ftproot
FTP.UserName=neu2ftp
FTP.Password=123456
#################################################
Topic.Partition=8
Log.Level=W
扩展实现
人脸同步；参考下列代码SampleFaceListener.java

图片上传【OSS｜FTP】&& 人脸上报
人脸上报参考下列代码SampleFaceUpload.java

参考代码
详见http://github.com/neucore/neucore_test_live/
