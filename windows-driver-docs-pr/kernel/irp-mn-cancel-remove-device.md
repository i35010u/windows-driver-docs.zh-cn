---
title: IRP_MN_CANCEL_REMOVE_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 5cadb1e2-7011-42a5-8e41-6473069b25a6
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 23a193598412103f347ad07066ae6027a6f741f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828082"
---
# <a name="irp_mn_cancel_remove_device"></a>IRP\_MN\_取消\_删除\_设备


所有 PnP 驱动程序都必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

PnP 管理器发送此 IRP，通知设备的驱动程序设备不会被删除。

PnP 管理器以 IRQL 被动\_级别在系统线程的上下文中发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序必须将**irp&gt;IoStatus**设置为该 IRP 的状态\_成功。 如果驱动程序未通过此 IRP，则设备处于不一致状态。

<a name="operation"></a>操作
---------

此 IRP 必须首先由设备的父总线驱动程序处理，然后由设备堆栈中的每个更高的驱动程序处理。

为响应此 IRP，驱动程序会将设备恢复到在接收**IRP\_MN\_QUERY\_删除\_设备**请求之前的状态。

如果设备已在驱动程序接收到此 IRP 时启动，则驱动程序只需将状态设置为 "成功"，并将 IRP 传递到下一个驱动程序（或者，如果驱动程序是总线驱动程序，则完成 IRP）。 对于这种取消删除 IRP，函数或筛选器驱动程序不需要设置完成例程。 设备可能不处于 "删除挂起" 状态，因为例如，驱动程序未能通过上一个**IRP\_MN\_QUERY\_删除\_设备**。

PnP 管理器通过 GUID\_目标\_设备调用具有 GUID 的任何**EventCategoryTargetDeviceChange**通知回调\_\_删除在**IRP\_MN 后取消\_** 请求完成。 此类回调是通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)在设备上注册的。 PnP 管理器还通过调用**RegisterDeviceNotification**调用在设备上注册了通知的任何用户模式组件。

如果文件系统已装载到设备上，则它必须撤消它为响应查询-删除通知而执行的任何操作。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解有关处理删除 irp 的详细信息以及处理所有[即插即用次要 irp](plug-and-play-minor-irps.md)的常规规则。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)

 

 




