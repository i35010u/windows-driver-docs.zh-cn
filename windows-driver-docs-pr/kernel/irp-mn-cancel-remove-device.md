---
title: IRP_MN_CANCEL_REMOVE_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 5cadb1e2-7011-42a5-8e41-6473069b25a6
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 68e3c96f910d47b093dc0fa75aefe9b9bf7b7d38
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922538"
---
# <a name="irp_mn_cancel_remove_device"></a>IRP\_MN\_取消\_删除\_设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x03

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP，通知设备的驱动程序设备不会被删除。

PnP 管理器在系统线程的上下文中\_以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


None

## <a name="output-parameters"></a>输出参数


None

## <a name="io-status-block"></a>I/o 状态块


对于此 IRP，驱动程序必须将**irp&gt;IOSTATUS**设置\_为状态 "成功"。 如果驱动程序未通过此 IRP，则设备处于不一致状态。

<a name="operation"></a>操作
---------

此 IRP 必须首先由设备的父总线驱动程序处理，然后由设备堆栈中的每个更高的驱动程序处理。

对于此 IRP，驱动程序会将设备返回到接收**IRP\_MN\_\_QUERY 删除\_设备**请求之前的状态。

如果设备已在驱动程序接收到此 IRP 时启动，则驱动程序只需将状态设置为 "成功"，并将 IRP 传递到下一个驱动程序（或者，如果驱动程序是总线驱动程序，则完成 IRP）。 对于这种取消删除 IRP，函数或筛选器驱动程序不需要设置完成例程。 设备可能不处于 "删除挂起" 状态，因为例如，驱动程序失败了以前的**IRP\_MN\_\_查询删除\_设备**。

PnP 管理器调用任何**EventCategoryTargetDeviceChange**通知回调，并\_在\_ **IRP\_MN\_\_CANCEL remove\_设备**请求完成后取消 GUID 目标设备\_删除\_。 此类回调是通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)在设备上注册的。 PnP 管理器还通过调用**RegisterDeviceNotification**调用在设备上注册了通知的任何用户模式组件。

如果文件系统已装载到设备上，则它必须撤消它为响应查询-删除通知而执行的任何操作。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解有关处理删除 irp 的详细信息以及处理所有[即插即用次要 irp](plug-and-play-minor-irps.md)的常规规则。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)

 

 




