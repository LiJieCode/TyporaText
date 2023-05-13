# IDEA

## Hadoop

```java


```







## Kafka

```java
// 0 配置
// 1 创建kafka生产者
// 2 发送数据
// 3 关闭资源


public class CustomProducer {
    public static void main(String[] args) {

        // 0 配置
        Properties properties = new Properties();

        // 连接集群  "bootstrap.servers"
        properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "l9z102:9092,l9z103:9092");

        // 指定对应的key和value的序列化类型  -   用到了反射
        properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
        properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

        // 1 创建kafka生产者
        // "" hello
        KafkaProducer<String, String> kafkaProducer = new KafkaProducer<>(properties);

        // 2 发送数据
        kafkaProducer.send(new ProducerRecord<>("first", "hello"));

        // 3 关闭资源
        kafkaProducer.close();
    }
}
```

