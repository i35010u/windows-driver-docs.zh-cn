---
title: 操作，可以是基于 IRP 的操作或快速的 I/O 操作
description: 操作，可以是基于 IRP 的操作或快速的 I/O 操作
ms.assetid: 768f5744-1aea-4fa8-b81b-d2670d6c878e
keywords:
- 快速 I/O 缓冲区 WDK 文件系统
- 标记成员 WDK 文件系统
- 设备对象标志 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdf46453087e4173551db7f0d8a4ffc76fff27de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352793"
---
# <a name="operations-that-can-be-irp-based-or-fast-io"></a>操作，可以是基于 IRP 的操作或快速的 I/O 操作


## <span id="ddk_operations_that_can_be_irp_based_or_fast_io_if"></span><span id="DDK_OPERATIONS_THAT_CAN_BE_IRP_BASED_OR_FAST_IO_IF"></span>


以下类型的操作可以是基于 IRP 的或快速 I/O 操作：

-   IRP\_MJ\_设备\_控件。 (请注意该 IRP\_MJ\_内部\_设备\_控件始终是基于 IRP 的。)

-   IRP\_MJ\_查询\_信息。 此操作可以是快速的 i/o 操作，如果**FileInformationClass**参数是**FileBasicInformation**， **FileStandardInformation**，或**FileNetworkOpenInformation**。

-   IRP\_MJ\_READ. 微筛选器驱动程序可以设置 FLTFL\_操作\_注册\_跳过\_缓存\_中的 IO 标志[ **FLT\_操作\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544668)结构，以避免接收快速 I/O IRP\_MJ\_读取操作和基于 IRP 的缓存的读取。

-   IRP\_MJ\_WRITE. 微筛选器驱动程序可以设置 FLTFL\_操作\_注册\_跳过\_缓存\_IO 标志中 FLT\_操作\_注册结构，以避免接收快速 I/O IRP\_MJ\_写入操作以及缓存基于 IRP 的写入。

上述任何操作时快速 I/O 操作，它始终使用既不缓冲，也不直接 I/O，即使等效基于 IRP 的操作使用不同的缓冲方法。

当 IRP\_MJ\_设备\_控件是一个快速的 I/O 操作，它将始终使用既不缓冲，也不直接 I/O，而不考虑 IOCTL 的传输类型。

尽管 IRP\_MJ\_锁\_控件可以是基于 IRP 的或快速 I/O 操作，它具有无缓冲区。

 

 




