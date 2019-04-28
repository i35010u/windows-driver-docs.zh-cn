---
title: 应用程序通知简介
description: 应用程序通知简介
ms.assetid: c115eb29-8bd2-40f7-b979-cff386bdc9aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a01abb24cf2e1c9de3de5c1afea43c8f2d427bde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341039"
---
# <a name="introduction-to-application-notification"></a>应用程序通知简介


从 Windows Server 2008 开始，处理器和内存模块被视为插 (PnP) 设备。 因此，操作系统使用的即插即用通知机制的应用程序通知。 即插即用通知机制发送 WM\_DEVICECHANGE 窗口消息，用户模式应用程序以通知有关更改硬件分区中的硬件的应用程序。

当新的处理器或内存模块添加到硬件分区时，操作系统将在此通知操作系统已启动新的处理器或内存设备后发送到用户模式应用程序。 对于新的处理器，操作系统不发送此消息可直到在它后面的用户模式应用程序已开始计划新的处理器上的线程。

**请注意**  是异步的所有即插即用通知。 因此，这些通知可能无法由接收用户模式应用程序，直到一段时间后在操作系统已启动的处理器或内存模块。

 

当在用户模式应用程序收到此通知时，它可以相应地调整某些或所有以下各项：

-   每个处理器的内存分配

-   中的应用程序的线程池的线程数

-   内存缓冲区分配

-   负载平衡算法

在用户模式应用程序可以获取通过调用是硬件分区中的物理内存量[GlobalMemoryStatusEx](https://go.microsoft.com/fwlink/p/?linkid=97891)函数。 有关详细信息**GlobalMemoryStatusEx**函数中，请参阅 Microsoft Windows SDK 文档。

在用户模式应用程序必须注册以接收应用程序通知操作系统。 有关详细信息，请参阅[注册应用程序通知](registering-for-application-notification.md)。

 

 




