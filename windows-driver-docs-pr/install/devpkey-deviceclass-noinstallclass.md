---
title: DEVPKEY_DeviceClass_NoInstallClass
description: DEVPKEY_DeviceClass_NoInstallClass
keywords:
- DEVPKEY_DeviceClass_NoInstallClass 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_NoInstallClass
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13ac1837ec7915038a9000e4a055740cf24f6036
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799519"
---
# <a name="devpkey_deviceclass_noinstallclass"></a>DEVPKEY_DeviceClass_NoInstallClass


DEVPKEY_DeviceClass_NoInstallClass 设备安装程序类属性表示一个布尔型标志，该标志控制 [设备安装程序类](./overview-of-device-setup-classes.md) 中的设备是否显示在 **添加硬件向导** 中。

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
<td align="left"><p>DEVPKEY_DeviceClass_NoInstallClass</p></td>
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
<td align="left"><p><strong>对应的注册表值名称</strong></p></td>
<td align="left"><p><strong>NoInstallClass</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

将 DEVPKEY_DeviceClass_NoInstallClass 的值设置为 DEVPROP_TRUE 指示类中设备的安装不需要最终用户交互。 如果此值未设置为 DEVPROP_TRUE，则添加硬件向导将显示设备安装程序类的设备。

设备安装程序类的 **NoInstallClass** 注册表值可由安装类的 inf 文件的 inf [**ClassInstall32 部分**](./inf-classinstall32-section.md)中包含的 [**inf AddReg 指令**](./inf-addreg-directive.md)设置。

可以调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索 DEVPKEY_DeviceClass_NoInstallClass 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceClass_NoInstallClass 属性键。 通过访问类注册表项下的相应 **NoInstallClass** 注册表值，可以访问此属性的值。 有关如何访问类注册表项下的值项的信息，请参阅 [访问类注册表项下的注册表项值](./accessing-registry-entry-values-under-the-class-registry-key.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](./inf-addreg-directive.md)

[**INF ClassInstall32 节**](./inf-classinstall32-section.md)

[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

