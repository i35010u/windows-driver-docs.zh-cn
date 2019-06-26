---
title: 从 FilterUnloadCallback 例程返回状态
description: 从 FilterUnloadCallback 例程返回状态
ms.assetid: 6fdaadc7-860d-49d6-833c-64624f435fd3
keywords:
- 状态值 WDK 文件系统
- 返回状态 WDK 文件系统
- 拒绝卸载操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7522f437a838eca3783c5e2c94da2165e25edb33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385944"
---
# <a name="returning-status-from-a-filterunloadcallback-routine"></a>从 FilterUnloadCallback 例程返回状态


## <span id="ddk_returning_status_from_a_filterunloadcallback_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)例程通常将返回状态\_成功。

若要拒绝不强制执行卸载操作，微筛选器驱动程序应返回类似于状态适当的警告或错误 NTSTATUS 值\_FLT\_不要\_不\_分离。 有关强制卸载操作的详细信息，请参阅[编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)并[ **PFLT\_筛选器\_卸载\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback).

如果*FilterUnloadCallback*例程返回警告或错误 NTSTATUS 值和卸载操作不是强制性，则微筛选器驱动程序将不会卸载。

 

 




