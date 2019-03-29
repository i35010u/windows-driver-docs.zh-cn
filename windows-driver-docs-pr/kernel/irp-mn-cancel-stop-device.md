---
title: IRP_MN_CANCEL_STOP_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 7047c266-84b4-4260-ad75-d56c87c8c9ef
keywords:
- IRP_MN_CANCEL_STOP_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 6d0034468905d5507a0b59ba82641e5fbae457b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562780"
---
# <a name="irpmncancelstopdevice"></a>IRP\_MN\_取消\_停止\_设备


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

即插即用 manager 之后的某个时刻发送此 IRP [ **IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)，以通知设备的驱动程序，设备不会被禁用 (Windows 98 / 只是我) 或资源重新配置已停止。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序必须设置**Irp-&gt;IoStatus.Status**于状态\_此 irp 的成功。 如果驱动程序失败时此 IRP，设备是处于不一致的状态。

<a name="operation"></a>操作
---------

按设备父总线驱动程序，然后按设备堆栈中每个更高版本的驱动程序，必须首先处理此 IRP。

在响应此 IRP，驱动程序将设备恢复为已启动状态。 驱动程序启动时在设备处于停止挂起状态已保持任何 Irp。

如果设备已处于活动状态时，驱动程序收到此 IRP，函数或筛选器驱动程序将只需将状态设置为成功，并将 IRP 传递到下一步的驱动程序。 父总线驱动程序完成 IRP。 对于此类取消停止 IRP，函数或筛选器驱动程序不需要设置完成例程。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)有关处理停止 Irp 的详细信息以及处理所有的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

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


[**IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)

 

 




