---
title: IRP_MN_DEVICE_ENUMERATED
description: PnP 管理器使用此 i/o 请求数据包（IRP）通知总线驱动程序，设备对象存在并且已由即插即用管理器完全枚举。
ms.date: 08/12/2017
ms.assetid: 50ECF6E1-4FC6-4EEA-BACF-EBAD0329DA2E
keywords:
- IRP_MN_DEVICE_ENUMERATED 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 24a4ff2d7707eca98779563cffa791d7c71f06b2
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922578"
---
# <a name="irp_mn_device_enumerated"></a>IRP\_MN\_设备\_已枚举


PnP 管理器使用此 i/o 请求数据包（IRP）通知总线驱动程序，设备对象存在并且已由即插即用管理器完全枚举。

## <a name="value"></a>值

0x19

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器会在用户模式被枚举 GUID\_设备\_通知之前发送此 IRP。 此 IRP 允许驱动程序为 IRP\_MN\_设备\_枚举提供预处理例程，如填写其他设备属性。 此 IRP 主要允许驱动程序使用[**IoSetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdevicepropertydata)为物理设备对象（PDO）设置设备属性。

## <a name="input-parameters"></a>输入参数


None

## <a name="output-parameters"></a>输出参数


None

## <a name="io-status-block"></a>I/o 状态块


处理此 IRP 的驱动程序将[irp&gt;IOSTATUS](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-status-blocks)设置为状态\_"成功" 或相应的错误状态。

<a name="operation"></a>操作
---------

**Irp\_\_MN 设备\_枚举**的 IRP 将发送到总线驱动程序的 PDO，指示总线驱动程序 pdo 存在。

## <a name="sending-the-irp"></a>发送 IRP


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
<td><p>版本</p></td>
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdm.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[即插即用次要 IRP](plug-and-play-minor-irps.md)

 

 




