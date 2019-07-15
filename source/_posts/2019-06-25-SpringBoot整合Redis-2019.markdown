---
layout:     post
title:      "SpringBoot整合Redisson"
subtitle:   " \"一边生活 | 一边代码\""
date:       2019-06-25
author:     "wuyi"
header-img: "img/post-bg-2015.jpg"
tags:
    - Redis
    - SpringBoot
---
>

## Redis使用场景

- 通常情况下,Redis常用作不频繁更新的热点数据的缓存,(如果数据量不大,感觉还是本地缓存比较好,比如全国省份列表等);
- [这里](http://blog.720ui.com/2016/redis_action_01_use_core/)对Redis缓存的使用合理性分析.

## Redis在Java中使用的客户端
- Jedis:

    可以认为这是比较接近redis一款Java实现客户端，其API和数据结构与Redis十分接近；
- Redission:

    其底层采用了Netty框架，提供了更加接近Java编程的方法，并对redis的数据结构进行了扩展，提供分布式支持等；用官方的话来说就是：
    Redisson的宗旨是促进使用者对Redis的关注分离（Separation of
    Concern），从而让使用者能够将精力更集中地放在处理业务逻辑上；

## 单机模式下与SpringBoot整合
- Redission支持多种方式进行配置如Java编程式配置和文件配置方式，其中文件配置方式有支持Json格式和yml文件格式配置方式：

  >  配置方式

        @Bean
        public static RedissonClient getRedissonClient() throws IOException {
            // yml文件配置方式
            Config config = Config.fromYAML(new ClassPathResource("application.yml").getInputStream());
            RedissonClient redissonClient = Redisson.create(config);
            return redissonClient;

            // Java编程式配置（其中属性要与Redission配置属性相对应）
            // Config config = new Config();
            // config.useSingleServer().setAddress("redis://yourhost:6379");
            // return Redisson.create(config);
        }


