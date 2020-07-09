---
title: IRP_MJ_SHUTDOWN （IFS）
description: IRP \_ MJ \_ 关闭
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
ms.openlocfilehash: eff3c2715c08763e86c554e46fda4b46b667f80b
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141318"
---
# <a name="irp_mj_shutdown-ifs"></a>IRP \_ MJ \_ 关闭（IFS）


## <a name="when-sent"></a>发送时间


\_ \_ 当关闭系统时，由 I/o 管理器或文件系统驱动程序发送 IRP MJ 关闭请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统应执行任何必要的清理并完成状态为 "成功" 的 IRP \_ 。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理关闭请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向[**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 集 \_ 关闭。

## <a name="see-also"></a>另请参阅


[**IO \_ 堆栈 \_ 位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 关闭（WDK 内核引用）**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)

 

 






