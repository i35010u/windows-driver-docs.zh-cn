---
title: IRP_MJ_SHUTDOWN
description: IRP\_MJ\_SHUTDOWN
ms.assetid: 4f7ba339-87f5-4011-8981-de6c31a9239a
keywords:
- IRP_MJ_SHUTDOWN 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SHUTDOWN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c85d543294cf537dd94aa186e6244d9a07c29634
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324457"
---
# <a name="irpmjshutdown"></a>IRP\_MJ\_SHUTDOWN


## <a name="when-sent"></a>发送时间


IRP\_MJ\_关闭请求系统正在关闭时发送的 I/O 管理器或文件系统驱动程序。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统应执行任何必要的清理和完成状态 IRP\_成功。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和 IRP 堆栈位置在处理关闭请求中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_设置\_关闭。

## <a name="see-also"></a>请参阅


[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_关闭 （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550807)

 

 






