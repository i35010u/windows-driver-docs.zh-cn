---
title: 从微筛选器 DriverEntry 例程返回状态
description: 从微筛选器 DriverEntry 例程返回状态
ms.assetid: a9448908-f712-43f7-99c0-e02abc1678ed
keywords:
- 状态值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 674dfc788bad0b87b53d289286b8d8482d5dac36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385942"
---
# <a name="returning-status-from-a-minifilter-driverentry-routine"></a>从微筛选器 DriverEntry 例程返回状态


## <span id="ddk_returning_status_from_a_minifilter_driverentry_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_MINIFILTER_DRIVERENTRY_ROUTINE_IF"></span>


微筛选器驱动程序**DriverEntry**例程通常将返回状态\_成功。 但是，如果微筛选器初始化失败， **DriverEntry**例程应返回相应的错误 NTSTATUS 值。

如果**DriverEntry**例程将返回一个状态的值，并不代表成功 NTSTATUS 值，系统就会卸载微筛选器驱动程序。 在微筛选器驱动程序[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)不调用例程。 出于此原因， **DriverEntry**例程必须释放返回一个状态的值，并不代表成功 NTSTATUS 值之前的系统资源分配任何内存。

 

 




