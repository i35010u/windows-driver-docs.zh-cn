---
title: GUID_DEVINTERFACE_DISPLAY_ADAPTER
description: GUID_DEVINTERFACE_DISPLAY_ADAPTER
keywords:
- GUID_DEVINTERFACE_DISPLAY_ADAPTER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_DISPLAY_ADAPTER
api_location:
- Ntddvdeo.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 123e4ae01eca1f640b1ec300836eb13a793bb66b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827075"
---
# <a name="guid_devinterface_display_adapter"></a>GUID_DEVINTERFACE_DISPLAY_ADAPTER


为显示适配器支持的显示视图定义 GUID_DEVINTERFACE_DISPLAY_ADAPTER [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>GUID_DEVINTERFACE_DISPLAY_ADAPTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{5B45201D-F2F2-4F3B-85BB-30FF1F953599}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的显示驱动程序将注册此设备接口类的实例，以通知操作系统和应用程序是否存在显示视图。

有关显示设备的信息，请参阅 [Windows Vista 显示驱动程序模型](../display/windows-vista-display-driver-model-design-guide.md) 和 [Windows 2000 显示驱动程序模型](../display/windows-2000-display-driver-model-design-guide.md)。

有关显示适配器的设备接口类的信息，请参阅 [**GUID_DISPLAY_DEVICE_ARRIVAL**](guid-display-device-arrival.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntddvdeo (包含 Ntddvdeo) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DISPLAY_DEVICE_ARRIVAL**](guid-display-device-arrival.md)

 

