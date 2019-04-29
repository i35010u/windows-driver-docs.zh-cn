---
title: Winsock 内核套接字类别
description: Winsock 内核套接字类别
ms.assetid: e99cbef5-c484-43ee-be02-8088f51117ef
keywords:
- 网络、 Winsock 内核 WDK 套接字类别
- WSK WDK 网络，套接字类别
- 基本套接字 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 数据报套接字 WDK Winsock 内核
- 面向连接的套接字 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e7dd65891cc5c27e326da663c876619c81d4bc3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379797"
---
# <a name="winsock-kernel-socket-categories"></a>Winsock 内核套接字类别


Winsock Kernel (WSK)[网络编程接口 (NPI)](network-programming-interface.md)定义五个不同类别的套接字：*基本套接字*，*侦听套接字*， *数据报套接字*，*面向连接的套接字*，并*流套接字*。 每个 WSK 套接字类别具有的独特功能，并支持一组不同的套接字函数。 WSK 应用程序必须指定 WSK 套接字的类别创建时它会创建一个新的套接字。 每个 WSK 套接字类别的目的是，如下所示：

<a href="" id="basic-sockets-------"></a>**基本的套接字**   
基本的套接字用于仅用于获取和设置传输堆栈的套接字选项，或若要执行套接字 I/O 控制操作。 基本的套接字不能绑定到本地传输地址，不支持发送或接收网络数据。

<a href="" id="listening-sockets-------"></a>**侦听套接字**   
侦听套接字用于侦听来自远程传输地址的传入连接。 侦听套接字的功能包括的所有基本套接字功能。

<a href="" id="datagram-sockets-------"></a>**数据报套接字**   
数据报套接字用于发送和接收数据报。 数据报套接字的功能包括的所有基本套接字功能。

<a href="" id="connection-oriented-sockets-------"></a>**面向连接的套接字**   
面向连接的套接字用于通过发送和接收网络数据已建立的连接。 面向连接的套接字的功能包括的所有基本套接字功能。

<a href="" id="stream-sockets-------"></a>**Stream 套接字**   
Stream 套接字用于可以侦听传入连接从远程传输地址 （作为侦听套接字），或通过发送和接收网络数据已建立的连接 （作为面向连接的套接字）。 使用流套接字时您不知道在创建套接字时如果您希望侦听套接字或面向连接的套接字。 流套接字的功能包括的所有基本套接字功能。
 





