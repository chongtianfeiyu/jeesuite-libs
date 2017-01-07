文件系统服务目前支持七牛和fastDFS集成，提供了工厂模式和spring注入两种集成方式。
#### 工厂模式
##### 配置文件,xx.properties

```
fs.groupNames=group1,group2
# 服务提供者可选值（fastDFS，qiniu）
fs.group1.provider=qiniu
fs.group1.accessKey=iqq3aa-ncqfdGGubCcS-N8EUV-qale2ezndnrtKS
fs.group1.secretKey=1RmdaMVjrjXkyRVPOmyMa6BzcdG5VDdF-SH_HUTe
fs.group1.urlprefix=http://7xq7jj.com1.z0.glb.clouddn.com
# group2 配置
fs.group2.provider=fastDFS
fs.group2.servers=192.168.1.101:22122,192.168.1.102:22122
.....
fs.group2.connectTimeout=3000
fs.group2.maxThreads=100
......
```

参数说明：
- groupNames：多个组用“,”隔开，对应七牛的bucketName
##### 用法

```
FSProvider provider = FSClientFactory.build("qiniu", "group1");
String url = provider.upload("test", null, new File("/Users/vakinge/logo.gif"));
```

spring方式

```
<bean id="jedisPoolConfig" class="com.jeesuite.filesystem.spring.FSProviderSpringFacade">
		<property name="provider" value="qiniu" />
		<property name="groupName" value="group1" />
		<property name="accessKey" value="xxxxx-xxxx-xxx" />
		<property name="secretKey" value="xxxxx-xxxx-xxx" />
		<property name="urlprefix" value="http://www.jeesuite.com/pic" />
	</bean>
```
##### 用法

```
@Autowired
FSProviderSpringFacade provider;
String url = provider.upload("test", null, new File("/Users/vakinge/logo.gif"));
```