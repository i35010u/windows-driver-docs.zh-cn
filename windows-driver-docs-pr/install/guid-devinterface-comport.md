---
title: GUID_DEVINTERFACE_COMPORT
description: GUID_DEVINTERFACE_COMPORT
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
ms.openlocfilehash: 42600275b681e37268d3490054a2cf837a310ac0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789835"
---
# <a name="guid_devinterface_comport"></a>GUID_DEVINTERFACE_COMPORT


为[COM 端口](/previous-versions/ff546485(v=vs.85))定义 GUID_DEVINTERFACE_COMPORT[设备接口类](./overview-of-device-interface-classes.md)。

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

串行端口驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在 COM 端口。

系统提供的串行端口函数驱动程序为 [串行端口](../serports/using-serial-sys-and-serenum-sys.md)注册此设备接口类的实例。

以下示例 (Github 上) 为串行端口注册此类的实例：

-   [串行示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)
-   [虚拟串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617963) (UMDF 1.0) 
-   [Virtual serial2 driver 示例](https://go.microsoft.com/fwlink/p/?LinkId=722209) (KMDF) 

[**GUID_CLASS_COMPORT**](guid-class-comport.md) 是此设备接口类的过时标识符;对于此类的新实例，请改用 GUID_DEVINTERFACE_COMPORT。

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
<td align="left">Ntddser (包含 Ntddser) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_COMPORT**](guid-class-comport.md)

