---
title: GUID_DEVICE_THERMAL_ZONE
description: GUID_DEVICE_THERMAL_ZONE
ms.assetid: bbb9abb8-aaff-4f1c-ba8d-96fc5b69676a
keywords:
- GUID_DEVICE_THERMAL_ZONE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_THERMAL_ZONE
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e9b676cf08893fdf50205a83117908b82a980df6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370962"
---
# <a name="guiddevicethermalzone"></a>GUID_DEVICE_THERMAL_ZONE


GUID_DEVICE_THERMAL_ZONE[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)的高级配置和电源接口 (ACPI) 温度区设备定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVICE_THERMAL_ZONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{4AFA3D51-74A7-11d0-be5e-00A0C9062857}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)注册此设备接口类，以通知操作系统和应用程序的散热区域设备是否存在的实例。

了解如何提供 WDM[函数的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)ACPI 的设备，请参阅[支持 ACPI 设备](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Poclass.h （包括 Poclass.h）</td>
</tr>
</tbody>
</table>

 

 





