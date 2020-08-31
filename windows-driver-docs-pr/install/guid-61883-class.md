---
title: GUID_61883_CLASS
description: GUID_61883_CLASS
ms.assetid: 3380c42c-3ac4-4d71-9a1b-581ef8c7b57a
keywords:
- GUID_61883_CLASS 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_61883_CLASS
api_location:
- 61883.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e5c6422da564c90296724626e8b1d16a088259cd
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095715"
---
# <a name="guid_61883_class"></a>GUID_61883_CLASS


为 61883[设备安装程序类](./overview-of-device-setup-classes.md)中的设备定义了 GUID_61883_CLASS[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_61883_CLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{7EBEFBC0-3200-11d2-B4C2-00A0C9697D07}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

61883设备安装程序类中的设备驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在61883设备。 61883设备接口类包括支持 IEC-61883 协议的 IEEE 1394 设备。 有关61883设备和驱动程序的信息，请参阅 [IEC-61883 客户端驱动程序](../ieee/iec-61883-client-drivers.md)。

有关1394总线设备的设备安装程序类的信息，请参阅 [**BUS1394_CLASS_GUID**](bus1394-class-guid.md)。

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
<td align="left">61883 (包含 61883) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BUS1394_CLASS_GUID**](bus1394-class-guid.md)

 

