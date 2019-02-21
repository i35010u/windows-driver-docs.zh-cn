---
title: 执行全局清理
description: 执行全局清理
ms.assetid: 18e0fca0-16ec-4ca9-8b71-47f58f41c46d
keywords:
- 全局清理 WDK 文件系统微筛选器
- 清理全局 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d6420a1275a74761c329237354664b3c38de7e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541497"
---
# <a name="performing-global-cleanup"></a>执行全局清理


## <span id="ddk_performing_global_cleanup_if"></span><span id="DDK_PERFORMING_GLOBAL_CLEANUP_IF"></span>


微筛选器驱动程序[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)例程必须执行任何所需的全局清除。 以下列表包含全局清除微筛选器驱动程序可能执行的任务的示例：

-   调用[ **ExDeleteResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544578)若要删除的以前调用已初始化的全局资源变量[ **ExInitializeResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545317).

-   调用[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)或[ **ExFreePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544593)来释放已分配到如例程的以前调用的全局内存[**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)。

-   调用[ **ExDeleteNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff544566)或[ **ExDeletePagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff544570)删除后备链列表由分配对上一个调用[ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)或[ **ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)，分别。

-   调用[ **PsRemoveCreateThreadNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559947)或[ **PsRemoveLoadImageNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559949)注销全局回调例程已注册的上一个调用[ **PsSetCreateThreadNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559954)或[ **PsSetLoadImageNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559957)分别。

 

 




