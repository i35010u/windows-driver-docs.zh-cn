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
ms.openlocfilehash: 2786bc94a56dcca755ea63f47b0dc7d4bd1216fb
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067368"
---
# <a name="registering-a-filterunloadcallback-routine"></a>注册 FilterUnloadCallback 例程

文件系统微筛选器驱动程序可以选择将 [**PFLT_FILTER_UNLOAD_CALLBACK**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)类型的例程注册为微筛选器驱动程序的 *FilterUnloadCallback* 例程。 此回调例程也称为微筛选器驱动程序的 *卸载例程*。

无需微筛选器驱动程序即可注册 *FilterUnloadCallback* 例程。 但是，我们强烈建议使用微筛选器驱动程序注册此回调例程，因为如果微筛选器驱动程序未注册 *FilterUnloadCallback* 例程，则无法卸载该驱动程序。

若要注册此回调例程，微筛选器驱动程序会在[**FLT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的**FilterUnloadCallback**成员中存储 PFLT_FILTER_UNLOAD_CALLBACK 类型例程的地址，微筛选器驱动程序将其作为参数传递到其**DriverEntry**例程中的[**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。