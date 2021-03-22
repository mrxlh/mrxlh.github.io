### springboot 集成 MinIo 文件服务器

#### 1.添加依赖

~~~java
dependency>
    <groupId>io.minio</groupId>
    <artifactId>minio</artifactId>
    <version>7.1.0</version>
</dependency>
~~~

#### 2. 集成springboot 并提供工具类

~~~java
package cn.com.taiji.util;

import io.minio.MinioClient;
import io.minio.ObjectStat;
import io.minio.PutObjectOptions;
import io.minio.Result;
import io.minio.messages.Bucket;
import io.minio.messages.Item;
import lombok.RequiredArgsConstructor;
import lombok.SneakyThrows;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import org.springframework.util.Assert;
import org.springframework.util.StringUtils;

import java.io.InputStream;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.Optional;

@Component
@RequiredArgsConstructor
public class MinioTemplate implements InitializingBean {
    /**
     * minio地址+端口号
     */
    @Value("${minio.url}")
    private  String url;
    /**
     * minio用户名
     */
    @Value("${minio.accessKey}")
    private  String accessKey;
    /**
     * minio密码
     */
    @Value("${minio.secretKey}")
    private  String secretKey;
    /**
     * 文件桶的名称
     */
    @Value("${minio.bucketName}")
    private String bucketName;

    private MinioClient minioClient;

    @Override
    public void afterPropertiesSet() throws Exception {
        Assert.hasText(url, "Minio url 为空");
        Assert.hasText(accessKey, "Minio accessKey为空");
        Assert.hasText(secretKey, "Minio secretKey为空");
        this.minioClient = new MinioClient(url, accessKey, secretKey);
    }

    /**
     * 创建bucket
     *
     * @param bucketName bucket名称
     */
    @SneakyThrows
    public void createBucket(String bucketName) {
        if (!minioClient.bucketExists(bucketName)) {
            minioClient.makeBucket(bucketName);
        }
    }

    /**
     * 获取全部bucket
     * <p>
     * https://docs.minio.io/cn/java-client-api-reference.html#listBuckets
     */
    @SneakyThrows
    public List<Bucket> getAllBuckets() {
        return minioClient.listBuckets();
    }

    /**
     * 根据bucketName获取信息
     *
     * @param bucketName bucket名称
     */
    @SneakyThrows
    public Optional<Bucket> getBucket(String bucketName) {
        return minioClient.listBuckets().stream().filter(b -> b.name().equals(bucketName)).findFirst();
    }

    /**
     * 根据bucketName删除信息
     *
     * @param bucketName bucket名称
     */
    @SneakyThrows
    public void removeBucket(String bucketName) {
        minioClient.removeBucket(bucketName);
    }

    /**
     * 根据文件前置查询文件
     *
     * @param bucketName bucket名称
     * @param prefix     前缀
     * @param recursive  是否递归查询
     * @return MinioItem 列表
     */
    @SneakyThrows
    public List getAllObjectsByPrefix(String bucketName, String prefix, boolean recursive) {
        List<Item> list = new ArrayList<>();
        Iterable<Result<Item>> objectsIterator = minioClient.listObjects(bucketName, prefix, recursive);
        if (objectsIterator != null) {
            Iterator<Result<Item>> iterator = objectsIterator.iterator();
            if (iterator != null) {
                while (iterator.hasNext()) {
                    Result<Item> result = iterator.next();
                    Item item = result.get();
                    list.add(item);
                }
            }
        }

        return list;
    }

    /**
     * 获取文件外链
     *
     * @param bucketName bucket名称
     * @param objectName 文件名称
     * @param expires    过期时间 <=7
     * @return url
     */
    @SneakyThrows
    public String getObjectURL(String bucketName, String objectName, Integer expires) {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        return minioClient.presignedGetObject(bucketName, objectName, expires);
    }

    /**
     * 获取文件路径
     * @param bucketName 
     * @param fileName
     * @return
     */
    @SneakyThrows
    public String getObjectURL(String bucketName, String fileName) {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        return minioClient.getObjectUrl(bucketName, fileName);
    }

    /**
     * 获取文件
     *
     * @param bucketName bucket名称
     * @param objectName 文件名称
     * @return 二进制流
     */
    @SneakyThrows
    public InputStream getObject(String bucketName, String objectName) {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        return minioClient.getObject(bucketName, objectName);
    }

    /**
     * 获取文件
     * @param bucketName
     * @param objectName
     * @return
     */
    @SneakyThrows
    public ObjectStat statObject(String bucketName, String objectName) {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        return minioClient.statObject(bucketName, objectName);
    }

    /**
     * 上传文件
     *
     * @param bucketName bucket名称
     * @param objectName 文件名称
     * @param stream     文件流
     * @throws Exception https://docs.minio.io/cn/java-client-api-reference.html#putObject
     */
    public void putObject(String bucketName, String objectName,InputStream stream,int length) throws Exception {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        minioClient.putObject(bucketName, objectName, stream, new PutObjectOptions(stream.available(), length));
        //minioClient.putObject(bucketName, objectName, stream, length,stream.available(), "application/octet-stream");
    }

    /**
     * 上传文件
     *
     * @param bucketName  bucket名称
     * @param objectName  文件名称
     * @param stream      文件流
     * @param size        大小
     * @throws Exception https://docs.minio.io/cn/java-client-api-reference.html#putObject
     */
    public void putObject(String bucketName, String objectName, InputStream stream, long size) throws Exception {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
       // client.putObject(bucketName, objectName, stream, size, contextType);
        minioClient.putObject(bucketName, objectName, stream, new PutObjectOptions(stream.available(), -1));
    }

    /**
     * 获取文件信息, 如果抛出异常则说明文件不存在
     *
     * @param bucketName bucket名称
     * @param objectName 文件名称
     * @throws Exception https://docs.minio.io/cn/java-client-api-reference.html#statObject
     */
    public ObjectStat getObjectInfo(String bucketName, String objectName) throws Exception {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        return minioClient.statObject(bucketName, objectName);
    }

    /**
     * 删除文件
     *
     * @param bucketName bucket名称
     * @param objectName 文件名称
     * @throws Exception https://docs.minio.io/cn/java-client-api-reference.html#removeObject
     */
    public void removeObject(String bucketName, String objectName) throws Exception {
        if (StringUtils.isEmpty(bucketName)) {
            bucketName = this.bucketName;
        }
        minioClient.removeObject(bucketName, objectName);
    }
}
~~~



#### 4. 配置信息

~~~Java
## minio文件系统
minio.url=http://10.0.26.51:9000
minio.accessKey=minioadmin
minio.secretKey=minioadmin
minio.bucketName=mhpt
~~~

#### 5. crud 示例

~~~~java
package cn.com.taiji.mhpt.modules.file.rest;

import cn.com.taiji.result.JsonResult;
import cn.com.taiji.sys.exception.BusinessException;
import cn.com.taiji.util.MinioTemplate;
import io.minio.ObjectStat;
import io.swagger.annotations.ApiOperation;
import lombok.SneakyThrows;
import org.apache.commons.io.IOUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;

import javax.servlet.http.HttpServletResponse;
import java.io.InputStream;
import java.net.URLEncoder;

/**
 * minio上传,下载,删除接口
 */
@RestController
@RequestMapping("/minio")
public class MinioController {


    @Autowired
    private MinioTemplate minioTemplate;

    /**
     * 下载文件
     */
    @ApiOperation(value = "下载文件")
    @GetMapping(value = "/download")
    @SneakyThrows(Exception.class)
    public void download(@RequestParam("fileName") String fileName, HttpServletResponse response) {
        ObjectStat stat = minioTemplate.statObject("", fileName);
        response.setContentType(stat.contentType());
        response.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode(fileName, "UTF-8"));
        InputStream in = minioTemplate.getObject("", fileName);
        IOUtils.copy(in, response.getOutputStream());
        in.close();
    }

    /**
     * 上传文件
     * @param file
     * @return
     * @throws Exception Exception
     */
    @ApiOperation(value = "上传文件")
    @PostMapping(value = "/upload")
    @SneakyThrows(Exception.class)
    public JsonResult upload(@RequestParam("file") MultipartFile file) throws Exception {
        if (file.isEmpty()) {
            throw new BusinessException("上传文件不能为空");
        } else {
            // 得到文件流
            final InputStream is = file.getInputStream();
            // 文件名
            final String fileName = file.getOriginalFilename();
            // 把文件放到minio的boots桶里面
            minioTemplate.putObject("",fileName,is,-1);
            String objectUrl = minioTemplate.getObjectURL("",fileName);
            // 关闭输入流
            is.close();
            return JsonResult.ok(objectUrl);
        }
    }

    /**
     * 删除文件
     * @author 溪云阁
     * @param fileName
     * @return JsonResult
     */
    @ApiOperation(value = "删除文件")
    @GetMapping(value = "/delete", produces = MediaType.APPLICATION_JSON_UTF8_VALUE)
    @SneakyThrows(Exception.class)
    public JsonResult delete(@RequestParam("fileName") String fileName) {
        minioTemplate.removeObject("",fileName);
        return JsonResult.ok("删除成功");
    }

}
~~~~

#### 6.MinIO dashboard 信息

~~~
1. 访问地址： http://10.0.26.51:9000/
2. 账户/密码： minioadmin/minioadmin
~~~

#### 7. 官网网址

~~~~
https://www.min.io/
~~~~

#### 8.参考文档

~~~
Go:         https://docs.min.io/docs/golang-client-quickstart-guide
Java:       https://docs.min.io/docs/java-client-quickstart-guide
Python:     https://docs.min.io/docs/python-client-quickstart-guide
JavaScript: https://docs.min.io/docs/javascript-client-quickstart-guide
.NET:       https://docs.min.io/docs/dotnet-client-quickstart-guide
~~~

