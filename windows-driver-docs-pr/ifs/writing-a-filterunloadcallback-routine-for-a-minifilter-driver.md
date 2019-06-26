---
title: 为微筛选器驱动程序编写 FilterUnloadCallback 例程
description: 为微筛选器驱动程序编写 FilterUnloadCallback 例程
ms.assetid: 0f4eac6d-08ef-47d5-8c1f-5397f058ecb2
keywords:
- 文件系统微筛选器驱动程序 WDK，FilterUnloadCallback 例程
- 微筛选器驱动程序 WDK，FilterUnloadCallback 例程
- FilterUnloadCallback
- 卸载例程 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3803c30268ba3fe240a32a23e183459db9ec1c95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356327"
---
# <a name="writing-a-filterunloadcallback-routine-for-a-minifilter-driver"></a>为微筛选器驱动程序编写 FilterUnloadCallback 例程


## <span id="ddk_writing_a_filterunloadcallback_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


文件系统微筛选器驱动程序可以选择注册[ **PFLT\_筛选器\_卸载\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)-微筛选器驱动类型化为例程*FilterUnloadCallback*例程。 此回调例程也称为微筛选器驱动程序*卸载例程*。

微筛选器驱动程序不需要注册*FilterUnloadCallback*例程。 但是，我们强烈建议微筛选器驱动程序注册此回调例程，因为如果微筛选器驱动程序不会注册*FilterUnloadCallback*例程，该驱动程序不能卸载。

若要注册此回调例程，微筛选器驱动程序存储的地址 PFLT\_筛选器\_UNLOAD\_回调类型中的例程**FilterUnloadCallback** 成员[ **FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)微筛选器驱动程序将作为参数传递的结构[ **FltRegisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)在其**DriverEntry**例程。

本部分包括：

[当调用 FilterUnloadCallback 例程](when-the-filterunloadcallback-routine-is-called.md)

[编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)

 

 




