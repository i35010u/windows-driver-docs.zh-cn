---
title: 指定上下文信息
description: 指定上下文信息
ms.assetid: 7133529f-5a6c-4df1-8d03-1c79c0d98fa9
keywords:
- 筛选注册表调用 WDK 内核，上下文信息
- 筛选驱动程序 WDK 内核，上下文信息的注册表
- 上下文信息
- 上下文信息 WDK 筛选器注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42749cfe5bc25ca98405d0061cb3f3acade2dd70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367932"
---
# <a name="specifying-context-information"></a>指定上下文信息


配置管理器提供多种方式筛选驱动程序，以将上下文信息分配给注册表操作的注册表。 注册表筛选驱动程序可以：

-   将分配到的上下文信息[ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)例程。

    当您的驱动程序调用[ **CmRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541918)或[ **CmRegisterCallbackEx** ](https://msdn.microsoft.com/library/windows/hardware/ff541921)以注册通知注册表操作该驱动程序可以指定驱动程序定义的上下文值。 配置管理器将此上下文值传递给驱动程序的*RegistryCallback*例程的配置管理器调用例程每次。

    开始使用 Windows XP 支持此上下文信息。

-   将上下文信息分配给注册表操作。

    驱动程序可以存储特定于操作的上下文中的信息**CallContext**的每个成员**REG\_*XXX*\_密钥\_信息**结构的驱动程序的*RegistryCallback*例程接收。 如果您的驱动程序收到预通知和注册表操作的后通知[ **REG\_POST\_操作\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560971)结构包含适当的预先通知结构的指针。 当*RegistryCallback*例程接收**REG\_POST\_操作\_信息**结构， **CallContext**该结构的成员匹配**CallContext**预通知结构中的成员。

    **CallContext**这些结构的成员是从 Windows Vista 开始提供。

-   分配到注册表项对象的上下文信息。

    一个[ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)例程可以将上下文信息分配给特定的注册表密钥对象。 如果*RegistryCallback*例程调用[ **CmSetCallbackObjectContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541924)以将上下文信息分配给键对象，后续的预先通知和在对象上的所有操作后通知将包括中的上下文值**ObjectContext**的每个成员**REG\_*XXX* \_密钥\_信息**结构。 如果驱动程序提供了多个*RegistryCallback*例程，该驱动程序可以分配不同的上下文信息为每个例程，用于单个注册表密钥对象。

    如果驱动程序已调用**CmSetCallbackObjectContext**，在驱动程序*RegistryCallback*例程将收到**RegNtCallbackObjectContextCleanup**通知后密钥对象的句柄已关闭。 在响应此通知，该例程应释放它分配给对象的上下文的资源。 当*Argument1*参数*RegistryCallback*例程**RegNtCallbackObjectContextCleanup**，则*Argument2*参数是指向指针[ **REG\_回调\_上下文\_清理\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560919)结构，其中包含指向的指针上下文。

    **CmSetCallbackObjectContext**例程并**RegNtCallbackObjectContextCleanup**通知是从 Windows Vista 开始提供。

 

 




