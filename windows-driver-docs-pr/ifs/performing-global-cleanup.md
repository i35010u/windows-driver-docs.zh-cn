---
title: 执行全局清理
description: 执行全局清理
ms.assetid: 18e0fca0-16ec-4ca9-8b71-47f58f41c46d
keywords:
- 全局清除 WDK 文件系统微筛选器
- 清除全局 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 016a3a204f2fc3df3e25077e85c6edffec46addc
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067374"
---
# <a name="performing-global-cleanup"></a>执行全局清理


## <span id="ddk_performing_global_cleanup_if"></span><span id="DDK_PERFORMING_GLOBAL_CLEANUP_IF"></span>


微筛选器驱动程序的 [**FilterUnloadCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback) 例程必须执行任何所需的全局清理。 以下列表包含了微筛选器驱动程序可能执行的全局清除任务的示例：

-   调用 [**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite) 可删除先前对 [**ExInitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)的调用初始化的全局资源变量。

-   调用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 或 [**ExFreePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag) 以释放之前对例程（如 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)）所分配的全局内存。

-   调用 [**ExDeleteNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist) 或 [**ExDeletePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist) ，以删除先前调用 [**ExInitializeNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist) 或 [**ExInitializePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)分配的后备链表列表。

-   调用 [**PsRemoveCreateThreadNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremovecreatethreadnotifyroutine) 或 [**PsRemoveLoadImageNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremoveloadimagenotifyroutine) ，以取消注册由先前调用 [**PsSetCreateThreadNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine) 或 [**PsSetLoadImageNotifyRoutine**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)注册的全局回调例程。

 

