---
title: DEVPKEY_DeviceClass_Icon
description: DEVPKEY_DeviceClass_Icon
ms.assetid: 036b6daf-b5de-4aa0-b7e3-ba0430107938
keywords:
- DEVPKEY_DeviceClass_Icon 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Icon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89dba30cbe839f002d29830f1c397dba6ddb7b3d
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418544"
---
# <a name="devpkey_deviceclass_icon"></a>DEVPKEY_DeviceClass_Icon


DEVPKEY_DeviceClass_Icon 设备属性表示[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)的图标。

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
<td align="left"><p>DEVPKEY_DeviceClass_Icon</p></td>
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
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_DeviceClass_Icon 的值是由安装类的[**Inf ClassInstall32 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)中包含的[**inf AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)设置的。 若要设置 DEVPKEY_DeviceClass_Icon 的值，请使用**AddReg**指令为类设置**图标**注册表项值。

**图标**项值是字符串格式的整数。 如果数字为负数，则该数值的绝对值是 setupapi.dll 中的图标的资源标识符。 如果数字为正，则该数字是类安装程序 DLL 中的图标的资源标识符（如果存在类安装程序）或类属性页提供程序（如果没有类安装程序，并且存在属性页提供程序）。 零值无效。

可以调用[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)或[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)来检索 DEVPKEY_DeviceClass_Icon 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceClass_Icon 属性键。 有关如何在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备安装程序类的小图标的信息，请参阅[访问设备安装程序类的图标属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-icon-properties-of-a-device-setup-class)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiDrawMiniIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)

[**SetupDiLoadClassIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)

 

 






