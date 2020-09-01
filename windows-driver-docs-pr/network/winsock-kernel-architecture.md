---
title: Winsock 内核体系结构
description: Winsock 内核体系结构
ms.assetid: 3a43c200-4180-4d1b-8ca6-ee82a84b9194
keywords:
- Winsock 内核 WDK 网络，体系结构
- WSK WDK 网络，体系结构
- 体系结构 WDK Winsock 内核
- 网络模块 WDK Winsock 内核
- 子系统 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6653d1d1ee7694bf95a30da927ccb3f61d6e44e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206709"
---
# <a name="winsock-kernel-architecture"></a>Winsock 内核体系结构


下图显示了 Winsock 内核 (WSK) 的体系结构。

![阐释 wsk 的体系结构的关系图 ](images/wskarch.png)

WSK 体系结构的核心是 WSK 子系统。 WSK 子系统是一个 [网络模块](network-module.md) ，用于实现 WSK [网络编程接口的提供方 (NPI) ](network-programming-interface.md)。 WSK 子系统与传输提供程序在其下边缘提供对各种传输协议的支持。

附加到 WSK 子系统的 WSK 应用程序。 WSK 应用程序是实现 WSK NPI 客户端的内核模式软件模块，以便执行网络 i/o 操作。  (在此上下文中，"客户端" 不应与) 的客户端-服务器系统中使用的术语混淆。 . WSK 子系统可以调用 WSK 客户端 NPI 中的函数，以通知 WSK 应用异步事件。

WSK 应用程序使用一组 [WSK 注册函数](/windows-hardware/drivers/ddi/_netvista/)发现并附加到 WSK 子系统。 应用程序可以使用这些函数在 WSK 子系统可用时动态检测，并交换组成 WSK NPI 提供程序和客户端实现的调度表。

另外，WSK 应用程序可以通过使用 [网络模块注册器 (NMR) ](network-module-registrar2.md)来附加到 WSK 子系统。 有关详细信息，请参阅 [使用 NMR 进行 WSK 注册和注销](using-nmr-for-wsk-registration-and-unregistration.md)。

 

