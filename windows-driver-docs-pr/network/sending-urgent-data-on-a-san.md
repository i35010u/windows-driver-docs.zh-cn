---
title: 在 SAN 上发送紧急数据
description: 在 SAN 上发送紧急数据
ms.assetid: 9ff9719a-dd42-4ce7-8c07-370afa17fd7b
keywords:
- 紧急数据 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2168866c5b17ec8deb1b15c72d0c896646ff055a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386834"
---
# <a name="sending-urgent-data-on-a-san"></a>在 SAN 上发送紧急数据





如果应用程序在 SAN 上发送紧急的数据，Windows 套接字切换传输的数据作为按以下顺序中所述：

1.  开关用于发送紧急的数据的请求，接收**WSPSend**在其中调用 MSG\_OOB 标志设置。

2.  此开关将紧急的数据复制到控制消息缓冲区的有效负载部分。

3.  此开关调用相应 SAN 服务提供商[ **WSPSend** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))函数传输 SAN 套接字的远程对等方连接到控制消息中包含的紧急数据。 SAN NIC 又会将紧急的数据传输。

4.  在远程对等方 switch 接收到它使用发布的接收缓冲区的传输的数据[ **WSPRecv** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))函数。

5.  在远程对等方 switch 将接收缓冲区中接收到的数据复制到专用存储。

6.  在远程对等方调用开关**WSPRecv**来重新投递接收缓冲区。

7.  在远程对等方 switch 将数据传送到标准 Windows 套接字过程根据应用程序。

 

 





