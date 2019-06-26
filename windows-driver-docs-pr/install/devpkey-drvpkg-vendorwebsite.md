---
title: DEVPKEY_DrvPkg_VendorWebSite
description: DEVPKEY_DrvPkg_VendorWebSite
ms.assetid: 5a460073-64ec-4f86-af18-ddd065ed03b1
keywords:
- DEVPKEY_DrvPkg_VendorWebSite 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_VendorWebSite
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3bdef72c1e18a29dafbeea7620b763e6083c7ca2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377279"
---
# <a name="devpkeydrvpkgvendorwebsite"></a>DEVPKEY_DrvPkg_VendorWebSite


DEVPKEY_DrvPkg_VendorWebSite 设备属性表示设备实例的供应商 URL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_VendorWebSite</p></td>
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

URL 可以是指向供应商网站，网站或重定向页面中的网页的根目录。 URL 还可以包含参数，例如，以下 URL 包含**prod**提供的产品标识符"DSC530"的参数和一个**rev**提供许多"34"的参数：

```cpp
http://www.microsoft.com/redirect?prod=DSC530&rev=34
```

可以设置的值由 DEVPKEY_DrvPkg_VendorWebSite [ **INF AddProperty 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)包含在[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)的安装设备的 INF 文件。 可以通过调用检索的值 DEVPKEY_DrvPkg_VendorWebSite [ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)。

下面是举例说明如何使用 INF **AddProperty**指令将 DEVPKEY_DrvPkg_VendorWebSite 属性值的情况下 INF 安装的设备*DDInstall*部分"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceVendorWebsite,,,,"http://www.microsoft.com/redirect?prod=DSC530&rev=34"
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


[**INF AddProperty Directive**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)

[**INF *DDInstall*部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






