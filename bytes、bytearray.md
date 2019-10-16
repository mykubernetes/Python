字符串与bytes
- 字符串是字符组成的有序序列，字符可以使用编码来理解
- bytes是字节组成的有序的不可变序列
- bytearray是字节组成的有序的可变序列

编码与解码
字符串按照不同的字符集编码encode返回字节序列bytes
 - encode(encoding='utf-8', errors='strict') -> bytes

字节序列按照不同的字符集解码decode返回字符串
 - bytes.decode(encoding="utf-8", errors="strict") -> str
 - bytearray.decode(encoding="utf-8", errors="strict") -> str


bytes定义
---
定义
- bytes() 空bytes
- bytes(int) 指定字节的bytes，被0填充
- bytes(iterable_of_ints) -> bytes [0,255]的int组成的可迭代对象
- bytes(string, encoding[, errors]) -> bytes 等价于string.encode()
- bytes(bytes_or_buffer) -> immutable copy of bytes_or_buffer 从一个字节序列或者buffer复制出一个新的不可变的bytes对象
- 使用b前缀定义
  - 只允许基本ASCII使用字符形式b'abc9'
  - 使用16进制表示b"\x41\x61"

```
print(bytes("abc","utf8"))
b'abc'

print("abc".encode())
b'abc'

a = "abc".encode()
print(type(a))
bytes

print(a.decode())
'abc'
```  

```
a = "abc".encode()
pring(a.split(b'b'))
[b'a',b'c']
```  
