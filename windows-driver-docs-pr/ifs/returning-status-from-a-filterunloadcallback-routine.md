---
title: 从 FilterUnloadCallback 例程返回状态
description: 从 FilterUnloadCallback 例程返回状态
keywords:
- status 值 WDK 文件系统
- 返回状态 WDK 文件系统
- 拒绝卸载操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 433a8fb83704bd68a8ce83a2a1503ebec04e4a22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803561"
---
# <a name="returning-status-from-a-filterunloadcallback-routine"></a>从 FilterUnloadCallback 例程返回状态


## <span id="ddk_returning_status_from_a_filterunloadcallback_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的 [**FilterUnloadCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback) 例程通常返回状态 " \_ 成功"。

若要拒绝不强制执行的卸载操作，微筛选器驱动程序应返回相应的警告或错误 NTSTATUS 值，如 STATUS \_ FLT \_ \_ 不 \_ 分离。 有关必需的卸载操作的详细信息，请参阅 [编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md) 和 [**PFLT \_ 筛选器 \_ 卸载 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)。

如果 *FilterUnloadCallback* 例程返回警告或错误 NTSTATUS 值并且卸载操作不是必需的，则不会卸载微筛选器驱动程序。

 

