---
title: GUID_DEVINTERFACE_COMPORT
description: GUID_DEVINTERFACE_COMPORT
ms.assetid: ce7fbe64-1445-4702-898e-2fc92f96ebf9
keywords:
- GUID_DEVINTERFACE_COMPORT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_COMPORT
api_location:
- Ntddser.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b2c01ad414ffea9756b38bce9eca80a6d8821d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342361"
---
# <a name="guiddevinterfacecomport"></a>GUID_DEVINTERFACE_COMPORT


GUID_DEVINTERFACE_COMPORT[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[COM 端口](https://msdn.microsoft.com/library/windows/hardware/ff546485)。

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
<td align="left"><p>GUID_DEVINTERFACE_COMPORT</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{86E0D1E0-8089-11D0-9CE4-08003E301F73}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

串行端口的驱动程序注册通知的操作系统和应用程序的 COM 端口存在此设备接口类的实例。

串行端口的系统提供的函数驱动程序注册此设备接口类的实例[串行端口](https://msdn.microsoft.com/library/windows/hardware/ff547451)。

下面的示例 （Github 上） 注册为串行端口的此类的实例：

-   [串行示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)
-   [虚拟串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617963)(UMDF 1.0)
-   [虚拟 serial2 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=722209)(KMDF)

[**GUID_CLASS_COMPORT** ](guid-class-comport.md)对于此类的新实例，而是使用 GUID_DEVINTERFACE_COMPORT 是此设备接口类; 的已过时标识符。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddser.h （包括 Ntddser.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_COMPORT**](guid-class-comport.md)

 

 






