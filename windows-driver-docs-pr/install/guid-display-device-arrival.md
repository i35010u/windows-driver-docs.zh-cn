---
title: GUID_DISPLAY_DEVICE_ARRIVAL
description: GUID_DISPLAY_DEVICE_ARRIVAL
ms.assetid: 4915c6b0-b9a7-4602-ae43-032e20353719
keywords:
- GUID_DISPLAY_DEVICE_ARRIVAL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DISPLAY_DEVICE_ARRIVAL
api_location:
- Ntddvdeo.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2d4dd9e5bbd9e6e38ca0bf954672e8f083cc0c5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096855"
---
# <a name="guid_display_device_arrival"></a>GUID_DISPLAY_DEVICE_ARRIVAL


为[显示适配器](../display/index.md)定义 GUID_DISPLAY_DEVICE_ARRIVAL[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DISPLAY_DEVICE_ARRIVAL</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{1CA05180-A699-450A-9A0C-DE4FBE3DDD89}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[Windows Vista 显示器驱动程序模型](../display/windows-vista-display-driver-model-design-guide.md)的系统提供的组件将注册此设备接口类的实例，通知操作系统和应用程序是否存在显示适配器。

有关显示适配器支持的显示视图的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_DISPLAY_ADAPTER**](guid-devinterface-display-adapter.md)。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddvdeo (包含 Ntddvdeo) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_DISPLAY_ADAPTER**](guid-devinterface-display-adapter.md)

 

