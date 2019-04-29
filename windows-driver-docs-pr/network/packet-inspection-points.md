---
title: 数据包检查点
description: 数据包检查点
ms.assetid: 9ad1c660-6811-4659-94ad-201a102a9ded
keywords:
- 数据包检查点 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21d158c06999e6f60a6f24ad8ea917ee5225e928
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363637"
---
# <a name="packet-inspection-points"></a>数据包检查点


传入的数据包分配给 WFP 层按以下顺序接收的计算机 （本地主机流量） 遍历的地址：

<a href="" id="ip-packet--network-layer-"></a>**IP 数据包 （网络层）**  
包括 IP 数据包分段的所有 IP 数据包都都可用于检查在此层。 但是，当数据包都不会受 IPsec 保护，深度内容检查或修改不能在执行时这一层数据包不是因为尚未经过身份验证或解密。

<a href="" id="transport-layer"></a>**传输层**  
独立部署或完全重新组合的所有数据包都都可用于检查在此层。 已通过身份验证或解密受 IPsec 保护的数据包。

<a href="" id="application-layer-enforcement--ale--receive-or-accept"></a>**应用程序层强制措施 (ALE) 接收或接受**  
到达本地终结点的第一个数据包指示在此层。 例如，到达 TCP 同步 (SYN) 段，或将指出与 UDP 流相关联的第一个 UDP 消息。 在此层，也会指示需要重新对连接进行授权，例如，防火墙策略更改之后的数据包并将设置 ALE 重新授权标志。

<a href="" id="datagram-data-or-stream"></a>**数据报数据或 Stream**  
UDP 消息和非 ICMP 错误消息指示在数据报数据层。 TCP 数据流 （仅适用于数据流） 都可用于在流层的检查。

源自以下 WFP 层下发送的计算机 （源自本地主机通信） 遍历到分配的地址的传出数据包：

<a href="" id="ale-connect"></a>**ALE 连接**  
TCP 连接 （SYN 段生成之前进行） 的请求和发送到远程终结点的第一个 UDP 消息表示在此层。

<a href="" id="datagram-data-or-stream"></a>**数据报数据或 Stream**  

<a href="" id="transport-and-icmp-error"></a>**传输和 ICMP 错误**  
TCP 连接请求 （之前生成的 SYN 段） 和发送到远程终结点的第一个 UDP 消息表示在此层。

<a href="" id="ip-packet"></a>**IP 数据包**  
未指定 IP 数据包分段;检查传出 IP 分段的是当前不可用。

IP 数据包或不是源自，或不是以片段，分配给本地计算机的地址是可用于检查在转发层。 例如，如果数据包发送到本地客户端修改为使用非本地的目标地址，然后被注入到接收路径，它将注入到转发层中。 同样，如果的数据包，源自本地源地址修改为使用非本地源地址，它将会传送给转发层后注入到发送路径。

 

 





