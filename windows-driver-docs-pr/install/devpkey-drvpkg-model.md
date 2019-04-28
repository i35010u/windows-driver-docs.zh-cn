---
title: DEVPKEY_DrvPkg_Model
description: DEVPKEY_DrvPkg_Model
ms.assetid: 54aedf63-50b3-49eb-9638-2984af7de59a
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
ms.openlocfilehash: db83a1fffaf2605b93a6aa91ee37e8779bfe35c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353831"
---
# <a name="devpkeydrvpkgmodel"></a>DEVPKEY_DrvPkg_Model


DEVPKEY_DrvPkg_Model 设备[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)属性表示的模型名称的设备实例。

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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以设置的值由 DEVPKEY_DrvPkg_Model [ **INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)包含在[ **INF *DDInstall*部分** ](https://msdn.microsoft.com/library/windows/hardware/ff547344)的安装设备的 INF 文件。 可以通过调用检索 DEVPKEY_DrvPkg_Model 属性的值[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)。

下面是举例说明如何使用 INF **AddProperty**指令以将设备 INF 安装 DEVPKEY_DrvPkg_Model 的值设置*DDInstall*部分"SampleDDInstallSection":

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
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






