---
title: DEVPKEY_DrvPkg_DocumentationLink
description: DEVPKEY_DrvPkg_DocumentationLink
ms.assetid: a4ae1f6c-edf5-4490-8f92-6d7a24040304
keywords:
- DEVPKEY_DrvPkg_DocumentationLink 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_DocumentationLink
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 264a34e2acde3f4716b94c419656155e14f8c954
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377281"
---
# <a name="devpkeydrvpkgdocumentationlink"></a>DEVPKEY_DrvPkg_DocumentationLink


DEVPKEY_DrvPkg_DocumentationLink 设备属性表示设备实例的文档的 URL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_DocumentationLink</p></td>
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

文档链接 URL 应是指向包含有关设备的信息的文件的链接。 此属性用于提供设备的 Web 访问文档。 该文件可以是 HTML 页 *.pdf*文件中， *.doc*文件或键入其他文件。 唯一的限制是，必须指定 URL 的文件中包含的所有文档内容。 例如， \* *.htm*都是独立的文件是否有效， \* *.htm*指的是其他图形文件的文件不是有效，和一个\* *.mta* web 存档文件包含引用的图形文件是否有效。

该 URL 可以包含参数。 例如，以下 URL 包含**prod**参数提供值"DSC530" **rev**提供的值"34"的参数和一个**类型**参数，提供的值"doc":

```cpp
http://www.microsoft.com/redirect?prod=DSC530&rev=34&type=docs
```

Microsoft 不提供 Web 宿主关系或 DEVPKEY_DrvPkg_DocumentationLink 属性值所指定的网页的重定向。 URL 必须链接到一个网页，通过维护[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)提供程序。

当用户单击安装程序生成的最终用户对话框中显示的网站链接时，Windows 会将以下信息添加到包括 DEVPKEY_DrvPkg_DocumentationLink 所提供的 URL 的 HTTP 请求：

-   与指定的 Windows 版本**pver**参数。 例如，"pver = 6.0"指定 Windows Vista。

-   指定的单品 (SKU) **sbp**参数，可以设置为每个或 pro。 例如，"sbp = pro"指定专业版。

-   由指定的本地标识符 (LCID)、 **olcid**参数。 例如，"olcid = 0x409"指定的英语 （标准） 语言。

-   通过指定设备的最具体的硬件标识符**pnpid**参数。 例如，"pnpid = PCI %5cven_8086%26dev_2533%26SUBSYS_00000000 %26rev_04"指定 PCI 设备的硬件标识符。

出于隐私原因，用户信息和设备的序列号不是包含在 HTTP 请求。

```cpp
The following example shows the type of HTTP request that would be sent to a web server: http://www.microsoft.com/redirect?prod=DSC530&rev34&type=docs&pver=6.0&spb=pro&olcid=0x409&pnpid=PCI%5CVEN_8086%26DEV_2533%26SUBSYS_00000000%26REV_04
```

可以设置的值由 DEVPKEY_DrvPkg_DocumentationLink [ **INF AddProperty 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addproperty-directive)包含在[ **INF *DDInstall*一节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)的安装设备的 INF 文件。 可以通过调用检索的值 DEVPKEY_DrvPkg_DocumentationLinkproperty [ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)。

下面是举例说明如何使用 INF **AddProperty**指令以将设备 INF 安装 DEVPKEY_DrvPkg_DocumentationLink 的值设置*DDInstall*部分"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceDocumentationLink,,,,"http://www.microsoft.com/redirect?prod=DSC530&rev34&type="docs"
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

 

 






