---
title: GUID_DEVICE_PROCESSOR
description: GUID_DEVICE_PROCESSOR
ms.assetid: 47a70d17-5b30-4bae-9f24-f77f3e26e7fc
keywords:
- GUID_DEVICE_PROCESSOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_PROCESSOR
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f8f617c539af8c4ded01ddb4ea916c0cc7253f2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355993"
---
# <a name="guiddeviceprocessor"></a>GUID_DEVICE_PROCESSOR


GUID_DEVICE_PROCESSOR[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)的高级配置和电源接口 (ACPI) 处理器设备定义。

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
<td align="left"><p>GUID_DEVICE_PROCESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{97FADB10-4E33-40AE-359C-8BEF029DBDD0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)注册此设备接口类，以通知操作系统和应用程序的处理器的设备是否存在的实例。

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
<td align="left"><p>Header</p></td>
<td align="left">Poclass.h （包括 Poclass.h）</td>
</tr>
</tbody>
</table>

 

 





