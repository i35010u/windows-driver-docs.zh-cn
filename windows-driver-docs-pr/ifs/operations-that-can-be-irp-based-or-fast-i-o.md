---
title: 操作，可以是基于 IRP 的操作或快速的 I/O 操作
description: 操作，可以是基于 IRP 的操作或快速的 I/O 操作
ms.assetid: 768f5744-1aea-4fa8-b81b-d2670d6c878e
keywords:
- fast i/o 缓冲 WDK 文件系统
- 标志成员 WDK 文件系统
- 设备对象标志 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0cdb2070bb47306e271fe66ba396d93d0ad696a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841051"
---
# <a name="operations-that-can-be-irp-based-or-fast-io"></a>操作，可以是基于 IRP 的操作或快速的 I/O 操作


## <span id="ddk_operations_that_can_be_irp_based_or_fast_io_if"></span><span id="DDK_OPERATIONS_THAT_CAN_BE_IRP_BASED_OR_FAST_IO_IF"></span>


以下类型的操作可以是基于 IRP 的操作，也可以是快速 i/o 操作：

-   IRP\_MJ\_设备\_控件。 （请注意，IRP\_MJ\_内部\_设备\_控件始终基于 IRP。）

-   IRP\_MJ\_查询\_信息。 如果**FileInformationClass**参数为**FileBasicInformation**、 **FileStandardInformation**或**FileNetworkOpenInformation**，此操作可为快速 i/o。

-   IRP\_MJ\_读取。 微筛选器驱动程序可以将 FLTFL\_操作设置\_注册\_跳过[**FLT\_操作\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration)结构中\_缓存\_IO 标志，以避免接收快速 i/o IRP\_MJ\_读取操作和缓存的基于 IRP 的读取。

-   IRP\_MJ\_写入。 微筛选器驱动程序可以将 FLTFL\_操作设置\_注册\_跳过\_注册结构中\_缓存\_IO 标志，以避免接收快速 i/o IRP\_MJ\_写入操作和缓存的基于 IRP 的写入。

当这些操作中的任何一种都是快速 i/o 操作时，它将始终不使用缓冲和直接 i/o，即使等效的基于 IRP 的操作使用不同的缓冲方法。

当 IRP\_MJ\_设备\_控件是快速 i/o 操作时，不管 IOCTL 的传输类型如何，它都始终使用未缓冲和直接的 i/o。

尽管 IRP\_MJ\_锁定\_控件可以是基于 IRP 或快速 i/o 操作，但它没有缓冲区。

 

 




