---
title: Winsock 内核体系结构
description: Winsock 内核体系结构
ms.assetid: 3a43c200-4180-4d1b-8ca6-ee82a84b9194
keywords:
- 网络、 Winsock 内核 WDK 体系结构
- WSK WDK 网络、 体系结构
- 体系结构 WDK Winsock 内核
- 网络模块 WDK Winsock 内核
- 子系统 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2162e94a4afc94eaee7c39717750c0b0fe37d654
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544797"
---
# <a name="winsock-kernel-architecture"></a>Winsock 内核体系结构


下图中显示体系结构的 Winsock Kernel (WSK)。

![说明 wsk 的体系结构的关系图 ](images/wskarch.png)

WSK 核心体系结构是 WSK 子系统。 WSK 子系统[网络模块](network-module.md)实现的提供商一端 WSK[网络编程接口 (NPI)](network-programming-interface.md)。 WSK 子系统可以与在其下边缘上的传输提供程序为各种传输协议提供支持的接口。

附加到 WSK 子系统是 WSK 应用程序。 WSK 应用程序是实现 WSK NPI 的客户端以执行网络 I/O 操作的内核模式软件模块。 （在此上下文中，"客户端"不应与在客户端-服务器系统中使用的术语相混淆）。 . WSK 子系统可以 WSK 客户端 NPI 通知的异步事件 WSK 应用程序中调用函数。

WSK 应用程序发现和使用的一组附加到 WSK 子系统[WSK 注册函数](https://msdn.microsoft.com/library/windows/hardware/ff571179)。 动态检测 WSK 子系统不可用并交换调度表构成的提供程序和客户端的 WSK NPI 端实现，应用程序可以使用这些函数。

或者，WSK 应用程序可以使用附加到 WSK 子系统[网络模块注册机构 (NMR)](network-module-registrar2.md)。 有关详细信息，请参阅[用于 WSK 注册和注销使用 NMR](using-nmr-for-wsk-registration-and-unregistration.md)。

 

 





