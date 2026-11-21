[English](README.md) | [簡體中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

# 檔案儲存 Spring Boot Starter

讓 Spring Boot 應用快速整合檔案儲存，支援多種儲存引擎。

## 快速開始

- 匯入相依性

```xml
    <dependency>
        <groupId>com.jiovan.spring.starter</groupId>
        <artifactId>file-storage-spring-boot-starter</artifactId>
        <version>LATEST</version>
    </dependency>
```

> 預設情況下，此 starter 會自動生效，你可以透過 `jiovan.file-storage.enabled = false` 關閉它。

- 使用字首 `jiovan.file-storage` 設定 Spring Boot 的 `application.yml`

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

- 隨後在程式碼中即可使用 `FileStorageComposer` 存取檔案

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

## 文件

- GitHub：https://github.com/jiovan-labs/file-storage-spring-boot-starter

## 環境要求

- jdk 17+

## 許可證

本專案採用 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) 許可證。

請參閱 `NOTICE.txt` 檔案瞭解所需的宣告與歸屬資訊。

## 捐贈

喜歡這個工具包嗎？歡迎[向我們捐贈](https://jiovan.com/donation)以支援開發。

## 版權

北京玖漫科技有限公司

## 網站

- 玖漫：https://jiovan.com
