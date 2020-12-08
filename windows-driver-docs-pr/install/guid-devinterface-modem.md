---
title: GUID_DEVINTERFACE_MODEM
description: GUID_DEVINTERFACE_MODEM
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
ms.openlocfilehash: 908649289ed0d6d71179f81ec464614f7171ba10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805513"
---
# <a name="guid_devinterface_modem"></a>GUID_DEVINTERFACE_MODEM


为[调制解调器设备](/previous-versions/windows/hardware/modem/ff542573(v=vs.85))定义 GUID_DEVINTERFACE_MODEM[设备接口类](./overview-of-device-interface-classes.md)。

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

调制解调器设备的驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在调制解调器设备。

仅当 INITGUID.H 和 DEFINE_GUID 宏的正确版本在包含 *Ntddmodm* 之前定义时，才会正确定义 *Ntddmodm* 中的 GUID_DEVINTERFACE_MODEM。 DEFINE_GUID 宏是在 *Guiddef* 中定义的。 若要确保正确定义 INITGUID.H、DEFINE_GUID 和 GUID_DEVINTERFACE_MODEM，请在头文件中包含以下代码：

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

有关调制解调器设备的信息，请参阅 [调制解调器设备设计指南](/previous-versions/windows/hardware/modem/ff542476(v=vs.85))。

有关使用此设备接口类的示例，请参阅 WDK 中提供的 [FakeModem-Unimodem 无控制器驱动程序](/samples/browse/) 示例。

[**GUID_CLASS_MODEM**](guid-class-modem.md) 是此设备接口类的过时标识符;对于此类的新实例，请改用 GUID_DEVINTERFACE_MODEM。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddmodm (包含 Ntddmodm) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_MODEM**](guid-class-modem.md)

