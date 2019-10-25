---
title: 从 FilterUnloadCallback 例程返回状态
description: 从 FilterUnloadCallback 例程返回状态
ms.assetid: 6fdaadc7-860d-49d6-833c-64624f435fd3
keywords:
- status 值 WDK 文件系统
- 返回状态 WDK 文件系统
- 拒绝卸载操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 396875f5222916d2f17123b7af0baa2166850079
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840991"
---
# <a name="returning-status-from-a-filterunloadcallback-routine"></a>从 FilterUnloadCallback 例程返回状态


## <span id="ddk_returning_status_from_a_filterunloadcallback_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)例程通常返回状态\_SUCCESS。

若要拒绝不强制执行的卸载操作，微筛选器驱动程序应返回相应的警告或错误 NTSTATUS 值，如 STATUS\_FLT\_是否\_不\_分离。 有关必需的卸载操作的详细信息，请参阅[FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)and [**PFLT\_FILTER\_unload\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)。

如果*FilterUnloadCallback*例程返回警告或错误 NTSTATUS 值并且卸载操作不是必需的，则不会卸载微筛选器驱动程序。

 

 




