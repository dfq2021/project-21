# project-21
Schnorr-Bacth
# 实验原理
Schnorr 签名是一种数字签名算法，由 Claus-Peter Schnorr 在 1989 年提出。它是一种基于离散对数问题的数字签名方案，被广泛认为比传统的 RSA 签名和 DSA (Digital Signature Algorithm) 更高效、安全。

批处理技术是一种优化方法，用于同时处理多个操作，从而提高计算效率。在密码学中，批处理技术常常用于在单个计算步骤中执行多个操作，以减少计算和通信开销。

Schnorr-Batch 签名方案结合了这两个概念，它允许在一个计算步骤中对多个消息进行签名，从而显著减少了签名的计算成本。这对于高性能的加密协议和区块链系统等场景中特别有用，因为它可以减少交易的签名验证时间和存储开销。

总结起来，Schnorr-Batch 是一种将 Schnorr 签名与批处理技术相结合的密码学签名方案，旨在提高签名的效率和性能。

# 实现方式
1.首先需要实现离散对数的求解，素数和素因子的生成以及计算生成元
```python
def discreteLogarithm(a, b, m):
    return discrete_log(m, b, a)

def prime_generator(a, b):
    check = true
    while check:
        i = random.randrange(a, b)
        if isprime(i):
            check = false
    return i

def divisor_number(p):
    for q in range(pow(2, 10), (p - 1) // 2):
        if (p - 1) % q == 0 & isprime(q):
            return q

def findPrimefactors(s, n):
    # Print the number of 2s that divide n
    while n % 2 == 0:
        s.add(2)
        n = n // 2
    for i in range(3, int(sqrt(n)), 2):
        while n % i == 0:
            s.add(i)
            n = n // i
    if n > 2:
        s.add(n)

def findPrimitive(n):
    s = set()
    if not isprime(n):
        return -1
    phi = n - 1
    findPrimefactors(s, phi)

    for r in range(2, phi + 1):
        flag = False
        for it in s:
            if pow(r, phi // it, n) == 1:
                flag = True
                break
        if not flag:
            return r
    return -1

```
2.之后按照Schnorr签名算法方式，就可以在Schnorr.py文件中直接使用这些计算。
# 实验结果
![image](https://github.com/dfq2021/project-21/assets/129512207/ad3fb3e5-3c05-46c6-bb51-2f429a01c16d)

运行时间：0.9977817535400391 ms
# 运行方式
直接用pycharm平台运行文件目录下的.py文件即可。

# 实验环境
| 语言  | 系统      | 平台   | 处理器                     |
|-------|-----------|--------|----------------------------|
| python| Windows10 | pycharm| Intel(R) Core(TM)i7-11800H |
# 小组分工
戴方奇 202100460092 单人组完成project21
