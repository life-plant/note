1. All netty servers require :
    - At least one channelHandler
    - bootstrapping

2. channel是通道，是全双工的，可读可写，或者一起读一起写

3. selector多路复用器，使用selector去轮询channel是否就绪，只需要一个进程管理selector，就可以接入千千万万个客户端

4. 