# Gem5 Note

## 设计实现

### port

To connect memory system components together, gem5 uses a port abstraction. Each memory object can have two kinds of ports, *request ports* and *response ports*. Requests are sent from a request port to a response port, and responses are sent from a response port to a request port. When connecting ports, you must connect a request port to a response port.

## 调用堆栈

以SimpleCPU为例，其调用堆栈如图：

![image-20211212183202664](/home/zhong/.config/Typora/typora-user-images/image-20211212183202664.png)

