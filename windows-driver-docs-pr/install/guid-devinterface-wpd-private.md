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
ms.openlocfilehash: 69478fb8cf5a752ca320191dc9dd2388582a8ff8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383844"
---
# <a name="guiddevinterfacewpdprivate"></a>GUID_DEVINTERFACE_WPD_PRIVATE


GUID_DEVINTERFACE_WPD_PRIVATE[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为专用化定义[Windows 便携设备](https://go.microsoft.com/fwlink/p/?linkid=106527)(WPD)。

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

GUID_DEVINTERFACE_WPD_PRIVATE 应仅为使用的自定义 WPD 应用程序的专用设备。 泛型 WPD 驱动程序和客户端的 WPD 设备不应使用此设备接口类的实例。

自定义应用程序可以枚举注册的调用此接口的专用设备**IPortableDeviceManager::GetPrivateDevices** （Windows SDK 中所述）。

有关通用 WPD 设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)。

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


[**GUID_DEVINTERFACE_WPD**](guid-devinterface-wpd.md)

 

 






