---
layout: post
title: @Conditional注解
---


1. @Conditional注解: 条件，注解内的条件满足才会创建这个类

    @Conditional(MyCondition.class)
    @Bean
    public String example() {
        return "example";
    }

    class MyCondition implements Condition {
        public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
            ...
        }
    }


2. @ConditionalOnClass注解: classpath里存在这个类才去解析配置类

3. @ConditionalOnMissingClsss