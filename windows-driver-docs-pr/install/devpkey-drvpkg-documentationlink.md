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
ms.openlocfilehash: 10297275bd643afca0d5fb81804c9040f8cc88d2
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716908"
---
# <a name="devpkey_drvpkg_documentationlink"></a>DEVPKEY_DrvPkg_DocumentationLink

DEVPKEY_DrvPkg_DocumentationLink 设备属性表示设备实例的文档的 URL。

|Attribute|值|
|----|----|
|**属性键**|DEVPKEY_DrvPkg_DocumentationLink|
|**属性数据类型标识符**|[DEVPROP_TYPE_STRING](devprop-type-string.md)|
|**和**|安装应用程序和安装程序的只读访问|
|**各种?**|是|

## <a name="remarks"></a>备注

文档链接 URL 应是指向包含设备相关信息的文件的链接。 此属性用于为设备提供 Web 辅助的文档。 该文件可以是 HTML 页面、 *.pdf* 文件、 *.doc* 文件或其他文件类型。 唯一的限制是，所有文档内容都必须包含在 URL 指定的文件中。 例如，一个独立的 \* *.htm*文件是有效的， \* 引用其他图形文件的 *.htm*文件无效，并且 \* 包含所引用的图形文件的 " *mta* " Web 存档文件是有效的。

URL 可以包含参数。 例如，以下 URL 包含提供值 "DSC530" 的 **生产** 参数、提供值 "34" 的 **rev** 参数，以及提供值 "doc" 的 **类型** 参数：

```cpp
http://www.microsoft.com/redirect?prod=DSC530&rev=34&type=docs
```

Microsoft 不为由 DEVPKEY_DrvPkg_DocumentationLink 属性值指定的网页提供 Web 承载或重定向。 此 URL 必须链接到 [驱动程序包](./driver-packages.md) 提供程序所维护的网页。

当用户单击在安装程序生成的最终用户对话框中显示的网站链接时，Windows 会将以下信息添加到 HTTP 请求，其中包括 DEVPKEY_DrvPkg_DocumentationLink 提供的 URL：

- Windows 版本，由 **pver** 参数指定。 例如，"pver = 6.0" 指定 Windows Vista。

- 按 **sbp** 参数指定的库存保留单位 (SKU) ，可将其设置为每或 pro。 例如，"sbp = pro" 指定专业版。

- 本地标识符 (LCID) ，由 **olcid** 参数指定。 例如，"olcid = 0x804" 指定英语 (标准) 语言。

- 设备的最特定硬件标识符，由 **pnpid** 参数指定。 例如，"pnpid = PCI% 5CVEN_8086% 26DEV_2533% 26SUBSYS_00000000% 26REV_04" 指定 PCI 设备的硬件标识符。

出于隐私原因，HTTP 请求中未包含用户信息和设备序列号。

```cpp
The following example shows the type of HTTP request that would be sent to a web server: http://www.microsoft.com/redirect?prod=DSC530&rev34&type=docs&pver=6.0&spb=pro&olcid=0x409&pnpid=PCI%5CVEN_8086%26DEV_2533%26SUBSYS_00000000%26REV_04
```

可以设置 AddProperty 的 DEVPKEY_DrvPkg_DocumentationLink 值，该 [**指令**](./inf-addproperty-directive.md) 包含在安装设备的 inf 文件的 [**inf *DDInstall* 部分**](./inf-ddinstall-section.md) 中。 可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_DrvPkg_DocumentationLinkproperty 的值。

下面的示例演示如何使用 INF **AddProperty** 指令为 INF *DDInstall* 部分为 "SampleDDInstallSection" 安装的设备设置 DEVPKEY_DrvPkg_DocumentationLink 值：

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection]
DeviceDocumentationLink,,,,"http://www.microsoft.com/redirect?prod=DSC530&rev34&type="docs"
...
```

## <a name="requirements"></a>要求

|要求| 说明|
|----|----|
|版本|在 Windows Vista 和更高版本的 Windows 中可用。|
|标头|Devpkey (包含 Devpkey) |

## <a name="see-also"></a>请参阅

[**INF AddProperty 指令**](./inf-addproperty-directive.md)

[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)