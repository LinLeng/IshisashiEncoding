# UTF-VLQ
## 所收编码
### 架空编码
- UTF-VLQ

## 解说
UTF-VLQ 是使用 VLQ 的 UCS 实作编码。

## 字节结构
|字节数|第一字节|第二字节|第三字节|第四字节|码位数|注释|
|-|-|-|-|-|-|-|
|单字节|0x00\~0x7F||||128||
|双字节|0xC2\~0xFF|0x80\~0xBF|||3968||
|三字节|0xC1\~0xFF|0xC0\~0xFF|0x80\~0xBF||256000||
|四字节|0xC1\~0xC4|0xC0\~0xFF|0xC0\~0xFF|0x80\~0xBF|851968||

## 与 UCS 的对应关系
### ASCII 部分（U+0000\~U+007F）
直接表示成单字节。

### 非 ASCII 部分
首先将 UCS 码表示成二进制，并去掉前面的 0。

如果位数不是 6 的倍数，则在前面填充 0，直到位数为 6 的倍数为止。

每 6 位进行分割。除了最后一组，所有组前面都填充 11。最后一组在前面填充 10。

以 U+4E00 为例。

表示成二进制，得 0100111000000000。

去掉前面的 0，得 100111000000000。

填充 0 并分割，得 000100 111000 000000。

填充 1 或 0，得 11000100 11111000 10000000。

所以最终结果为 0xC4F880。
