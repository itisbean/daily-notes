# 

## 

1. 浮點數的表示公式

```
Value = Sing * Exponent * Fraction
```

- **Sign** 符號位(sign bit)，0為正，1為負。
- **Exponent** 指數偏移值(exponent bias)，等於指數的實際值加上某個固定的值，IEEE 754標準規定該固定值為2^(e-1)^-1，*以單精度浮點數為例，指數域占8bit，固定偏移值就是 2^(8-1)^-1=127*
- **Fraction** 分數值(fraction)