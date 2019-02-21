---
title: 取消注册微筛选器
description: 取消注册微筛选器
ms.assetid: 4af2d4fd-bfbe-4a75-bbfb-2a1c4b5c2032
keywords:
- 正在注销微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f324979ab0975083aeabbf78b227bee33f23446
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541528"
---
# <a name="unregistering-the-minifilter"></a>取消注册微筛选器


## <span id="ddk_unregistering_the_minifilter_if"></span><span id="DDK_UNREGISTERING_THE_MINIFILTER_IF"></span>


微筛选器驱动程序[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)例程必须调用[ **FltUnregisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544606)注销微筛选器驱动程序. 调用**FltUnregisterFilter**会导致发生以下操作：

-   微筛选器驱动程序的回调例程会撤消注册。

-   微筛选器驱动程序的实例数据被破坏向下键，并在微筛选器驱动程序[ **InstanceTeardownStartCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551098)并**InstanceTeardownCompleteCallback**例程为每个微筛选器驱动程序实例调用。

-   如果微筛选器驱动程序上的卷、 实例、 流或流句柄设置任何上下文，将删除这些上下文。 如果微筛选器驱动程序已注册[ **CleanupContext** ](https://msdn.microsoft.com/library/windows/hardware/ff551078)给定的上下文类型的回调例程，筛选器管理器调用*CleanupContext*例程之前正在删除上下文。

如果微筛选器驱动程序的不透明的筛选器指针上有未完成的断开引用**FltUnregisterFilter**进入等待状态，直到它们被删除。 因为已调用了微筛选器驱动程序，通常会发生未处理断开引用[ **FltQueueGenericWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff543452)插入到系统工作队列中，工作项和工作项但尚未取消排队和处理。 (筛选器管理器会将断开引用添加当微筛选器驱动程序调用**FltQueueGenericWorkItem**并微筛选器驱动程序的处理例程返回时将其删除。)

如果微筛选器驱动程序已调用任何例程，如添加对微筛选器驱动程序的不透明的筛选器指针的断开引用也会发生未处理断开引用[ **FltObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff543382)或[ **FltGetFilterFromInstance**](https://msdn.microsoft.com/library/windows/hardware/ff543049)，但未随后不调用[ **FltObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff543378)。

 

 




