---
layout: post
title: code highlight test
date: 2018-01-18
categories: blog
tags: [test]
subtitle: 测试代码高亮
---

```java

public interface LongTermTaskCallback {
    void callback(Object result);
}
 
public class LongTimeAsyncCallService {
    private final int CorePoolSize = 4;
    private final int NeedSeconds = 3;
    private Random random = new Random();
    private ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(CorePoolSize);
    public void makeRemoteCallAndUnknownWhenFinish(LongTermTaskCallback callback){
        System.out.println("完成此任务需要 : " + NeedSeconds + " 秒");
        scheduler.schedule(new Runnable() {
            @Override
            public void run() {
                callback.callback("长时间异步调用完成.");
            }
        }, "这是处理结果:)", TimeUnit.SECONDS);
    }	
}


```


```sql

insert into `ams_sys_config` (`config_key`, `config_value`, `config_type`, `create_time`, `remark`) values('smsRateRedisChannel', 'exceedChannels', 'string', '2018-01-05 11:50:34', '通道使用率超过70%的redis发布通道');
insert into `ams_sys_config` (`config_key`, `config_value`, `config_type`, `create_time`, `remark`) values('smsRatePublisOpen', '0', 'int', '2018-01-05 11:51:08', '通道使用率超过70%的redis发布开关');

```