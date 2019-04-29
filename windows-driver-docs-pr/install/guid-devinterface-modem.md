---
title: GUID_DEVINTERFACE_MODEM
description: GUID_DEVINTERFACE_MODEM
ms.assetid: 80f5c063-8b22-422f-8102-4ac1e62241c8
keywords:
- GUID_DEVINTERFACE_MODEM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_MODEM
api_location:
- Ntddmodm.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9f8776a4c7b6a684ccb1d216bf8bf519d78e6482
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363737"
---
# <a name="guiddevinterfacemodem"></a>GUID_DEVINTERFACE_MODEM


GUID_DEVINTERFACE_MODEM[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[调制解调器设备](https://msdn.microsoft.com/library/windows/hardware/ff542573)。

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
<td align="left"><p>GUID_DEVINTERFACE_MODEM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2C7089AA-2E0E-11D1-B114-00C04FC2AAE4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

调制解调器设备的驱动程序注册通知的操作系统和应用程序的调制解调器设备存在此设备接口类的实例。

在 GUID_DEVINTERFACE_MODEM *Ntddmodm.h*仅当 INITGUID 和 DEFINE_GUID 宏的正确版本之前的包含定义正确定义*Ntddmodm.h*。 中定义 DEFINE_GUID 宏*Guiddef.h*。 若要确保正确定义 INITGUID、 DEFINE_GUID 和 GUID_DEVINTERFACE_MODEM，包括头文件中的以下代码：

```cpp
#ifndef INITGUID
#define INITGUID
#include <guiddef.h>
#undef INITGUID
#else 
#include <guiddef.h>
#endif

#include <ntddmodm.h>
...
```

有关调制解调器设备的信息，请参阅[调制解调器设备设计指南](https://msdn.microsoft.com/library/windows/hardware/ff542476)。

使用此设备接口类的示例，请参阅[FakeModem-Unimodem 控制器无调制解调器示例驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256110)WDK 中提供的示例。

[**GUID_CLASS_MODEM** ](guid-class-modem.md)对于此类的新实例，而是使用 GUID_DEVINTERFACE_MODEM 是此设备接口类; 的已过时标识符。

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
<td align="left">Ntddmodm.h （包括 Ntddmodm.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_MODEM**](guid-class-modem.md)

 

 






