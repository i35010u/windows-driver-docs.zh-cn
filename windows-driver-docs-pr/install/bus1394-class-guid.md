---
title: BUS1394_CLASS_GUID
description: BUS1394_CLASS_GUID
keywords:
- BUS1394_CLASS_GUID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- BUS1394_CLASS_GUID
api_location:
- 1394.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: def923563f77b8db783fc1a58b9bcfc50bfc8203
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787529"
---
# <a name="bus1394_class_guid"></a>BUS1394_CLASS_GUID


为[1394 总线设备](../ieee/index.md)定义了 BUS1394_CLASS_GUID[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>BUS1394_CLASS_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6BDD1FC1-810F-11d0-BEC7-08002BE2092F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

1394总线的总线驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在1394总线设备。

有关1394总线的信息，请参阅 [1394 bus 设备](../ieee/index.md)。

WDK 示例包括 [1394api 示例](../ieee/1394-samples-and-diagnostic-tools.md) 应用程序。 此应用程序使用 BUS1394_CLASS_GUID 注册，通知此设备接口类的实例是否存在。

有关支持 IEC-61883 协议的 61883 [设备安装程序类](./overview-of-device-setup-classes.md) 中的 IEEE 1394 设备的设备接口类的信息，请参阅 [**GUID_61883_CLASS**](guid-61883-class.md)。

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
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">1394 .h (包括 1394 .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_61883_CLASS**](guid-61883-class.md)

 

