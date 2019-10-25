---
title: IRP_MN_DEVICE_ENUMERATED
description: PnP 管理器使用此 i/o 请求数据包（IRP）通知总线驱动程序，设备对象存在并且已由即插即用管理器完全枚举。
ms.date: 08/12/2017
ms.assetid: 50ECF6E1-4FC6-4EEA-BACF-EBAD0329DA2E
keywords:
- IRP_MN_DEVICE_ENUMERATED 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 51de059536e25608d0c2b3746ab04ba56d27492f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828071"
---
# <a name="irp_mn_device_enumerated"></a>IRP\_MN\_设备\_枚举


PnP 管理器使用此 i/o 请求数据包（IRP）通知总线驱动程序，设备对象存在并且已由即插即用管理器完全枚举。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

仅在向用户模式通知 GUID\_设备\_枚举时，PnP 管理器发送此 IRP。 此 IRP 允许驱动程序为 IRP\_MN\_设备\_枚举提供预处理例程，例如填写其他设备属性。 此 IRP 主要允许驱动程序使用[**IoSetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdevicepropertydata)为物理设备对象（PDO）设置设备属性。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


处理此 IRP 的驱动程序将[irp&gt;IOSTATUS](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-status-blocks)状态设置为状态\_成功或相应的错误状态。

<a name="operation"></a>操作
---------

会将**irp\_MN\_设备\_枚举**的 irp 发送到总线驱动程序的 pdo，以指示总线驱动程序 pdo 存在。

## <a name="sending-the-irp"></a>发送 IRP


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
<td><p>版本</p></td>
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdm。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[即插即用次要 Irp](plug-and-play-minor-irps.md)

 

 




