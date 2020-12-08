---
title: GUID_DEVICE_MESSAGE_INDICATOR
description: GUID_DEVICE_MESSAGE_INDICATOR
keywords:
- GUID_DEVICE_MESSAGE_INDICATOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_MESSAGE_INDICATOR
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 915df09201da4c729709655ce3173de620cd6974
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796067"
---
# <a name="guid_device_message_indicator"></a>GUID_DEVICE_MESSAGE_INDICATOR


为高级配置和电源接口 (ACPI) 消息指示器设备定义 GUID_DEVICE_MESSAGE_INDICATOR [设备接口类](./overview-of-device-interface-classes.md) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVICE_MESSAGE_INDICATOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{CD48A365-FA94-4CE2-A232-A1B764E5D8B4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 [ACPI 驱动程序](../kernel/acpi-driver.md) 将注册此设备接口类的实例，通知操作系统和应用程序是否存在 ACPI 消息指示器设备。

有关为 ACPI 设备提供 WDM [函数驱动程序](../kernel/function-drivers.md) 的信息，请参阅 [支持 acpi 设备](../acpi/supporting-acpi-devices.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Poclass (包含 Poclass) </td>
</tr>
</tbody>
</table>

 

