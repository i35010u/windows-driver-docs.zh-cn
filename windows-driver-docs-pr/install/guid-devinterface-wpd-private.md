---
title: GUID_DEVINTERFACE_WPD_PRIVATE
description: GUID_DEVINTERFACE_WPD_PRIVATE
ms.assetid: 50292137-d648-41cf-928e-d72549f6321b
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
ms.openlocfilehash: ba189fd2b06626cd3a2d8b4dda137602b1dbea60
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096873"
---
# <a name="guid_devinterface_wpd_private"></a>GUID_DEVINTERFACE_WPD_PRIVATE


GUID_DEVINTERFACE_WPD_PRIVATE [设备接口类](./overview-of-device-interface-classes.md) 定义 (WPD) 专用 [Windows 便携式设备](https://go.microsoft.com/fwlink/p/?linkid=106527) 。

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

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)

 

