elasticsearch 在Windows下的安装与启动

1、安装JDK，至少1.8.0_73以上版本，java -version

2、下载和解压缩Elasticsearch安装包，目录结构

​    官网下载地址：https://www.elastic.co/cn/downloads/

​    中文社区下载地址： https://elasticsearch.cn/download/ 

目录结构说明：

| 目录名称                 | 解释说明                                            |
| ------------------------ | --------------------------------------------------- |
| bin                      | 可执行的文件 elasticsearch.bat 、elasticsearch 启动 |
| config/elasticsearch.yml | es配置相关                                          |
| config/jvm.options       | jvm配置的相关参数                                   |
| config/log4j2.properties | 日志相关配置                                        |
| data                     | 存储数据相关                                        |
| modules                  | 模块相关                                            |
| plugins                  | 插件相关                                            |

3. elasticsearch.yml 配置说明

   cluster.name 集群名称，以此作为是否同一个集群的判断条件

   node.name: 节点名称，以此作为集群中不同节点的区分条件

   network.host:/http.port:  网络地址和端口，用于http 和transport服务使用；network.host:对外发布的网络地址; http.port: 对外提供API的端口

   path.data: 数据存储地址

   path.logs:日志存储地址

4. Elasticsearch的两种模式： Development 、Production 模式说明

   以transport的地址是否绑定在localhost为判断标准 network.host

   Development  模式下载启动时会议warning的方式提示配置检查异常

   Production 模式下载启动时会以error的方式提示配置检查异常并退出

   参数修改的第二种方式：

   elasticsearch  -Ehttp.port=9200

5. 解压并启动Elasticsearch：bin\elasticsearch.bat  从这里就是可以说是开箱即用

6. 检查ES是否启动成功：http://localhost:9200/?pretty

   ```json
   {
     "name" : "4onsTYV",
     "cluster_name" : "elasticsearch",
     "cluster_uuid" : "nKZ9VK_vQdSQ1J0Dx9gx1Q",
     "version" : {
       "number" : "5.2.0",
       "build_hash" : "24e05b9",
       "build_date" : "2017-01-24T19:52:35.800Z",
       "build_snapshot" : false,
       "lucene_version" : "6.4.0"
     },
     "tagline" : "You Know, for Search"
   }
   ```

   7. 下载和解压缩Kibana安装包，使用里面的开发界面

   8. 启动Kibana kibana.bat  <http://localhost:5801>

   9. 进入Dev Tools界面

   10. GET _cluster/health


​     