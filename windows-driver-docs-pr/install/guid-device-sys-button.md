---
title: GUID_DEVICE_SYS_BUTTON
description: GUID_DEVICE_SYS_BUTTON
ms.assetid: 6d07e015-3ea5-4951-ab2d-9c110edef1c5
keywords:
- GUID_DEVICE_SYS_BUTTON 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_SYS_BUTTON
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5850f59eebf1d7f3492c2f3ff74a9d44e9673c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546631"
---
# <a name="guiddevicesysbutton"></a>GUID_DEVICE_SYS_BUTTON


GUID_DEVICE_SYS_BUTTON[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)的高级配置和电源接口 (ACPI) 系统电源按钮设备定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVICE_SYS_BUTTON</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{4AFA3D53-74A7-11d0-be5e-00A0C9062857}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)注册此设备接口类，以通知操作系统和应用程序的系统电源按钮设备是否存在的实例。 I8042prt，PS/2 式键盘和鼠标设备的系统提供的驱动程序还会注册支持的系统电源按钮的键盘此类的实例。

了解如何提供 WDM[函数的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff546516)ACPI 的设备，请参阅[支持 ACPI 设备](https://msdn.microsoft.com/library/windows/hardware/ff536161)。

PS/2 式键盘和鼠标设备的信息，请参阅[非 HIDClass 键盘和鼠标设备](../hid/keyboard-and-mouse-class-drivers.md)。

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
<td align="left">Poclass.h （包括 Poclass.h）</td>
</tr>
</tbody>
</table>

 

 





