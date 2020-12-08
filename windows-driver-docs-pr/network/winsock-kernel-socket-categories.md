---
title: Winsock 内核套接字类别
description: Winsock 内核套接字类别
keywords:
- Winsock 内核 WDK 网络，套接字类别
- WSK WDK 网络，套接字类别
- 基本套接字 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 数据报套接字 WDK Winsock 内核
- 面向连接的套接字 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46ca851a92cf1ceba71806b9a22a266fd1cdd298
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836219"
---
# <a name="winsock-kernel-socket-categories"></a>Winsock 内核套接字类别


Winsock 内核 (WSK) [网络编程接口 (NPI)](network-programming-interface.md) 定义五个不同类别的套接字 *：基本套接字*、 *侦听套接字*、 *数据报套接字*、 *面向连接的套接字* 和 *流套* 接字。 每个 WSK 套接字类别都具有独特的功能，并支持一组不同的套接字函数。 WSK 应用程序必须指定在创建新套接字时创建的 WSK 套接字的类别。 每个 WSK 套接字类别的用途如下所示：

<a href="" id="basic-sockets-------"></a>**基本套接字**   
基本套接字仅用于获取和设置传输堆栈套接字选项或执行套接字 i/o 控制操作。 基本套接字不能绑定到本地传输地址，也不支持发送或接收网络数据。

<a href="" id="listening-sockets-------"></a>**侦听套接字**   
侦听套接字用于侦听来自远程传输地址的传入连接。 侦听套接字的功能包括基本套接字的所有功能。

<a href="" id="datagram-sockets-------"></a>**数据报套接字**   
数据报套接字用于发送和接收数据报。 数据报套接字的功能包括基本套接字的所有功能。

<a href="" id="connection-oriented-sockets-------"></a>**面向连接的套接字**   
面向连接的套接字用于通过建立的连接发送和接收网络数据。 面向连接的套接字的功能包括基本套接字的所有功能。

<a href="" id="stream-sockets-------"></a>**流套接字**   
流套接字用于侦听远程传输地址中的传入连接 (充当侦听套接字) ，或通过建立的连接发送和接收网络数据 (充当面向连接的套接字) 。 如果需要侦听套接字或面向连接的套接字，则在创建套接字时不知道，请使用流套接字。 流套接字的功能包括基本套接字的所有功能。
 





