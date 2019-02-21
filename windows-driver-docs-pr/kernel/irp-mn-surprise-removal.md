---
title: IRP_MN_SURPRISE_REMOVAL
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 19d6847c-6b64-4552-b8b8-fef1d9b13fc7
keywords:
- IRP_MN_SURPRISE_REMOVAL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: fb0889a768a4593e713ac9489471c4b6794590fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545938"
---
# <a name="irpmnsurpriseremoval"></a>IRP\_MN\_SURPRISE\_REMOVAL


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP 通知设备的驱动程序设备不再可用于 I/O 操作。 在 Windows 2000 和更高的系统发送此 IRP。

PnP 管理器将此 IRP 发送之前通知用户模式应用程序或其他内核模式组件。 此 IRP 完成后，已注册应用程序和驱动程序的设备已被删除，则通知即插即用管理器。

PnP 管理器发送此 IRP 时，设备可以为任何即插即用状态。

在 Windows 98/Windows Me，即插即用管理器不会发送此 IRP。

PnP 管理器将此 IRP 发送在 IRQL = 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序必须设置**Irp-&gt;IoStatus.Status**于状态\_成功。 驱动程序不得失败此 IRP。

<a name="operation"></a>操作
---------

此 IRP 是首先处理设备堆栈顶部驱动程序，然后向下传递到堆栈中每个较低的驱动程序。

有关此 IRP 的详细信息，请参阅[处理 IRP\_MN\_惊讶\_删除请求](https://msdn.microsoft.com/library/windows/hardware/ff546699)。 支持设备删除的其他信息，请参阅[删除设备](https://msdn.microsoft.com/library/windows/hardware/ff561046)。

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


[**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)

 

 




