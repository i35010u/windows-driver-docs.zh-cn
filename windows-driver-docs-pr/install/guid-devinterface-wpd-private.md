---
title: GUID_DEVINTERFACE_WPD_PRIVATE
description: GUID_DEVINTERFACE_WPD_PRIVATE
keywords:
- GUID_DEVINTERFACE_WPD_PRIVATE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_WPD_PRIVATE
api_location:
- Portabledevice.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a249b2285f1f029c138dd4e93cd1d43a0f8980a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808167"
---
# <a name="guid_devinterface_wpd_private"></a>GUID_DEVINTERFACE_WPD_PRIVATE


GUID_DEVINTERFACE_WPD_PRIVATE [设备接口类](./overview-of-device-interface-classes.md) 定义 (WPD) 专用 [Windows 便携式设备](/previous-versions//ff597729(v=vs.85)) 。

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
<td align="left"><p>GUID_DEVINTERFACE_WPD_PRIVATE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{BA0C718F-4DED-49B7-BDD3-FABE28661211}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

GUID_DEVINTERFACE_WPD_PRIVATE 应仅用于自定义 WPD 应用程序使用的专用设备。 WPD 设备的通用 WPD 驱动程序和客户端不应使用此设备接口类的实例。

自定义应用程序可以通过调用 Windows SDK) 中记录的 **IPortableDeviceManager：： GetPrivateDevices** (来枚举注册此接口的专用设备。

有关通用 WPD 设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)。

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
<td align="left"><p>在 windows Vista、Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Portabledevice (包含 Portabledevice) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)

