---
title: DEVPKEY_DrvPkg_Model
description: DEVPKEY_DrvPkg_Model
keywords:
- DEVPKEY_DrvPkg_Model 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_Model
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 21d947b72eb3cb6b565c6a705089dea00ef08099
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816159"
---
# <a name="devpkey_drvpkg_model"></a>DEVPKEY_DrvPkg_Model


DEVPKEY_DrvPkg_Model 设备 [驱动程序包](./driver-packages.md) 属性表示设备实例的模型名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_Model</p></td>
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

可以设置 AddProperty 的 DEVPKEY_DrvPkg_Model 值，该 [**指令**](./inf-addproperty-directive.md) 包含在安装设备的 inf 文件的 [**inf *DDInstall* 部分**](./inf-ddinstall-section.md) 中。 可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_DrvPkg_Model 属性的值。

下面的示例演示如何使用 INF **AddProperty** 指令为 INF *DDInstall* 部分为 "SampleDDInstallSection" 安装的设备设置 DEVPKEY_DrvPkg_Model 值：

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceModel,,,,"DSC-530"
...
```

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


[**INF AddProperty 指令**](./inf-addproperty-directive.md)

[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

