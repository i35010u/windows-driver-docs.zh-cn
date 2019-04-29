---
title: IRP_MJ_FLUSH_BUFFERS
description: IRP\_MJ\_刷新\_缓冲区
ms.assetid: 13df0d84-0320-4d7e-9acc-8f913ba6afaa
keywords:
- IRP_MJ_FLUSH_BUFFERS 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_FLUSH_BUFFERS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e45210a271f6579a896f1aaf0b820ba66f0ae92c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324356"
---
# <a name="irpmjflushbuffers"></a>IRP\_MJ\_刷新\_缓冲区


## <a name="when-sent"></a>发送时间


IRP\_MJ\_刷新\_缓冲区发送请求 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序，如果缓冲的数据需要刷新到磁盘。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**FlushFileBuffers**。 (文件系统驱动程序和文件系统筛选器驱动程序，调用[ **CcFlushCache** ](https://msdn.microsoft.com/library/windows/hardware/ff539082)通常适用于发送 IRP。)

所有文件系统和筛选器驱动程序的维护数据的内部缓冲区必须都处理此 IRP，以便可以在系统关闭保留对文件数据或元数据的更改。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应刷新到磁盘的任何重要数据或元数据与文件对象相关联并完成 IRP。 有关如何处理此 IRP，研究 FASTFAT 示例的详细信息。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应刷新到磁盘的任何重要数据或元数据与文件对象相关联，并在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和 IRP 堆栈位置中处理刷新缓冲区请求中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_刷新\_缓冲区，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_刷新\_缓冲区。

## <a name="see-also"></a>请参阅


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_刷新\_缓冲区 （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550760)

 

 






