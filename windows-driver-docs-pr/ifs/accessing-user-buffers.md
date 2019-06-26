---
title: 访问用户缓冲区
description: 访问用户缓冲区
ms.assetid: 5ab32074-0949-4cdc-8a95-1bded0085ce1
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，用户缓冲区
- 缓冲区 WDK 文件系统微筛选器
- 用户缓冲区 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2421faf736146662add2de160fb1ac3ec61dbc33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379019"
---
# <a name="accessing-user-buffers"></a>访问用户缓冲区


特定于给定的 I/O 操作，包括缓冲区和内存描述符列出 (MDLs) 的所有参数中都定义[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)联合。 中包含此联合[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构，它通过访问**Iopb**成员[ **FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)结构，它表示在 I/O 操作。 筛选器管理器和使用微筛选器驱动程序**FLT\_回调\_数据**结构来启动和处理 I/O 操作。

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)联合还包含有关特定于该操作使用的缓冲方法的基于 IRP 的操作的任何参数定义 (缓冲，直接 I/O，或既不缓冲，也不直接 I/O)。 它还包含非基于 IRP 的操作 （快速 I/O 和 FsFilter 回调例程） 的参数定义。

微筛选器驱动程序可以调用[ **FltDecodeParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters)若要获取到 MDL 地址的指针，缓冲区的指针、 缓冲区长度和 I/O 操作的所需的访问参数。 这使微筛选器驱动程序无 switch 语句在跨多个 I/O 操作中访问这些参数的帮助器例程中查找这些参数的位置。

在处理涉及用户缓冲区的 I/O 操作时，微筛选器驱动程序应始终会使用 MDL，如果有可用。 如果因此，微筛选器驱动程序应调用[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) MDL 获取系统地址并使用系统地址来访问用户缓冲区。

如果仅有的缓冲区地址，则微筛选器驱动程序应始终将任何尝试访问在一个 try / except 块的缓冲区。 如果微筛选器驱动程序需要访问不同步的 postoperation 回调例程中的缓冲区或 I/O 操作被发布到工作线程时，如果微筛选器驱动程序还应通过调用锁定用户缓冲区[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)。 此函数确定要为锁定缓冲区上的 I/O 操作的类型基于应用的适当的访问方法，并创建指向锁定的页 MDL。

### <a name="span-idfiltermanagerroutinesforaccessinguserbuffersspanspan-idfiltermanagerroutinesforaccessinguserbuffersspanspan-idfiltermanagerroutinesforaccessinguserbuffersspanfilter-manager-routines-for-accessing-user-buffers"></a><span id="Filter_Manager_Routines_for_Accessing_User_Buffers"></span><span id="filter_manager_routines_for_accessing_user_buffers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_ACCESSING_USER_BUFFERS"></span>用于访问用户缓冲区筛选管理器例程

筛选器管理器提供用于访问用户缓冲区 preoperation 和 postoperation 回调例程中的以下支持例程：

[**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)

 

 




