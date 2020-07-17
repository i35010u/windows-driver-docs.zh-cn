---
title: DEVPKEY_DeviceClass_SilentInstall
description: DEVPKEY_DeviceClass_SilentInstall
ms.assetid: db9ff5d2-020f-47bc-a1e3-2b305b5270e9
keywords:
- DEVPKEY_DeviceClass_SilentInstall 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_SilentInstall
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8ce6cddf2f8d396977f1f7383e0452feecf5f8cd
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418327"
---
# <a name="devpkey_deviceclass_silentinstall"></a>DEVPKEY_DeviceClass_SilentInstall


DEVPKEY_DeviceClass_SilentInstall 设备属性表示一个布尔型标志，该标志控制是否应安装[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)中的设备（如果可能），而不显示任何用户界面项。

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
<td align="left"><p>DEVPKEY_DeviceClass_SilentInstall</p></td>
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
<td align="left"><p><strong>SilentInstall</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 DEVPKEY_DeviceClass_SilentInstall 的值设置为 DEVPROP_TRUE，则 Windows 将安装设备驱动程序，而不显示任何用户界面项（如果驱动程序已在驱动程序存储区中预安装）。 否则，Windows 不会禁止显示用户界面项。

设备安装程序类的**SilentInstall**注册表值可由安装类的 inf 文件的 inf [**ClassInstall32 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)中包含的[**inf AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)设置。

可以调用[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)或[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)来检索 DEVPKEY_DeviceClass_SilentInstall 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceClass_SilentInstall 属性键。 通过访问类注册表项下的相应**SilentInstall**注册表值，可以访问此属性的值。 有关如何访问类注册表项下的值项的信息，请参阅[访问类注册表项下的注册表项值](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-registry-entry-values-under-the-class-registry-key)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






