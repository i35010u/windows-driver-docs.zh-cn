---
title: IRP_MJ_CLEANUP
description: IRP\_MJ\_CLEANUP
ms.assetid: e4593d99-a721-4ab1-82a5-b32b9c312b25
keywords:
- IRP_MJ_CLEANUP 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CLEANUP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3cfcac0ecd2fedb768c79e997c2d4e06fa4b0f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540927"
---
# <a name="irpmjcleanup"></a>IRP\_MJ\_CLEANUP


## <a name="when-sent"></a>发送时间


接收 IRP\_MJ\_清除请求指示文件对象的句柄引用计数归零。 （换句话说，文件对象的所有句柄已关闭。）当用户模式应用程序已调用 Microsoft Win32 时的发送通常**CloseHandle**函数 (或内核模式驱动程序时调用[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)) 的最后一个未完成句柄的文件对象。

请务必注意，当文件对象的所有句柄已关闭，这并不意味着不再使用的文件对象。 系统组件，例如缓存管理器和内存管理器中，可能会保存到文件对象未完成的引用。 这些组件可以仍读取或写入从一个文件，即使 IRP\_MJ\_收到清理请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统控制设备对象，该文件系统驱动程序必须完成 IRP。

否则，文件系统驱动程序应处理的清除请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，该筛选器驱动程序必须完成 IRP。

否则，筛选器驱动程序应将传递到下一步低驱动程序 IRP 堆栈上执行任何所需的处理后。

文件系统筛选器驱动程序编写人员应注意[ **IoCreateStreamFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff548296)导致 IRP\_MJ\_清除请求发送到的文件系统驱动程序堆栈卷。 因为文件系统通常创建流文件对象以外的 IRP 其他操作的副作用\_MJ\_创建，很难可靠地检测到流文件对象创建的筛选器驱动程序。 因此筛选器驱动程序应该会收到 IRP\_MJ\_清理和 IRP\_MJ\_关闭请求对于以前不可见的文件对象。

筛选器驱动程序编写人员应注意，还与不同[ **IoCreateStreamFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548296)， [ **IoCreateStreamFileObjectLite** ](https://msdn.microsoft.com/library/windows/hardware/ff548306)不导致 IRP\_MJ\_清除请求发送到文件系统驱动程序堆栈。 出于此原因，因为文件系统通常创建流文件对象以外的 IRP 其他操作的副作用\_MJ\_创建，很难可靠地检测到流文件对象创建的筛选器驱动程序。 因此筛选器驱动程序应该会收到 IRP\_MJ\_关闭请求对于以前不可见的文件对象。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理清除请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--flags"></a>*Irp-&gt;标志*  
此请求设置以下标志：

IRP\_关闭\_操作

IRP\_同步\_API

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)有关接收最终的完成状态和信息的结构请求的操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;的文件对象*与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_清理，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction* IRP 指定\_MJ\_清理。

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCreateStreamFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548296)

[**IoCreateStreamFileObjectLite**](https://msdn.microsoft.com/library/windows/hardware/ff548306)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_清理 （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550718)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)

 

 






