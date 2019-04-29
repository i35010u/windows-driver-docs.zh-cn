---
title: IRP_MN_QUERY_STOP_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 22f58964-23a0-4307-a748-9c1620e30871
keywords:
- IRP_MN_QUERY_STOP_DEVICE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 81dc0f034b028e240b637525b3e5026a5b78b938
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381419"
---
# <a name="irpmnquerystopdevice"></a>IRP\_MN\_查询\_停止\_设备


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

是否可以停止设备来重新平衡资源，即插即用管理器会将此 IRP 发送到查询。

在 Windows 98 上 / 我，即插即用管理器还会发送此 IRP 时设备将被禁用。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。 如果驱动程序不能停用设备，驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_未成功。

总线驱动程序可以设置**Irp-&gt;IoStatus.Status**于状态\_资源\_要求\_已更改为指示成功的 IRP，但也以请求的即插即用管理器重新查询设备发送停止 IRP 之前的资源要求。

<a name="operation"></a>操作
---------

此 IRP 是首先处理设备堆栈顶部驱动程序，然后向下传递到堆栈中每个较低的驱动程序。

在响应此 IRP，Windows 2000 和更高版本的驱动程序指示它是否可以安全地停用的资源重新平衡设备。

在 Windows 98 上 / 我来说，此 IRP 不仅在期间发送资源重新平衡，但还时设备将被禁用。 驱动程序不能区分这两种情况，因为它应继续像该设备已被禁用。 如果有任何打开的句柄到设备，该驱动程序失败，此 IRP。 如果任何句柄不处于打开状态，如中所述，驱动程序应继续[处理 IRP\_MN\_查询\_停止\_设备请求 (Windows 98 / 我)](https://msdn.microsoft.com/library/windows/hardware/ff546684)。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用和播放次要 Irp](plug-and-play-minor-irps.md)。

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


[**IRP\_MN\_CANCEL\_STOP\_DEVICE**](irp-mn-cancel-stop-device.md)

[**IRP\_MN\_DEVICE\_USAGE\_NOTIFICATION**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)

[**IRP\_MN\_STOP\_DEVICE**](irp-mn-stop-device.md)

 

 




