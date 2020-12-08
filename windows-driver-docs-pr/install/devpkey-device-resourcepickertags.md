---
title: DEVPKEY_Device_ResourcePickerTags
description: DEVPKEY_Device_ResourcePickerTags
keywords:
- DEVPKEY_Device_ResourcePickerTags 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ResourcePickerTags
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7fb171a2400420d9609387ca99ff05f727ab7e64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821453"
---
# <a name="devpkey_device_resourcepickertags"></a>DEVPKEY_Device_ResourcePickerTags


DEVPKEY_Device_ResourcePickerTags 设备属性表示设备实例的资源选取器标记。

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
<td align="left"><p>DEVPKEY_Device_ResourcePickerTags</p></td>
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
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_RESOURCE_PICKER_TAGS</p>
<p><strong>ResourcePickerTags</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

你可以使用安装设备的 INF 文件的 [**Inf *DDInstall* 部分**](./inf-ddinstall-section.md)中包含的 [**inf AddReg 指令**](./inf-addreg-directive.md)来设置 DEVPKEY_Device_ResourcePickerTags 的值。

可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 PKEY_Device_ResourcePickerTags 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_ResourcePickerTags 属性键。 在这些早期版本的 Windows 上，可以通过访问设备实例的软件密钥下的相应 **ResourcePickerTags** 注册表值来访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [访问设备驱动程序属性](./accessing-device-driver-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](./inf-addreg-directive.md)

[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

