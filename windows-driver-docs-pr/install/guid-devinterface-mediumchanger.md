---
title: GUID_DEVINTERFACE_MEDIUMCHANGER
description: GUID_DEVINTERFACE_MEDIUMCHANGER
ms.assetid: d7c41c5c-b03b-459e-81b0-b363b4c174b0
keywords:
- GUID_DEVINTERFACE_MEDIUMCHANGER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_MEDIUMCHANGER
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 695e6e51483814a2a98faa8243a46abcbcb5e0d2
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096949"
---
# <a name="guid_devinterface_mediumchanger"></a>GUID_DEVINTERFACE_MEDIUMCHANGER


为中型转换器设备定义 GUID_DEVINTERFACE_MEDIUMCHANGER [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>GUID_DEVINTERFACE_MEDIUMCHANGER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F56310-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的媒体 [更换器驱动程序](../storage/changer-drivers.md) 将注册一个 GUID_DEVINTERFACE_MEDIUMCHANGER 实例，以通知操作系统和应用程序是否存在中型转换器设备。

有关存储驱动程序的详细信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

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
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MediumChangerClassGuid**](mediumchangerclassguid.md)

 

