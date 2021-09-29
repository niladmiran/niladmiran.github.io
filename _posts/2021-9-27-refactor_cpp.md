# 重构
重构第一步： 建立测试环境，为重构的代码编写单元测试。好的测试是重构的根本。

## 重构步骤
1. 找出代码的逻辑泥团并运用Extract Method,此方法可以分解过长的函数
2. 函数分解完毕之后，使用Substitute Algorithm引入更清晰的算法


## Extract Method

## Replace Method with Method Object

## Replace Temp with Query

## Introduce Explanning variable
如果我们有一个复杂的表达式，我们可以将这个复杂表达式的结果放进一个临时变量，以此变量名称来解释表达式的用途。

这个方法主要用于拥有大量局部变量的算法，此时extract method会不可行。

## Split Temporary Variable


