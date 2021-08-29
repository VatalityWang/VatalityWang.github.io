---
layout: post
title: 流程图
categories: 学习
description: mermaid
keywords: flowcat code
mermaid: true
---



<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

<head>
 <script src="//unpkg.com/mermaid@8.4.8/dist/mermaid.min.js"></script>
	<script>mermaid.initialize({startOnLoad:true});
	</script>
</head>


# 1 server

```mermaid
graph TD
subgraph __
A(开始) -->B[读取配置]
B-->C[初始化日志]
C-->C1[初始化各终端状态]
C1-->E[绑定端口]
E-->F[等待连接]
F-->G{连接成功?}
end 
subgraph _
G-->|Y|H[创建客户端指令线程]
H-->H1[等待指令]
H1-->M{指令到来}
M-->|N|H1
M-->|Y|M1[解析指令]
M1-->M2{控制中心 or 定制终端?}
M2-->|控制中心|M3[状态存储 指令转发]
M2-->|定制终端|M4[指令响应反馈]
M3-->M5[状态存储]
M5-->M6[反馈状态至控制中心]
M4-->M5
M6-->H1
end

subgraph _
G-->|Y|H2[创建客户端心跳线程]
H2-->H4[等待回复心跳包]
H4-->H3{等待超时?}
H3-->|N|H5[发送心跳包]
H3-->|Y|H6[心跳线程退出]
H6-->H7[对应客户端状态清理]
H7-->H8[反馈状态至控制中心]
H8-->F
G-->|N|F
end



subgraph _
F--程序异常-->N(结束)
end
```

# 2 client

 ```mermaid

graph TD
A(开始) -->B[读取配置]
B-->C[连接后台服务器]
C-->D{后台服务器在线?}
D--Y-->E[连接成功]
E-->G[接收指令]


G-->M[指令解析]
M-->G1{操作指令?后台反馈指令}
G1--操作指令-->G3{是否关闭软件?}
G3--Y-->G4(结束)


G3--N-->G2[指令转发至后台服务器]
G1--反馈指令-->N
G2-->N[更新界面]
N-->G

D--N-->F[连接失败]
F-->C

 ```