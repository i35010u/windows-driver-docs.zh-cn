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
ms.openlocfilehash: 4d8c0eb8229059377ddf572508c2b967badbce3f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715764"
---
# <a name="devpkey_drvpkg_vendorwebsite"></a>DEVPKEY_DrvPkg_VendorWebSite

DEVPKEY_DrvPkg_VendorWebSite 设备属性表示设备实例的供应商 URL。

|Attribute|值|
|----|----|
|**属性键**|DEVPKEY_DrvPkg_VendorWebSite|
|**属性数据类型标识符**|[DEVPROP_TYPE_STRING](devprop-type-string.md)">|
|**和**|安装应用程序和安装程序的只读访问|
|**各种?**|是|

## <a name="remarks"></a>备注

URL 可以是到供应商网站的根、网站中的网页或重定向页面的链接。 URL 还可以包含参数，例如，以下 URL 包含提供产品标识符 "DSC530" 的 **生产** 参数和提供数字 "34" 的 **rev** 参数：

```cpp
http://www.microsoft.com/redirect?prod=DSC530&rev=34
```

可以设置 AddProperty 的 DEVPKEY_DrvPkg_VendorWebSite 值，该 [**指令**](./inf-addproperty-directive.md) 包含在安装设备的 inf 文件的 [**inf DDInstall 部分**](./inf-ddinstall-section.md) 中。 可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_DrvPkg_VendorWebSite 的值。

下面的示例演示如何使用 INF **AddProperty** 指令为 INF *DDInstall* 部分为 "SampleDDInstallSection" 安装的设备设置 DEVPKEY_DrvPkg_VendorWebSite 属性值：

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection]
DeviceVendorWebsite,,,,"http://www.microsoft.com/redirect?prod=DSC530&rev=34"
...
```

## <a name="requirements"></a>要求

|要求|说明|
|----|----|
|版本|在 Windows Vista 和更高版本的 Windows 中可用。|
|标头|Devpkey (包含 Devpkey) |

## <a name="see-also"></a>请参阅

[**INF AddProperty 指令**](./inf-addproperty-directive.md)

[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)