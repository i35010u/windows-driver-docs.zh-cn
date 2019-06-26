---
title: IRP_MN_DEVICE_ENUMERATED
description: PnP 管理器使用此 I/O 请求数据包 (IRP) 来通知总线驱动程序存在的设备对象并且具有插管理器完全枚举。
ms.date: 08/12/2017
ms.assetid: 50ECF6E1-4FC6-4EEA-BACF-EBAD0329DA2E
keywords:
- IRP_MN_DEVICE_ENUMERATED Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 06ce4ed5f8781a720a2268c020a57deebd0efa71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384944"
---
# <a name="irpmndeviceenumerated"></a>IRP\_MN\_DEVICE\_ENUMERATED


PnP 管理器使用此 I/O 请求数据包 (IRP) 来通知总线驱动程序存在的设备对象并且具有插管理器完全枚举。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器之前通过 GUID 通知用户模式下发送此 IRP\_设备\_枚举。 此 IRP 允许驱动程序为 IRP 提供预处理例程\_MN\_设备\_枚举，如在其他设备属性填充。 此 IRP 主要允许驱动程序，以使用设置的物理设备对象 (PDO) 设备属性[ **IoSetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdevicepropertydata)。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


处理此 IRP 的驱动程序设置[Irp-&gt;IoStatus.Status](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-status-blocks)于状态\_成功或相应的错误状态。

<a name="operation"></a>操作
---------

**IRP\_MN\_设备\_ENUMERATED** IRP 发送到总线驱动程序的 PDO，指示总线驱动程序 PDO 存在。

## <a name="sending-the-irp"></a>发送 IRP


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
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdm.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[Plug and Play 次要 Irp](plug-and-play-minor-irps.md)

 

 




