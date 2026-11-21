[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

# 文件存储 Spring Boot Starter

让 Spring Boot 应用快速集成文件存储，支持多种存储引擎。

## 快速开始

- 导入依赖

```xml
    <dependency>
        <groupId>com.jiovan.spring.starter</groupId>
        <artifactId>file-storage-spring-boot-starter</artifactId>
        <version>LATEST</version>
    </dependency>
```

> 默认情况下，此 starter 会自动生效，你可以通过 `jiovan.file-storage.enabled = false` 关闭它。

- 使用前缀 `jiovan.file-storage` 配置 Spring Boot 的 `application.yml`

```yml
jiovan:
    file-storage:
        concat-date: true
        storage-type: 'minio'
        local:
            entry-path: '/path/to/your/storage'
            domain: 'http://localhost:8090'
        minio:
            endpoint: 'localhost'
            port: 9000
            access-key: 'minio'
            secret-key: 'minio123'
            bucket-name: 'demo-bucket'
            access-control: 'public-read'
        aliyun:
            endpoint: 'https://oss-cn-beijing.aliyuncs.com'
            access-key: 'your-access-key'
            secret-key: 'your-secret-key'
            region: 'cn-beijing'
            bucket-name: 'demo-bucket'
            access-control: 'public-read'
        tencent:
            endpoint: 'https://cos.ap-beijing.myqcloud.com'
            secret-id: 'your-secret-id'
            secret-key: 'your-secret-key'
            region: 'ap-beijing'
            bucket-name: 'demo-bucket'
            access-control: 'public-read'
```

- 随后在代码中即可使用 `FileStorageComposer` 存取文件

```java
@Service
public class DemoService {
    @Autowired
    private FileStorageComposer storageComposer;

    public void demoMethod() {
        // Uploads a file, or a pure text, or a byte array, or an input stream
        storageComposer.uploadObject();

        // Checks if exist an object
        storageComposer.existsObject(objectKey, pathPrefix);

        // Downloads an object as an input stream
        storageComposer.downloadObject(objectKey, pathPrefix);

        // Downloads an object as a file
        storageComposer.downloadObjectTo(objectKey, pathPrefix, targetFile);

        // Removes an object
        storageComposer.removeObject(objectKey, pathPrefix);

        // Gets the object URL
        storageComposer.getObjectUrl(objectKey, pathPrefix);
        storageComposer.getObjectUrl(objectKey, pathPrefix, expiration);
        
        // Gets the raw client for advanced usage
        storageComposer.getRawClient();
        storageComposer.getRawClientAs(expectType);
    }
}
```

## 文档

- GitHub：https://github.com/jiovan-labs/file-storage-spring-boot-starter

## 环境要求

- jdk 17+

## 许可证

本项目采用 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) 许可证。

请参阅 `NOTICE.txt` 文件了解所需的声明与归属信息。

## 捐赠

喜欢这个工具包吗？欢迎[向我们捐赠](https://jiovan.com/donation)以支持开发。

## 版权

北京玖漫科技有限公司

## 网站

- 玖漫：https://jiovan.com
