---
title: DEVPKEY_DeviceClass_ClassInstaller
description: DEVPKEY_DeviceClass_ClassInstaller
ms.assetid: 7bde624e-37e5-4603-bf8c-1122b7090ab2
keywords:
- DEVPKEY_DeviceClass_ClassInstaller 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassInstaller
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fa18fcbf899424927e03e3c24cd0cf68c93f5eb6
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096161"
---
# <a name="devpkey_deviceclass_classinstaller"></a>DEVPKEY_DeviceClass_ClassInstaller


DEVPKEY_DeviceClass_ClassInstaller 设备属性表示 [设备安装程序类](./overview-of-device-setup-classes.md)的类安装程序。

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
<td align="left"><p>DEVPKEY_DeviceClass_ClassInstaller</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>"<em>class-installer</em>，<em>子类</em>"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>对应的注册表值名称</strong></p></td>
<td align="left"><p><strong>Installer32</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_DeviceClass_ClassInstaller 的值是类注册表项下的 **Installer32** 注册表值的值。 此条目包含类安装程序 DLL 的名称和设备安装程序类的安装程序入口点。

设备安装程序类的**Installer32**注册表值可由安装设备安装程序类的 inf 文件的[**inf ClassInstall32 部分**](./inf-classinstall32-section.md)中包含的[**inf AddReg 指令**](./inf-addreg-directive.md)设置。

可以调用 [**SetupDiGetClassProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索 DEVPKEY_DeviceClass_ClassInstaller 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceClass_ClassInstaller 属性键。 通过访问类注册表项下的相应 **Installer32** 注册表值，可以访问此属性的值。 有关如何访问类注册表项下的值项的信息，请参阅 [访问类注册表项下的注册表项值](./accessing-registry-entry-values-under-the-class-registry-key.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**INF AddReg 指令**](./inf-addreg-directive.md)

[**INF ClassInstall32 节**](./inf-classinstall32-section.md)

[**SetupDiGetClassProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

