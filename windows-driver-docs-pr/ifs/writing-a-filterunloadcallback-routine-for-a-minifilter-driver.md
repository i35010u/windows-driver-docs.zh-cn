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
ms.openlocfilehash: 119110e6c9489f95a4cc91ad59bbc2be0de19366
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840927"
---
# <a name="writing-a-filterunloadcallback-routine-for-a-minifilter-driver"></a>为微筛选器驱动程序编写 FilterUnloadCallback 例程


## <span id="ddk_writing_a_filterunloadcallback_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


文件系统微筛选器驱动程序可以选择将 PFLT\_筛选器注册为微筛选器驱动程序的*FilterUnloadCallback*例程[ **\_卸载\_回叫**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)类型的例程。 此回调例程也称为微筛选器驱动程序的*卸载例程*。

无需微筛选器驱动程序即可注册*FilterUnloadCallback*例程。 但是，我们强烈建议使用微筛选器驱动程序注册此回调例程，因为如果微筛选器驱动程序未注册*FilterUnloadCallback*例程，则无法卸载该驱动程序。

若要注册此回调例程，微筛选器驱动程序会在[**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的**FilterUnloadCallback**成员中存储 PFLT\_筛选器的地址\_卸载\_微筛选器驱动程序将作为参数传递到其**DriverEntry**例程中的[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。

本部分包括：

[调用 FilterUnloadCallback 例程时](when-the-filterunloadcallback-routine-is-called.md)

[编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)

 

 




