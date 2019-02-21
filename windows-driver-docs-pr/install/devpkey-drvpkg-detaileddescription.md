---
title: DEVPKEY_DrvPkg_DetailedDescription
description: DEVPKEY_DrvPkg_DetailedDescription
ms.assetid: ee9080d1-8c66-42b3-af48-cb1fbfc332e2
keywords:
- DEVPKEY_DrvPkg_DetailedDescription 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_DetailedDescription
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c16ad58d16baef6ff4214667b1dae7210d477628
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545028"
---
# <a name="devpkeydrvpkgdetaileddescription"></a>DEVPKEY_DrvPkg_DetailedDescription


DEVPKEY_DrvPkg_DetailedDescription 设备属性表示的设备实例功能的详细的说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_DetailedDescription</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>有限的 XML 标记</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

详细的说明字符串是以 XML 格式。 XML 格式使 Windows 以基于支持的超文本标记语言 (HTML) 标记的以下子集的信息的显示格式。 这些标记的操作如下所示的 HTML 标记的操作。

<a href="" id="heading-level-tags"></a>标题级别标记  
&lt;h1&gt;， &lt;h2&gt;， &lt;h3&gt;

<a href="" id="list-tags"></a>列表标记  
&lt;ul&gt;， &lt;ol&gt;， &lt;l i&gt;

<a href="" id="paragraph-tag"></a>段落标记  
&lt;p&gt;

可以设置的值由 DEVPKEY_DrvPkg_DetailedDescription [ **INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)包含在[ **INF *DDInstall*一节**](https://msdn.microsoft.com/library/windows/hardware/ff547344)的安装设备的 INF 文件。 可以通过调用检索的值 DEVPKEY_DrvPkg_DetailedDescription [ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)。

下面是举例说明如何使用 INF **AddProperty**指令，若要设置的情况下 INF 安装的设备实例值的 DEVPKEY_DrvPkg_DetailedDescription *DDInstall*部分"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceDetailedDescription,,,,"<xml><h1>Microsoft DiscoveryCam 530</h1><h2>Overview<h2>The Microsoft DiscoveryCam is great.<p>Really.<p><h2>Features</h2>The Microsoft DiscoveryCam has three features.<ol><li>Feature 1</li><li>Feature 2</li><li>Feature 3</li></ol></xml>"
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
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**INF AddProperty Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






