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
ms.openlocfilehash: 653806bc1e091cc01d259b877ecf2990f8a482e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841501"
---
# <a name="accessing-user-buffers"></a>访问用户缓冲区


特定于给定 i/o 操作的所有参数（包括缓冲区和内存描述符列表（MDLs））在[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)联合中定义。 此联合包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构，可通过[ **\_FLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)的**Iopb**成员访问，\_表示 i/o 操作的数据结构。 筛选器管理器和微筛选器驱动程序都使用**FLT\_回调\_数据**结构来启动和处理 i/o 操作。

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)联合还包含基于 IRP 的操作的任何参数定义，这些操作特定于用于该操作的缓冲方法（缓冲、直接 i/o，或者非缓冲或直接 i/o）。 它还包含非基于 IRP 的操作（fast i/o 和 FsFilter 回调例程）的参数定义。

微筛选器驱动程序可以调用[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters) ，以获取指向 MDL 地址、缓冲区指针、缓冲区长度和 i/o 操作所需的访问参数的指针。 这会使微筛选器驱动程序不会使用 switch 语句在帮助程序例程中查找这些参数的位置，从而可跨多个 i/o 操作访问这些参数。

处理涉及用户缓冲区的 i/o 操作时，微筛选器驱动程序应始终使用 MDL （如果有）。 如果是这样，则微筛选器驱动程序应调用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)来获取 MDL 的系统地址并使用系统地址来访问用户缓冲区。

如果只有一个缓冲区地址可用，则微筛选器驱动程序应始终将访问该缓冲区的任何尝试置于 try/except 块中。 如果微筛选器驱动程序需要访问未同步的 postoperation 回调例程中的缓冲区，或者 i/o 操作发布到工作线程，则微筛选器驱动程序还应该通过调用[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)来锁定用户缓冲区。 此函数根据 i/o 操作类型确定要应用于锁定缓冲区的适当访问方法，并创建指向锁定页面的 MDL。

### <a name="span-idfilter_manager_routines_for_accessing_user_buffersspanspan-idfilter_manager_routines_for_accessing_user_buffersspanspan-idfilter_manager_routines_for_accessing_user_buffersspanfilter-manager-routines-for-accessing-user-buffers"></a><span id="Filter_Manager_Routines_for_Accessing_User_Buffers"></span><span id="filter_manager_routines_for_accessing_user_buffers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_ACCESSING_USER_BUFFERS"></span>用于访问用户缓冲区的筛选器管理器例程

筛选器管理器提供以下支持例程，用于访问 preoperation 和 postoperation 回调例程中的用户缓冲区：

[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)

 

 




