---
title: IRP_MN_QUERY_REMOVE_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 95ec9ed8-014f-4d01-bed7-3aeb29cd9e73
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5534a502f0f465fc2f94c9dbe7853100ec199732
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568719"
---
# <a name="irpmnqueryremovedevice"></a>IRP\_MN\_查询\_删除\_设备


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，以通知设备已将要移除从计算机和查询是否可以无需中断在计算机中删除该设备的驱动程序。 PnP 管理器还会发送此 IRP，如果用户请求来更新设备驱动程序。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_未成功。

<a name="operation"></a>操作
---------

此 IRP 是首先处理设备堆栈顶部驱动程序，然后向下传递到堆栈中每个较低的驱动程序。

在响应此 IRP，驱动程序指示是否可以无需中断在计算机中删除该设备。

有关处理此 IRP 的详细信息，请参阅[处理 IRP\_MN\_查询\_删除\_设备请求](https://msdn.microsoft.com/library/windows/hardware/ff546674)。 支持设备删除的常规信息，请参阅[删除设备](https://msdn.microsoft.com/library/windows/hardware/ff561046)。

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

## <a name="see-also"></a>请参阅


[**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](irp-mn-cancel-remove-device.md)

[**IRP\_MN\_DEVICE\_USAGE\_NOTIFICATION**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)

 

 




