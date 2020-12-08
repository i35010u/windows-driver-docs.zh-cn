---
title: 注册 FilterUnloadCallback 例程
description: 注册 FilterUnloadCallback 例程
keywords:
- 文件系统微筛选器驱动程序 WDK，FilterUnloadCallback 例程
- 微筛选器驱动程序 WDK，FilterUnloadCallback 例程
- FilterUnloadCallback
- 卸载例程 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455a14bc8f5a5a4879ecef82e4d029d6992bf3e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829665"
---
# <a name="registering-a-filterunloadcallback-routine"></a>注册 FilterUnloadCallback 例程

文件系统微筛选器驱动程序可以选择将 [**PFLT_FILTER_UNLOAD_CALLBACK**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)类型的例程注册为微筛选器驱动程序的 *FilterUnloadCallback* 例程。 此回调例程也称为微筛选器驱动程序的 *卸载例程*。

无需微筛选器驱动程序即可注册 *FilterUnloadCallback* 例程。 但是，我们强烈建议使用微筛选器驱动程序注册此回调例程，因为如果微筛选器驱动程序未注册 *FilterUnloadCallback* 例程，则无法卸载该驱动程序。

若要注册此回调例程，微筛选器驱动程序会在 [**FLT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的 **FilterUnloadCallback** 成员中存储 PFLT_FILTER_UNLOAD_CALLBACK 类型例程的地址，微筛选器驱动程序将其作为参数传递到其 **DriverEntry** 例程中的 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。
