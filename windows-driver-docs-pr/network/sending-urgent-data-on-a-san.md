---
title: 在 SAN 上发送紧急数据
description: 在 SAN 上发送紧急数据
ms.assetid: 9ff9719a-dd42-4ce7-8c07-370afa17fd7b
keywords:
- 紧急数据 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10370e2e6d1a6e44d6145abc9832ff5fa465f09f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346755"
---
# <a name="sending-urgent-data-on-a-san"></a>在 SAN 上发送紧急数据





如果应用程序在 SAN 上发送紧急的数据，Windows 套接字切换传输的数据作为按以下顺序中所述：

1.  开关用于发送紧急的数据的请求，接收**WSPSend**在其中调用 MSG\_OOB 标志设置。

2.  此开关将紧急的数据复制到控制消息缓冲区的有效负载部分。

3.  此开关调用相应 SAN 服务提供商[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)函数传输 SAN 套接字的远程对等方连接到控制消息中包含的紧急数据。 SAN NIC 又会将紧急的数据传输。

4.  在远程对等方 switch 接收到它使用发布的接收缓冲区的传输的数据[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)函数。

5.  在远程对等方 switch 将接收缓冲区中接收到的数据复制到专用存储。

6.  在远程对等方调用开关**WSPRecv**来重新投递接收缓冲区。

7.  在远程对等方 switch 将数据传送到标准 Windows 套接字过程根据应用程序。

 

 





