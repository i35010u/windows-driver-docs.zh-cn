---
title: Winsock 内核对象
description: Winsock 内核对象
ms.assetid: 1ce9bd19-9159-4a73-96f6-6e2adac886b9
keywords:
- 网络、 Winsock 内核 WDK 对象
- 网络、 WSK WDK 对象
- 对象 WDK Winsock 内核
- 套接字对象 WDK Winsock 内核
- 客户端对象 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ff662187dd3341091f87d5747fb3a693a9c1ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330434"
---
# <a name="winsock-kernel-objects"></a>Winsock 内核对象


Winsock Kernel (WSK)[网络编程接口 (NPI)](network-programming-interface.md)是设计围绕两个主要对象类型：*客户端*并*套接字*。

<a href="" id="client-object-------"></a>**客户端对象**   
一个*客户端对象*表示附件或 WSK 应用程序和 WSK 子系统之间绑定。 客户端对象来表示[ **WSK\_客户端**](https://msdn.microsoft.com/library/windows/hardware/ff571155)结构。 指向客户端对象的指针返回到 WSK 应用程序在过程中的附件 WSK 子系统。 WSK 应用程序将此指针传递给所有客户端对象级别操作的 WSK 函数。

<a href="" id="socket-object-------"></a>**套接字对象**   
一个*套接字对象*表示可用于网络 I/O 的网络套接字。 通过表示套接字对象[ **WSK\_套接字**](https://msdn.microsoft.com/library/windows/hardware/ff571182)结构。 应用程序会创建一个新的套接字时或当应用程序接受传入连接时，将到 WSK 应用程序返回指向套接字对象的指针。 WSK 应用程序将此指针传递给所有特定于特定的套接字的 WSK 函数。

 

 





