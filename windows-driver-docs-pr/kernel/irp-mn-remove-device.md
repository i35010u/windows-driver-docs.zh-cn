---
title: IRP_MN_REMOVE_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 0d733cbd-2da8-48a5-afc6-e1e6b8f507a1
keywords:
- IRP_MN_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 54a269203a867f81b2c65eb2e57b330d3a47732a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381409"
---
# <a name="irpmnremovedevice"></a>IRP\_MN\_REMOVE\_DEVICE


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器使用此 IRP 将驱动程序，以删除设备的软件表示形式 （设备对象等）。 PnP 管理器将发送此 IRP 惊讶 （用户从其槽而不发出警告之前从该设备），已以有序的方式 （例如，在程序中拔出或弹出硬件用户启动的），而删除了设备或用户请求来更新 driver(s)。

在 Windows 2000 和更高版本的系统，即插即用管理器还会发送此 IRP 如果一个设备堆栈中的驱动程序出现故障[ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md)请求设备。

对于有序设备删除时，即插即用管理器发送[ **IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)之前删除 IRP。 在这种情况下，设备处于挂起删除状态时删除 IRP 到达。 对于在意外设备删除 Microsoft Windows 2000 或更高版本，即插即用管理器发送[ **IRP\_MN\_惊讶\_删除**](irp-mn-surprise-removal.md)之前删除 IRP。 在这种情况下，设备处于意外删除状态时删除 IRP 到达。 启动设备之前，驱动程序还可以接收删除 IRP。 在这种情况下，设备处于非启动状态 IRP 到达时。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序必须设置**Irp-&gt;IoStatus.Status**于状态\_成功。 驱动程序不得失败此 IRP。

<a name="operation"></a>操作
---------

按设备堆栈顶部的驱动程序，然后按每个较低的驱动程序堆栈中，将首先处理此 IRP。

在响应此 IRP，驱动程序执行关闭设备、 删除设备的软件表示形式 （用于保存设备对象等），并释放任何资源的设备等任务。

有关处理此 IRP 的详细信息，请参阅[处理 IRP\_MN\_删除\_设备请求](https://msdn.microsoft.com/library/windows/hardware/ff546687)。 支持设备删除的常规信息，请参阅[删除设备](https://msdn.microsoft.com/library/windows/hardware/ff561046)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

如果总线驱动程序检测到的一个 （或多个） 及其子设备 (子 PDOs) 具有已以物理方式从计算机中删除，总线驱动程序会调用[ **IoInvalidateDeviceRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff549353)报告到的更改PnP 管理器。 PnP 管理器然后发送删除 Irp 消失了任何设备中。

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


[**IoInvalidateDeviceRelations**](https://msdn.microsoft.com/library/windows/hardware/ff549353)

[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)

[**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](irp-mn-cancel-remove-device.md)

[**IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)

[**IRP\_MN\_SURPRISE\_REMOVAL**](irp-mn-surprise-removal.md)

 

 




