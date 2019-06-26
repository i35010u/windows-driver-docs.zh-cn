---
title: GUID_DEVICE_MEMORY
description: GUID_DEVICE_MEMORY
ms.assetid: 8351585d-6538-41aa-891a-b7c1e0b75cef
keywords:
- GUID_DEVICE_MEMORY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_MEMORY
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0f16e4bc030dc09e5e0270e14a569b50f5ccc93c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379349"
---
# <a name="guiddevicememory"></a>GUID_DEVICE_MEMORY


GUID_DEVICE_MEMORY[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)的高级配置和电源接口 (ACPI) 内存设备定义。

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
<td align="left"><p>GUID_DEVICE_MEMORY</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{3FD0F03D-92E0-45FB-B75C-5ED8FFB01021}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)注册通知的操作系统和应用程序的 ACPI 内存设备是否存在此设备接口类的实例。

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

 

 





