---
title: 数据包检查点
description: 数据包检查点
keywords:
- 数据包检查点 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc8e98615eee5e59089b6d6d0aee01cb2a0c5ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840623"
---
# <a name="packet-inspection-points"></a>数据包检查点


对于分配给接收计算机的地址的传入数据包 (本地主机流量) 按以下顺序遍历 WFP 层：

<a href="" id="ip-packet--network-layer-"></a>**IP 数据包 (网络层)**  
所有 IP 数据包（包括 IP 数据包片段）都可在此层上检查。 但是，如果数据包受 IPsec 保护，则无法在此层上执行深度内容检查或修改，因为数据包尚未经过身份验证或解密。

<a href="" id="transport-layer"></a>**传输层**  
所有独立或完全重新组合的数据包都可在该层上检查。 受 IPsec 保护的数据包已通过身份验证或解密。

<a href="" id="application-layer-enforcement--ale--receive-or-accept"></a>**应用程序层强制 (ALE) 接收或接受**  
在此层上指出到达本地终结点的第一个数据包。 例如，到达 TCP 同步 (SYN) 段或与 UDP 流关联的第一条 UDP 消息。 在此层上也指示重新授权连接所需的数据包（例如，防火墙策略更改后），并且将设置 ALE 重新授权标志。

<a href="" id="datagram-data-or-stream"></a>**数据报数据或流**  
UDP 消息和非 ICMP 错误消息都在数据报数据层上指明。 TCP 数据流 (仅) 可在流层进行检查的数据流。

源自发送到发送计算机的地址的传出数据包 (本地主机源流量，) 遍历以下 WFP 层：

<a href="" id="ale-connect"></a>**ALE 连接**  
 (在) 中生成 SYN 段之前发出 TCP 连接请求，并在此层指明发送到远程终结点的第一个 UDP 消息。

<a href="" id="datagram-data-or-stream"></a>**数据报数据或流**  

<a href="" id="transport-and-icmp-error"></a>**传输和 ICMP 错误**  
TCP 连接请求在) 生成 SYN 段之前 (，并在此层指明发送到远程终结点的第一个 UDP 消息。

<a href="" id="ip-packet"></a>**IP 数据包**  
不指示 IP 数据包片段;传出 IP 碎片检查当前不可用。

分配给本地计算机的 IP 数据包或分段不是来自的 IP 数据包或分段，可用于在转发层进行检查。 例如，如果将目标为本地客户端的数据包修改为具有非本地目标地址，然后将其注入接收路径，则该数据包将被注入到转发层中。 同样，如果将来自本地源地址的数据包修改为具有非本地源地址，则在将其注入发送路径后，将传递到转发层。

 

 





