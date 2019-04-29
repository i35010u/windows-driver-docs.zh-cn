---
title: GUID_DEVINTERFACE_WPD
description: GUID_DEVINTERFACE_WPD
ms.assetid: 611d1866-2530-4acb-8c83-77c29bdd128c
keywords:
- GUID_DEVINTERFACE_WPD 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_WPD
api_location:
- Portabledevice.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2260f30e0b6d1bf026cbed3298bdaea1a2b95bcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370006"
---
# <a name="guiddevinterfacewpd"></a>GUID_DEVINTERFACE_WPD


GUID_DEVINTERFACE_WPD[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[Windows 便携设备](https://go.microsoft.com/fwlink/p/?linkid=106527)(WPD)。

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
<td align="left"><p>GUID_DEVINTERFACE_WPD</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6AC27878-A6FA-4155-BA85-F98F491D4F33}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

支持 WPD 设备驱动程序接口 (DDI) 的设备驱动程序注册 GUID_DEVINTERFACE_WPD WPD 设备存在所通知的操作系统和应用程序的实例。

WPD 类扩展组件注册使用 WPD 类扩展的 WPD 驱动程序此设备接口的实例。

使用 WPD 设备的客户端应注册此设备接口类的实例到达接收通知。

客户端可以枚举 WPD 设备要注册此接口通过调用**IPortableDeviceManager::GetDevices** （Windows SDK 中所述）。

有关专用 WPD 设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_WPD_PRIVATE**](guid-devinterface-wpd-private.md)。

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
<td align="left"><p>在 Windows Vista、 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Portabledevice.h （包括 Portabledevice.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_WPD_PRIVATE**](guid-devinterface-wpd-private.md)

 

 






