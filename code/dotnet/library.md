## FluentAssertions

单元测试

以自然的语言来预测结果，支持多种测试框架

```c#
string actual = "ABCDEFGHI";
actual.Should().StartWith("AB").And.EndWith("HI").And.Contain("EF").And.HaveLength(9);
```

## Polly

弹性和瞬态故障处理

