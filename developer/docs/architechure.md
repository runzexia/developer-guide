# 系统架构

AppCenter 2.0 包括开发者控制台和用户控制台及调度系统三大部分，最终用户在[青云官网](https://appcenter.qingcloud.com/)上可以浏览服务商提供的 App 并创建 App 实例。个人用户和企业用户可以在开发者控制台开发供自己内部使用的 App。开发应用的时候，除了填写必要的应用信息外，还要上传一个配置包，这个配置包含 config.json，cluster.json.mustache 和国际化语言包，这些文件是一种描述性的集群实例信息的文件。使用者在创建该 App 实例的时候，青云的调度系统会根据这个配置包定义的信息创建基础资源，
然后注册集群信息到青云为每个 VPC 环境下部署的 metadata service 中，集群主机通过 confd (配合 toml，tmpl 模版配置文件系统)进程检查 metadata service 的变化，来刷新应用配置文件，然后启动应用服务。 

![系统架构图](../images/architecture.png)