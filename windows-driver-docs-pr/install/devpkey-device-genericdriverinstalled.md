---
title: DEVPKEY_Device_GenericDriverInstalled
description: DEVPKEY_Device_GenericDriverInstalled
ms.assetid: 7809bed7-af11-42b0-bcc8-9492c47d92ab
keywords:
- DEVPKEY_Device_GenericDriverInstalled 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_GenericDriverInstalled
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1896ce798a22be19be2e806151dfdc7cd39838ad
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096831"
---
# <a name="devpkey_device_genericdriverinstalled"></a>DEVPKEY_Device_GenericDriverInstalled


DEVPKEY_Device_GenericDriverInstalled 设备属性表示一个布尔值，该值指示为设备实例安装的驱动程序是否只提供基本的设备功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_GenericDriverInstalled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_GenericDriverInstalled 的值。

DEVPKEY_Device_GenericDriverInstalled 的值设置为 DEVPROP_TRUE 以指示已安装基本驱动程序。 否则，属性的值将设置为 DEVPROP_FALSE。

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_GenericDriverInstalled 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

