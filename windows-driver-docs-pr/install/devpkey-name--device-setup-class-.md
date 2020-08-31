---
title: DEVPKEY_NAME（设备安装程序类）
description: DEVPKEY_NAME（设备安装程序类）
ms.assetid: cc953918-f11a-464c-95cc-ee2a9aa68b7a
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
ms.openlocfilehash: 0f7748759897182f9fbf20267d5264e095ba0dc5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095933"
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

可以调用 [**SetupDiGetClassProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索设备安装程序类的 DEVPKEY_NAME 的值。

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

## <a name="see-also"></a>另请参阅


[**DEVPKEY_DeviceClass_ClassName**](devpkey-deviceclass-classname.md)

[**DEVPKEY_DeviceClass_Name**](devpkey-deviceclass-name.md)

[**SetupDiGetClassProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiGetClassDescription**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona)

[**SetupDiClassNameFromGuid**](/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)

 

