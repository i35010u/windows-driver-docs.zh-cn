---
title: 执行全局清理
description: 执行全局清理
ms.assetid: 18e0fca0-16ec-4ca9-8b71-47f58f41c46d
keywords:
- 全局清除 WDK 文件系统微筛选器
- 清除全局 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018a6c77b544c540b5dda7ee437dc9d503164ef2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841032"
---
# <a name="performing-global-cleanup"></a>执行全局清理


## <span id="ddk_performing_global_cleanup_if"></span><span id="DDK_PERFORMING_GLOBAL_CLEANUP_IF"></span>


微筛选器驱动程序的[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)例程必须执行任何所需的全局清理。 以下列表包含了微筛选器驱动程序可能执行的全局清除任务的示例：

-   调用[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)可删除先前对[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)的调用初始化的全局资源变量。

-   调用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)或[**ExFreePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)以释放之前对例程（如[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)）所分配的全局内存。

-   调用[**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)或[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)以删除先前调用[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)或[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)分配的后备链表列表。分别.

-   调用[**PsRemoveCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremovecreatethreadnotifyroutine)或[**PsRemoveLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremoveloadimagenotifyroutine)以取消注册由之前对[**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)的调用注册的全局回调例程，或[**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)。

 

 




