---
title: IRP_MN_SURPRISE_REMOVAL
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 19d6847c-6b64-4552-b8b8-fef1d9b13fc7
keywords:
- IRP_MN_SURPRISE_REMOVAL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 29406ccc147c510639ebc87943a31eec165013e4
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922554"
---
# <a name="irp_mn_surprise_removal"></a>IRP\_MN\_意外\_删除


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x17

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP，通知设备的驱动程序设备不再可用于 i/o 操作。 仅在 Windows 2000 和更高版本的系统上发送此 IRP。

PnP 管理器会在通知用户模式应用程序或其他内核模式组件之前发送此 IRP。 此 IRP 完成后，PnP 管理器将通知已注册的应用程序和驱动程序已删除设备。

当 PnP 管理器发送此 IRP 时，设备可以处于 PnP 状态。

在 Windows 98/Windows Me 上，PnP 管理器不会发送此 IRP。

PnP 管理器在系统线程的上下文中以\_IRQL = 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


None

## <a name="output-parameters"></a>输出参数


None

## <a name="io-status-block"></a>I/o 状态块


驱动程序必须将**Irp-&gt;IOSTATUS**设置为状态\_"成功"。 驱动程序不能使此 IRP 失败。

<a name="operation"></a>操作
---------

此 IRP 首先由设备堆栈顶部的驱动程序处理，然后向下传递到堆栈中的每个较低的驱动程序。

有关此 IRP 的详细信息，请参阅[处理 IRP\_MN\_意外\_删除请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)。 有关支持设备删除的其他信息，请参阅[删除设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)。

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


[**IRP\_MN\_删除\_设备**](irp-mn-remove-device.md)

 

 




