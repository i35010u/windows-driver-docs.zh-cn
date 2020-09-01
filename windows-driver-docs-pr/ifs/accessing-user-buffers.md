---
title: 访问用户缓冲区
description: 访问用户缓冲区
ms.assetid: 5ab32074-0949-4cdc-8a95-1bded0085ce1
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，用户缓冲区
- 缓冲 WDK 文件系统微筛选器
- 用户缓冲区 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a625a76d92135ea93bf910f71307e75c5df2a3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066228"
---
# <a name="accessing-user-buffers"></a>访问用户缓冲区


特定于给定 i/o 操作的所有参数（包括缓冲区和内存描述符列表 (MDLs) ）在 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 联合中定义。 此联合包含在[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构中，该结构通过表示 I/o 操作的[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)结构的**Iopb**成员访问。 筛选器管理器和微筛选器驱动程序都使用 **FLT \_ 回调 \_ 数据** 结构来启动和处理 i/o 操作。

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)联合还包含基于 IRP 的操作的任何参数定义，这些操作特定于用于该操作的缓冲方法 (缓冲、直接 i/o，或者既非缓冲的，也不是直接 i/o) 。 它还包含基于非 IRP 操作的参数定义 (fast i/o 和 FsFilter 回调例程) 。

微筛选器驱动程序可以调用 [**FltDecodeParameters**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters) ，以获取指向 MDL 地址、缓冲区指针、缓冲区长度和 i/o 操作所需的访问参数的指针。 这会使微筛选器驱动程序不会使用 switch 语句在帮助程序例程中查找这些参数的位置，从而可跨多个 i/o 操作访问这些参数。

处理涉及用户缓冲区的 i/o 操作时，微筛选器驱动程序应始终使用 MDL （如果有）。 如果是这样，则微筛选器驱动程序应调用 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) 来获取 MDL 的系统地址并使用系统地址来访问用户缓冲区。

如果只有一个缓冲区地址可用，则微筛选器驱动程序应始终将访问该缓冲区的任何尝试置于 try/except 块中。 如果微筛选器驱动程序需要访问未同步的 postoperation 回调例程中的缓冲区，或者 i/o 操作发布到工作线程，则微筛选器驱动程序还应该通过调用 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)来锁定用户缓冲区。 此函数根据 i/o 操作类型确定要应用于锁定缓冲区的适当访问方法，并创建指向锁定页面的 MDL。

### <a name="span-idfilter_manager_routines_for_accessing_user_buffersspanspan-idfilter_manager_routines_for_accessing_user_buffersspanspan-idfilter_manager_routines_for_accessing_user_buffersspanfilter-manager-routines-for-accessing-user-buffers"></a><span id="Filter_Manager_Routines_for_Accessing_User_Buffers"></span><span id="filter_manager_routines_for_accessing_user_buffers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_ACCESSING_USER_BUFFERS"></span>用于访问用户缓冲区的筛选器管理器例程

筛选器管理器提供以下支持例程，用于访问 preoperation 和 postoperation 回调例程中的用户缓冲区：

[**FltDecodeParameters**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)

[**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)

 

