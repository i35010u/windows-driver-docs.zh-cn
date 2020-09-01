---
title: 在 SAN 上发送紧急数据
description: 在 SAN 上发送紧急数据
ms.assetid: 9ff9719a-dd42-4ce7-8c07-370afa17fd7b
keywords:
- 紧急数据 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a05d44b866b860d4c3d794ee15bbbcb69504662
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214450"
---
# <a name="sending-urgent-data-on-a-san"></a>在 SAN 上发送紧急数据





如果应用程序在 SAN 上发送紧急数据，Windows 套接字交换机会按以下顺序传输该数据：

1.  对于发送紧急数据的请求，开关将接收设置了 MSG OOB 标志的 **WSPSend** 调用 \_ 。

2.  该开关将紧急数据复制到控制消息缓冲区的负载部分。

3.  此开关调用适当的 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85)) 函数，以将控制消息中包含的紧急数据传输到 SAN 套接字的远程对等连接。 SAN NIC 反过来传输紧急数据。

4.  远程对等节点上的开关接收传输的数据到其通过 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85)) 函数发送的接收缓冲区。

5.  远程对等节点上的交换机将接收的数据从接收缓冲区复制到专用存储。

6.  远程对等机上的开关调用 **WSPRecv** 来重新发布接收缓冲区。

7.  远程对等机上的开关根据标准 Windows 套接字过程将数据传递给应用程序。

 

