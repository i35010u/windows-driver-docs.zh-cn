---
title: IRP_MN_CANCEL_REMOVE_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 5cadb1e2-7011-42a5-8e41-6473069b25a6
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 8cd7eea40cbe3b1108668c8ca3f61b66ea5dfad5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545575"
---
# <a name="irpmncancelremovedevice"></a>IRP\_MN\_CANCEL\_REMOVE\_DEVICE


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，以通知设备的驱动程序将不会删除设备。

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

在响应此 IRP，驱动程序将设备恢复为之前接收的状态**IRP\_MN\_查询\_删除\_设备**请求。

如果设备已启动时驱动程序收到此 IRP，驱动程序只需将状态设置为成功和将 IRP 传递给下一步的驱动程序 （或完成 IRP，如果该驱动程序是总线驱动程序）。 对于此类取消删除 IRP，函数或筛选器驱动程序不需要设置完成例程。 设备可能无法在删除挂起状态下，由于，例如，驱动器失败以前**IRP\_MN\_查询\_删除\_设备**。

PnP 管理器会调用任何**EventCategoryTargetDeviceChange**具有 GUID 的通知回调\_目标\_设备\_删除\_后取消**IRP\_MN\_取消\_删除\_设备**请求完成。 通过调用在设备上注册此类回调[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)。 PnP 管理器注册任何用户模式组件还要求对设备上的通知上，通过调用**RegisterDeviceNotification**。

如果在设备上装入文件系统，则它必须撤消删除查询通知的响应中的操作的任何操作。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)有关处理删除 Irp 的详细信息以及处理所有的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

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
<td><p>标头</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)

[**IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)

 

 




