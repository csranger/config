# config server 项目：统一配置中心
## 使用 spring cloud config
1. 两个组件构成：config server + config client
2. 新建项目是需要添加 Eureka Server 依赖和 Config Server 依赖
3. 为什么使用 spring cloud config 统一配置中心？
    - 更加方便维护
    - 配置内容更加安全，账号密码不放到order，product等项目里
    - 更新配置不需要重启项目
4. 注册到 eureka server
    - 作为服务在启动项加上 @EnableDiscoveryClient 注解
    - application.properties 也需要添加上 eureka server 配置:eureka.client.service-url.defaultZone=http://localhost:8761/eureka/
5. 为使此服务成为 config server 端
    - 在在启动项加上 @EnableConfigServer 注解
    - application.properties 也需要添加上 repository 存放配置文件相关配置：配置仓库地址及仓库的用户与密码
    - 验证 repository 存放配置文件是否成功：访问 localhost:8080/order-a.properties
6. config server 会将远端的git 拉到本地创建的目录下放置
    - 此处默认的路径是/var/folders/45/gn2c8rbs7rs8xyd1ycl7j7zr0000gn/T/config-repo-8133077895891439033
    - 可以在 application.properties 指定目录，此处设为 /Users/hailong/Documents/IdeaProjects/projects/cloud/config/basedir
    - spring.cloud.config.server.git.basedir=/Users/hailong/Documents/IdeaProjects/projects/cloud/config/basedir


