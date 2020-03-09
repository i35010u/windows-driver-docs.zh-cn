---
title: 注册 FilterUnloadCallback 例程
description: 注册 FilterUnloadCallback 例程
ms.assetid: 0f4eac6d-08ef-47d5-8c1f-5397f058ecb2
keywords:
- 文件系统微筛选器驱动程序 WDK，FilterUnloadCallback 例程
- 微筛选器驱动程序 WDK，FilterUnloadCallback 例程
- FilterUnloadCallback
- 卸载例程 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc31dab494d4e380772ceb6e087836de243c4790
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910534"
---
# <a name="registering-a-filterunloadcallback-routine"></a>注册 FilterUnloadCallback 例程

文件系统微筛选器驱动程序可以选择将[**PFLT_FILTER_UNLOAD_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)类型的例程注册为微筛选器驱动程序的*FilterUnloadCallback*例程。 此回调例程也称为微筛选器驱动程序的*卸载例程*。

无需微筛选器驱动程序即可注册*FilterUnloadCallback*例程。 但是，我们强烈建议使用微筛选器驱动程序注册此回调例程，因为如果微筛选器驱动程序未注册*FilterUnloadCallback*例程，则无法卸载该驱动程序。

若要注册此回调例程，微筛选器驱动程序会在[**FLT_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的**FilterUnloadCallback**成员中存储 PFLT_FILTER_UNLOAD_CALLBACK 类型例程的地址，微筛选器驱动程序将其作为参数传递到其**DriverEntry**例程中的[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。
