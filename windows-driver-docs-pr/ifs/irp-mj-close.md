---
title: IRP_MJ_CLOSE
description: IRP\_MJ\_CLOSE
ms.assetid: 62bb28de-7f89-4009-9ea9-0aa3d6bca0ed
keywords:
- IRP_MJ_CLOSE 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0397bed8fe7dfb85c62369e3be18259255574c68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522716"
---
# <a name="irpmjclose"></a>IRP\_MJ\_CLOSE


## <a name="when-sent"></a>发送时间


接收 IRP\_MJ\_关闭请求指示文件对象的引用计数已达到零，通常是因为文件系统驱动程序或其他内核模式组件调用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)上的文件对象。 此请求通常遵循清除请求。 但是，这并不意味着，将清除请求后立即收到关闭请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统控制设备对象，该文件系统驱动程序必须执行任何所需的处理后完成 IRP。

否则，文件系统驱动程序应处理关闭请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，该筛选器驱动程序应执行必要的操作来结束与控件设备对象之间的通信并完成 IRP。

否则，筛选器驱动程序应将传递到下一步低驱动程序 IRP 堆栈上执行任何所需的处理，如删除的每个文件和每个文件是由筛选器驱动程序维护对象上下文信息后。

文件系统筛选器驱动程序编写人员应注意[ **IoCreateStreamFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff548296)导致[ **IRP\_MJ\_清理**](irp-mj-cleanup.md)请求发送到文件系统驱动程序堆栈，供该卷。 因为文件系统通常创建流文件对象的操作的副作用以外[ **IRP\_MJ\_创建**](irp-mj-create.md)，很难可靠地检测到的筛选器驱动程序创建流文件对象。 因此筛选器驱动程序应该会收到**IRP\_MJ\_清理**并[ **IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)之前未的文件对象的请求。

筛选器驱动程序编写人员应注意，还与不同[ **IoCreateStreamFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548296)， [ **IoCreateStreamFileObjectLite** ](https://msdn.microsoft.com/library/windows/hardware/ff548306)不会导致[ **IRP\_MJ\_清理**](irp-mj-cleanup.md)请求发送到文件系统驱动程序堆栈。 出于此原因，并因为文件系统通常创建流文件对象的操作的副作用以外[ **IRP\_MJ\_创建**](irp-mj-create.md)，很难筛选器驱动程序若要可靠地检测到流文件对象创建。 因此筛选器驱动程序应该会收到**IRP\_MJ\_关闭**请求对于以前不可见的文件对象。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和 IRP 堆栈位置在处理关闭请求中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--flags"></a>*Irp-&gt;标志*  
此请求设置以下标志：

IRP\_关闭\_操作

IRP\_同步\_API

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)有关接收最终的完成状态和信息的结构请求的操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;的文件对象*与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_关闭，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction* IRP 指定\_MJ\_关闭。

## <a name="see-also"></a>另请参阅


[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCreateStreamFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548296)

[**IoCreateStreamFileObjectLite**](https://msdn.microsoft.com/library/windows/hardware/ff548306)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_关闭 （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550720)

[**IRP\_MJ\_CLEANUP**](irp-mj-cleanup.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**ObDereferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff557724)

 

 






