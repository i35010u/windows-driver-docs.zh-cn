---
title: 应用程序通知简介
description: 应用程序通知简介
ms.assetid: c115eb29-8bd2-40f7-b979-cff386bdc9aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cd5ddcf7dc0f90770b0d4ab11b3b4f4f560732f0
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733065"
---
# <a name="introduction-to-application-notification"></a>应用程序通知简介


从 Windows Server 2008 开始，会将处理器和内存模块视为即插即用 (PnP) 设备。 因此，操作系统使用应用程序通知的 PnP 通知机制。 PnP 通知机制将 WM \_ DEVICECHANGE 窗口消息发送到用户模式的应用程序，以通知应用程序对硬件分区中的硬件所做的更改。

当将新的处理器或内存模块添加到硬件分区时，操作系统启动了新的处理器或内存设备后，操作系统会将此通知发送到用户模式应用程序。 对于新的处理器，操作系统在开始计划新处理器上的线程之前，不会将此消息发送给用户模式应用程序。

**注意**   所有 PnP 通知都是异步的。 因此，用户模式应用程序在操作系统启动处理器或内存模块之前，可能不会收到这些通知。

 

当用户模式应用程序收到此通知时，它可以相应地调整部分或全部以下项：

-   每个处理器的内存分配

-   应用程序的线程池中的线程数

-   内存缓冲区分配

-   负载平衡算法

用户模式应用程序可以通过调用 [GlobalMemoryStatusEx](/windows/win32/api/sysinfoapi/nf-sysinfoapi-globalmemorystatusex) 函数获取硬件分区中的物理内存量。 有关 **GlobalMemoryStatusEx** 函数的详细信息，请参阅 Microsoft Windows SDK 文档。

用户模式应用程序必须向操作系统注册，以接收应用程序通知。 有关详细信息，请参阅 [注册应用程序通知](registering-for-application-notification.md)。

 

