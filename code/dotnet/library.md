## FluentAssertions

单元测试

以自然的语言来预测结果，支持多种测试框架

```c#
string actual = "ABCDEFGHI";
actual.Should().StartWith("AB").And.EndWith("HI").And.Contain("EF").And.HaveLength(9);
```

## Polly

弹性和瞬态故障处理

## Ocelot

.NET Core开源API网关

## IdentityServer4

基于OIDC架构的身份认证授权服务器

## MediatR

利用中介者模式，解耦消息的发送和接收者之间的关联

## Autofac.Extras.Moq

结合`Autofac`与`Moq`使用，在单元测试中将mock对象注入到容器中

## HealthChecks && HealthChecks.UI

健康检查

## Dapper

高性能ORM