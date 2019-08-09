---
title: fastjson反序列化LocalDateTime失败解决方案
date: 2019-07-31 14:21:57
tags:
---

> ```java
>     @Bean
>     public RedisTemplate<String, Serializable> redisTemplate(LettuceConnectionFactory redisConnectionFactory) {
>         RedisTemplate<String, Serializable> template = new RedisTemplate<>();
>         template.setKeySerializer(new StringRedisSerializer());
>         template.setValueSerializer(genericJackson2JsonRedisSerializer());
>         template.setConnectionFactory(redisConnectionFactory);
>         return template;
>     }
> 
>     @Bean
>     public GenericJackson2JsonRedisSerializer genericJackson2JsonRedisSerializer() {
>         ObjectMapper om = new ObjectMapper();
>         om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
>         // 解决jackson2无法反序列化LocalDateTime的问题
>         om.disable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS);
>         om.registerModule(new JavaTimeModule());
>         om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
>         return new GenericJackson2JsonRedisSerializer(om);
>     }
> ```

