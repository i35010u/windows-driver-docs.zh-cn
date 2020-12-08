---
title: DEVPKEY_NAME（设备安装程序类）
description: DEVPKEY_NAME（设备安装程序类）
keywords:
- DEVPKEY_NAME (设备安装程序类) 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Setup Class)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0f600a7f49738bcfb20f347ae2304bb9fa514c2a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801741"
---
# <a name="devpkey_name-device-setup-class"></a>DEVPKEY_NAME（设备安装程序类）


DEVPKEY_NAME 设备属性表示 [设备安装程序类](./overview-of-device-setup-classes.md)的名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_NAME</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

您可以使用 DEVPKEY_NAME 的值，将设备安装程序类标识为用户界面项中的最终用户。

如果设置 DEVPKEY_DeviceClass_Name，则 DEVPKEY_NAME 的值与 [**DEVPKEY_DeviceClass_Name**](devpkey-deviceclass-name.md) 设备属性的值相同。 否则，DEVPKEY_NAME 值与 [**DEVPKEY_DeviceClass_ClassName**](devpkey-deviceclass-classname.md) 设备属性的值相同。

可以调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索设备安装程序类的 DEVPKEY_NAME 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持相应的名称属性。 但是，这些早期版本的 Windows 确实支持与 DEVPKEY_DeviceClass_Name 和 DEVPKEY_DeviceClass_ClassName 对应的属性。

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
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPKEY_DeviceClass_ClassName**](devpkey-deviceclass-classname.md)

[**DEVPKEY_DeviceClass_Name**](devpkey-deviceclass-name.md)

[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiGetClassDescription**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdescriptiona)

[**SetupDiClassNameFromGuid**](/windows/win32/api/setupapi/nf-setupapi-setupdiclassnamefromguida)

 

