---
title: 从微筛选器 DriverEntry 例程返回状态
description: 从微筛选器 DriverEntry 例程返回状态
ms.assetid: a9448908-f712-43f7-99c0-e02abc1678ed
keywords:
- status 值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 294188f08ede91af1902887a3e9b906bf72432c9
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062996"
---
# <a name="returning-status-from-a-minifilter-driverentry-routine"></a>从微筛选器 DriverEntry 例程返回状态


## <span id="ddk_returning_status_from_a_minifilter_driverentry_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_MINIFILTER_DRIVERENTRY_ROUTINE_IF"></span>


微筛选器驱动程序的 **DriverEntry** 例程通常返回状态 " \_ 成功"。 但如果微筛选器初始化失败， **DriverEntry** 例程应返回相应的错误 NTSTATUS 值。

如果 **DriverEntry** 例程返回的状态值不是成功的 NTSTATUS 值，系统将通过卸载微筛选器驱动程序来做出响应。 不调用微筛选器驱动程序的 [**FilterUnloadCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback) 例程。 出于此原因，在返回不是成功的 NTSTATUS 值的状态值之前， **DriverEntry** 例程必须释放为系统资源分配的任何内存。

 

