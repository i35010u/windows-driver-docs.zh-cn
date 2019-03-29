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
ms.openlocfilehash: f8593d83f89624b486201acbd2b0a2e8bac93483
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565441"
---
# <a name="writing-a-filterunloadcallback-routine-for-a-minifilter-driver"></a>为微筛选器驱动程序编写 FilterUnloadCallback 例程


## <span id="ddk_writing_a_filterunloadcallback_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


文件系统微筛选器驱动程序可以选择注册[ **PFLT\_筛选器\_卸载\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff551085)-微筛选器驱动类型化为例程*FilterUnloadCallback*例程。 此回调例程也称为微筛选器驱动程序*卸载例程*。

微筛选器驱动程序不需要注册*FilterUnloadCallback*例程。 但是，我们强烈建议微筛选器驱动程序注册此回调例程，因为如果微筛选器驱动程序不会注册*FilterUnloadCallback*例程，该驱动程序不能卸载。

若要注册此回调例程，微筛选器驱动程序存储的地址 PFLT\_筛选器\_UNLOAD\_回调类型中的例程**FilterUnloadCallback** 成员[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)微筛选器驱动程序将作为参数传递的结构[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)在其**DriverEntry**例程。

本部分包括：

[当调用 FilterUnloadCallback 例程](when-the-filterunloadcallback-routine-is-called.md)

[编写 FilterUnloadCallback 例程](writing-a-filterunloadcallback-routine.md)

 

 




