
## 实时数仓
    逻辑计算层：Spark Streaming、Flink
    消息队列：Kafka、Talos
    落盘：HBase、Mysql、Pegasus
    OLAP：Druid、Doris、Greenplum、Clickhouse、Presto

    1、Lambda架构：
        在离线大数据架构基础上加了一个加速层，使用流处理技术完成实时性较高的计算。
    
        批处理层(Batch Layer)：存储管理主数据集(不可变的数据集)和预先批处理计算好的视图。
        速度处理层(Apeed Layer)：实时处理新来的数据，降低批处理层的延迟。
        相应查询服务层(Serving Layer)：返回预先计算好的数据视图和速度层构建好的数据视图的合并结果，响应查询。
    
    不足：
        同样的代码需要开发两套一样的代码。
        同样的逻辑计算两次，整体占用资源会增多。
    
    2、Kappa架构：
        以实时事件处理为核心，统一数据处理。

        与Lambda架构不同的是，Kappa结构去掉了批处理层。
        统一数据处理方式，一套代码处理离线和实时的逻辑。
        
    不足：
        不适用离线和实时同一套代码逻辑。
        重新处理历史的吞吐不如批处理。
        修改或历史回溯都需要通过重新消费上游数据。
