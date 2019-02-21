---
title: 筛选注册表调用
description: 筛选注册表调用
ms.assetid: 6b35c3a0-4ece-4101-b348-e71f5cccf0c8
keywords:
- 筛选注册表调用 WDK 内核
- 注册表筛选驱动程序 WDK 内核
- RegistryCallback
- 筛选注册表调用 WDK 的内核，有关筛选注册表调用
- 注册表筛选驱动程序 WDK 内核，有关筛选注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3875f62cc4aa19e775384500c6653097d83d2bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523111"
---
# <a name="filtering-registry-calls"></a>筛选注册表调用


一个*筛选驱动程序的注册表*是筛选注册表的调用，如驱动程序组件的防病毒软件程序包的任何内核模式驱动程序。 配置管理器，它实现了注册表，允许注册表筛选驱动程序来筛选对注册表函数的任何线程的调用。 首先在 Microsoft Windows XP 中支持的注册表调用筛选。

在 Windows XP 上的注册表筛选驱动程序可以调用[ **CmRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541918)注册[ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)例程和[**CmUnRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541928)取消注册回调例程。 *RegistryCallback*例程接收的每个注册表操作的通知之前的配置管理器正在处理操作。 一套**REG\_*XXX*\_密钥\_信息**数据结构包含有关每个注册表操作的信息。 *RegistryCallback*例程可以阻止注册表操作。 回调例程还会收到通知时配置管理器已完成创建或打开注册表项。

Windows Server 2003 提供了附加完成通知。

Windows Vista 提供了以下其他注册表筛选功能：

-   注册表筛选驱动程序在驱动程序堆栈中，可以进行分层，堆栈中的每个驱动程序可以筛选注册表操作。

-   **CmRegisterCallback**例程替换为[ **CmRegisterCallbackEx** ](https://msdn.microsoft.com/library/windows/hardware/ff541921)例程。

-   驱动程序可以完全处理注册表操作 （或将请求的操作重定向到不同的操作），并防止配置管理器处理该操作。

-   驱动程序可以将上下文信息分配给单个注册表操作或键对象。

-   驱动程序可以修改注册表操作的输出参数和返回值。

-   已添加到所有其他成员**REG\_*XXX*\_密钥\_信息**数据结构。

-   驱动程序收到通知的其他注册表操作。

有关驱动程序可以筛选每个版本的 Windows 的注册表操作的列表，请参阅[ **REG\_通知\_类**](https://msdn.microsoft.com/library/windows/hardware/ff560950)。

若要了解有关筛选注册表调用的详细信息，请参阅以下主题：

[注册通知](registering-for-notifications.md)

[处理通知](handling-notifications.md)

[支持分层的注册表筛选驱动程序](supporting-layered-registry-filtering-drivers.md)

[指定的上下文信息](specifying-context-information.md)

[获取附加注册表信息](obtaining-additional-registry-information.md)

[中的注册表通知无效密钥对象指针](invalid-key-object-pointers-in-registry-notifications.md)

[筛选应用程序上的注册表操作配置单元](filtering-registry-operations-on-application-hives.md)

 

 




