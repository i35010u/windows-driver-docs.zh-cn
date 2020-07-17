---
title: DEVPKEY_DeviceClass_Security
description: DEVPKEY_DeviceClass_Security
ms.assetid: e23fd11b-07ee-4375-841d-1fa9c42d5a28
keywords:
- DEVPKEY_DeviceClass_Security 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Security
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2218fa5cb800499582277696d00ce3cabce8484
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418381"
---
# <a name="devpkey_deviceclass_security"></a>DEVPKEY_DeviceClass_Security


DEVPKEY_DeviceClass_Security 设备属性表示[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)的安全描述符结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Security</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-security-descriptor.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](devprop-type-security-descriptor.md)"><strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_SECURITY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以在安装应用程序安装设备安装程序类的过程中或之后设置 DEVPKEY_DeviceClass_Security 的值。 有关如何设置此属性的详细信息，请参阅[创建安全设备安装](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)。

可以通过调用[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)或[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)来检索 DEVPKEY_DeviceClass_Security 的值。 可以通过调用[**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)或[**SetupDiSetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)来设置 DEVPKEY_DeviceClass_Security。

Windows Server 2003 和 Windows XP 支持此属性，但不支持 DEVPKEY_DeviceClass_Security 属性键。 在这些早期版本的 Windows 中，可以使用 SPCRP_SECURITY 标识符来访问此属性的值。 有关如何访问此属性的值的信息，请参阅[检索设备安装程序类 SPCRP_Xxx 属性](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-spcrp-xxx-properties)和[设置设备安装程序类 SPCRP_Xxx 属性](https://docs.microsoft.com/windows-hardware/drivers/install/setting-spcrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

[**SetupDiSetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)

 

 






