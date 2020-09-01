---
title: 'IRP_MJ_SHUTDOWN (IFS) '
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
ms.openlocfilehash: fac4054a0cad7d859a70e8a28fe5d651d1c07767
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067398"
---
# <a name="irp_mj_shutdown-ifs"></a>\_ (IFS 的 IRP MJ \_ 关闭) 


## <a name="when-sent"></a>发送时间


\_ \_ 当关闭系统时，由 I/o 管理器或文件系统驱动程序发送 IRP MJ 关闭请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统应执行任何必要的清理并完成状态为 "成功" 的 IRP \_ 。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>parameters


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理关闭请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 集 \_ 关闭。

## <a name="see-also"></a>请参阅


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ \_ (WDK 内核引用的 IRP 关闭) **](../kernel/irp-mj-shutdown.md)

 

