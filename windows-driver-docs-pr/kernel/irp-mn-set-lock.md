---
title: IRP_MN_SET_LOCK
description: 总线驱动程序必须处理此 IRP 为支持设备锁定其子设备 (子 PDOs)。 函数和筛选器驱动程序不处理此请求。
ms.date: 08/12/2017
ms.assetid: d4e09527-f817-4eb5-b0f5-7584de8888b1
keywords:
- IRP_MN_SET_LOCK Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: c100b8c427067239d3b390fea035681cf8de6fb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371851"
---
# <a name="irpmnsetlock"></a>IRP\_MN\_SET\_LOCK


总线驱动程序必须处理此 IRP 为支持设备锁定其子设备 (子 PDOs)。 函数和筛选器驱动程序不处理此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送到直接驱动程序的此 IRP，若要锁定设备，以防止设备弹出，或以解锁设备。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.SetLock.Lock**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构是布尔值，该值指定是否要锁定 (TRUE) 或 (FALSE) 解锁设备。

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


总线驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

如果总线驱动程序不处理此 IRP，则将保留**Irp-&gt;IoStatus.Status**完成 IRP 和时。

函数和筛选器驱动程序不处理此 IRP。 此类驱动程序调用[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，并将传递到下一步的驱动程序 IRP。 未设置函数和筛选器驱动程序[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，请不要修改**Irp-&gt;IoStatus**，并且必须完成 IRP。

<a name="operation"></a>操作
---------

如果为此 IRP，驱动程序返回成功，则确保该设备已锁定或解锁完成 IRP 之前。

请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

 




