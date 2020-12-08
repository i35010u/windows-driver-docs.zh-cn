---
title: 应用程序通知简介
description: 应用程序通知简介
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a1d5d7c0677f04b3c526b10f2a164007d4913429
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824425"
---
# <a name="introduction-to-application-notification"></a>应用程序通知简介


从 Windows Server 2008 开始，会将处理器和内存模块视为即插即用 (PnP) 设备。 因此，操作系统使用应用程序通知的 PnP 通知机制。 PnP 通知机制将 WM \_ DEVICECHANGE 窗口消息发送到用户模式的应用程序，以通知应用程序对硬件分区中的硬件所做的更改。

当将新的处理器或内存模块添加到硬件分区时，操作系统启动了新的处理器或内存设备后，操作系统会将此通知发送到用户模式应用程序。 对于新的处理器，操作系统在开始计划新处理器上的线程之前，不会将此消息发送给用户模式应用程序。

**注意**   所有 PnP 通知都是异步的。 因此，用户模式应用程序在操作系统启动处理器或内存模块之前，可能不会收到这些通知。

 

当用户模式应用程序收到此通知时，它可以相应地调整部分或全部以下项：

-   每个处理器的内存分配

-   应用程序的线程池中的线程数

-   内存缓冲区分配

-   负载平衡算法

用户模式应用程序可以通过调用 [GlobalMemoryStatusEx](/windows/win32/api/sysinfoapi/nf-sysinfoapi-globalmemorystatusex) 函数获取硬件分区中的物理内存量。 有关 **GlobalMemoryStatusEx** 函数的详细信息，请参阅 Microsoft Windows SDK 文档。

用户模式应用程序必须向操作系统注册，以接收应用程序通知。 有关详细信息，请参阅 [注册应用程序通知](registering-for-application-notification.md)。

 

