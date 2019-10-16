字符串与bytes
---
字符串是字符组成的有序序列，字符可以使用编码来理解
- bytes是字节组成的有序的不可变序列
- bytearray是字节组成的有序的可变序列
编码与解码
- 字符串按照不同的字符集编码encode返回字节序列bytes
 - encode(encoding='utf-8', errors='strict') -> bytes
- 字节序列按照不同的字符集解码decode返回字符串
 - bytes.decode(encoding="utf-8", errors="strict") -> str
 - bytearray.decode(encoding="utf-8", errors="strict") -> str
