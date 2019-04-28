---
title: DEVPKEY_DrvPkg_BrandingIcon
description: DEVPKEY_DrvPkg_BrandingIcon
ms.assetid: 4a830401-5677-4fda-a087-407b1246699f
keywords:
- DEVPKEY_DrvPkg_BrandingIcon 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_BrandingIcon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d11bcb467ab7c7e113020f09f189d76a3e78405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335282"
---
# <a name="devpkeydrvpkgbrandingicon"></a>DEVPKEY_DrvPkg_BrandingIcon


DEVPKEY_DrvPkg_BrandingIcon 设备属性表示将设备实例与供应商相关联的图标的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_BrandingIcon</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
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

可以指定一个品牌图标，为.ico 文件或可执行文件内的资源。

图标列表的格式是所述的相同[ **DEVPKEY_DrvPkg_Icon** ](devpkey-drvpkg-icon.md)设备属性。

可以设置的值由 DEVPKEY_DrvPkg_BrandingIcon [ **INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)包含在[ **INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)安装设备的 INF 文件。 可以通过调用检索的值 DEVPKEY_DrvPkg_BrandingIcon [ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)。

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


[**DEVPKEY_DrvPkg_Icon**](devpkey-drvpkg-icon.md)

[**INF AddProperty Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






