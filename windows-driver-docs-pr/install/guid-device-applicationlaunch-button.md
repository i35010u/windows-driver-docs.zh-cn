---
title: GUID_DEVICE_APPLICATIONLAUNCH_BUTTON
description: GUID_DEVICE_APPLICATIONLAUNCH_BUTTON
ms.assetid: d2ca6eab-b0a1-4626-94cb-5b0a66ec6a6f
keywords:
- GUID_DEVICE_APPLICATIONLAUNCH_BUTTON 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_APPLICATIONLAUNCH_BUTTON
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 81278aa4aaac7027ffe13708f2698e5f320c97f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533795"
---
# <a name="guiddeviceapplicationlaunchbutton"></a>GUID_DEVICE_APPLICATIONLAUNCH_BUTTON


GUID_DEVICE_APPLICATIONLAUNCH_BUTTON[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为高级配置和电源接口 (ACPI) 应用程序启动按钮定义。

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
<td align="left"><p>GUID_DEVICE_APPLICATIONLAUNCH_BUTTON</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{629758EE-986E-4D9E-8E47-DE27F8AB054D}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)注册此设备接口类，以通知操作系统和应用程序的 ACPI 应用程序的状态的实例启动按钮。

了解如何提供 WDM[函数的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff546516)ACPI 的设备，请参阅[支持 ACPI 设备](https://msdn.microsoft.com/library/windows/hardware/ff536161)。

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

 

 





